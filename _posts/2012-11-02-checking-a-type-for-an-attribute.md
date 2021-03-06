---
layout: post
title: Checking a Type for an Attribute
tags: code

---

I needed to be able to detect at run time if an Enum has a specific Attribute on it.  Generalizing it, I came up with this:

Calling:

{% highlight c# %}
var hasFlags = typeof(EnumWithFlags).HasAttribute<FlagsAttribute>();
{% endhighlight %}

Implementation:

{% highlight c# %}
public static Boolean HasAttribute<T>(this Type self) where T : Attribute
{
	if (self == null)
	{
		throw new ArgumentNullException("self");
	}

	return self.GetCustomAttributes(typeof(T), false).Any();
}
{% endhighlight %}

It may only be two lines, but it is very useful none the less.
