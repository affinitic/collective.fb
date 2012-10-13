The Plone Side
==============

collective.fb
-------------

This `package <https://github.com/RedTurtle/collective.fb>`_ contains `collective.opengraph <https://github.com/RedTurtle/collective.opengraph>`_. It adds the opengraph metadata to your HTML head section.

In the future it will include also the PAS plugin to authenticate users using their Facebook's account.

Supported metadata:
 * og:site_name name of the site
 * og:url url of the webpage
 * og:title title of the webpage
 * og:description description of the webpage
 * og:image your webpage image (either 'image' field of your context or collective.contentleadimage one)

from the control panel you can manage following settings:
- the default og:type 
- which content types should be opengraph metadata aware

How to install it
^^^^^^^^^^^^^^^^^

Add collective.fb to your buildout's list of eggs such as::

	[buildout]
	...
	eggs =
		collective.fb
	...

and run the buildout. Start Zope, go to Site Setup -> Add-on Products in your Plone site and install the 'collective.fb' product.


How to configure it
^^^^^^^^^^^^^^^^^^^

Go to "Site Setup" -> "Add on configuration" -> "Collective Opengraph".
The first two information you have to enter are:

* the **Facebook app id**
* the **Facebook app secret**

You can find it in the basic setting of your Facebook app.

Then you have to enter the **app's admins**. 
You can specify more than one admin as a comma separated list of names.
Admins can be both a Facebook user or the id.

If you prefer to use the id, you can go to: https://developers.facebook.com/tools/explorer. There you can obtain the id starting from an username.

For example: https://developers.facebook.com/tools/explorer?method=GET&path=massimo.azzolini
returns::
	{
	  "id": "1306804485", 
	  "name": "Massimo Azzolini", 
	  "first_name": "Massimo", 
	  "last_name": "Azzolini", 
	  "link": "https://www.facebook.com/massimo.azzolini", 
	  "username": "massimo.azzolini", 
	  "gender": "male", 
	  "locale": "en_US"
	}

all of this to obtain an additional metadata::

	<meta property="fb:admins" content="{YOUR_FACEBOOK_USER_ID}"/>

that is needed for some kind of plugins like, for example, the Facebook `Comments <https://developers.facebook.com/docs/reference/plugins/comments/>`_'s one.

Next two fields are about the built-in Facebook object types. See https://developers.facebook.com/docs/opengraph/objects/builtin/ for a complete list.

You have to select the **default opengraph type** (for example 'article') and you can manage the vocabulary of that drop down list in the field **Type of contents**.

At last, you have to choose to which **Content types** all the machinery applies.

As a default none of the content types is selected.

The final result is something like::

	<meta property="og:title" content="Welcome to Plone" />
	<meta property="og:url" content="http://localhost:8080/Plone/front-page" />
	<meta property="og:image" content="http://localhost:8080/Plone/logo.jpg" />
	<meta property="og:site_name" content="Site" />
	<meta property="og:description" content="Congratulations! You have successfully installed Plone." />
	<meta property="og:type" content="article" />
	<meta property="fb:admins" content="1306804485" />
	<meta property="fb:app_id" content="360891567328123" />

and it'll appear in the HEAD of your HTML page.



How to customize the behaviour of a AT
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

One of the goals of this package is also to allow developers extend the default metadata definition.
It's available threw IOpengrapMetatags adapter::

	from collective.opengraph.interfaces IOpengraphMetatags
	from collective.opengraph.viewlets import ATMetatags

        class MyATMetatags(ATMetatags):

	    implements(IOpengrapMetatags)

	    @property
	    def metatags(self):
		tags = super(MyATMetatags, self).metatags
                tags.update({'og:newtype': 'custom value'})
                return tags

In this way you can, for example, define all the contents as 'webpage' in the Site Setup configuration and add custom configuration for news as 'articles' and/or pages as 'blog'.

You can also customize existing og values::

	from collective.opengraph.interfaces IOpengraphMetatags
	from collective.opengraph.viewlets import ATMetatags

        class AnotherMetatags(ATMetatags):

	    implements(IOpengrapMetatags)

	    @property
            def title(self):
                return '%s - Lorem ipsum' % self.context.Title()

In this case, for example, you can manipulate the images of a page to fit the Facebook's restriction.

how to add extra metadatas to an AT
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
XXX

Authenticate Facebook users
---------------------------
This package has to be refactored.


How to install it
^^^^^^^^^^^^^^^^^

How to configure it
^^^^^^^^^^^^^^^^^^^