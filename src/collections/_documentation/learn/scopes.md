---
title: Scopes and Hubs
sidebar_order: 4
---

When an event is captured and sent to Sentry SDKs will merge that event data with extra
information from the current scope.  SDKs will typically automatically mange the scopes
for you in the framework integrations and you don't need to think about them.  However
you should know what a scope is and how you can use it for your advantage.

## What's a Scope, what's a Hub

You can think of the hub as the central point that our SDKs use to route an
event to Sentry.  When you call `init()` a hub is created and a client and a
blank scope are created on it.  That hub is then associated with the current
thread and will internally hold a stack of scopes.

The scope will hold useful information that should be sent along with the
event.  For instance [contexts]({% link _documentation/learn/context.md %}) or
[breadcrumbs]({% link _documentation/learn/breadcrumbs.md %}) are stored on
the scope.  When a scope is pushed it inherits all data from the parent scope
and when it pops all modifications are reverted.

The default SDK integrations will push and pop scopes intelligently.  For
instance web framework integrations will create and destroy scopes around your
routes or controllers.

## How do the Scope and Hub Work

As you start using an SDK a scope and hub are automatically created for you out
of the box.  The hub you are unlikely to be interacting with directly unless you
are writing an integration or you want to create or destroy scopes.  Scopes on the
other hand are more user facing.  You can at any point in time call
`configure_scope` to modify data stored on the scope.  This is for instance
used to [modify the context]({% link _documentation/learn/context.md %}).

{% capture __alert_content -%}
If you are very curious about how this thread locality thing works here are the
nitty gritty details.  On platforms such as .NET or on Python 3.7 and later we will
use "ambient data" to have either the hub flow with your code or the hub is already
a singleton that internally manages the scope.

Effectively this means that when you spawn a task in .NET and the execution flow is 
not supressed all the context you have bound to the scope in Sentry will flow along.
If however you suppress the flow, you get new scope data.
{% endcapture %}
{%- include components/alert.html
  title="Note"
  content=__alert_content
%}

When you call a global function such as `capture_event` internally Sentry
discovers the current hub and asks it to capture an event.  Internally the hub will
then merge the event with the topmost scope's data.

## Configuring the Scope

The most useful operation when working with scopes is the `configure_scope` function.
It can be used to reconfigure the current scope.  This for instance can be used to
add custom tags or to inform sentry about the currently authenticated user.

{% include components/platform_content.html content_dir='configure-scope' %}

To learn what useful information can be associated with scopes see
[the context documentation]({% link _documentation/learn/context.md %}).