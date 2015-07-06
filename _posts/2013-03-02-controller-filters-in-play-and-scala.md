---
layout: post
title: Controller filters in Play and Scala
---

We were chilling with other students enrolled in the coursera Scala class wondering aloud why one would ever use [currying](https://en.wikipedia.org/wiki/Currying). Admittedly, the ability to organize parameter lists for your functions feels somewhat academic, but we have managed to use function currying in ways that we’re really happy with.

In our web app, we have many controllers that respond to different kinds of requests. Some of those controllers respond to simple GET requests that are not expected to alter state on the server. Some respond to POST requests that are expected to change state and also check CSRF tokens. And some other controllers respond to POST requests to Api endpoints for which CSRF tokens are not relevant.

We have a class called ControllerMethod that is flexible enough to handle these general types of requests whether GET or POST or Api POST, and yet can be tailored with the specific logic that should execute for that route.

{% highlight js %}
class ControllerMethod () {
  def apply[A](dbSettings: ControllerDBSettings = WithoutDBConnection)
              (action: Action[A]): Action[A] =
  {
    Action(action.parser) { request =>
      dbSettings match {
        case WithoutDBConnection => action(request)
          ... other cases ...
      }
    }
  }
}
{% endhighlight %}
 
Treating ControllerMethod as a “root method” for controllers, we can use it to streamline our controllers like, for example, the one that returns an egraph:

{% highlight js %}
def getEgraph(id: Long) = controllerMethod {
  Action { implicit request =>
    egraphStore.findFulfilledEgraph(id) match {
      case Some(egraph) => Ok(renderEgraphPage(egraph))
      case None => NotFound("No Egraph found")
    }
  }
}
{% endhighlight %}

This simple pattern eliminates tons of boilerplate code that would otherwise need to be written into each controller. Moreover, the POST controller that handles changes applied to an egraph uses a slightly modified version of controllerMethod. So with minimal variation in code, we treat the POST controller with functionality that you would expect to have, such as a writable database context and protected against CSRF attacks.
 
Currying is not a technique I envisioned using much when I was first introduced to it. But as we matured as Scala devs and left old Java habits behind, we have used this technique to write dozens of controllers (and other classes) across our web app. Based on experience, currying has proven to be an extremely powerful pattern for bringing organizational sanity to our codebase. =)
