The Plone Side
==============

collective.fb
-------------

This package contains collective.opengraph. It adds the opengraph metadata to your HTML head section.

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

XXX add few screenshots here




How to customize the behaviour of a AT
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

One of the goals of this package is to allow developers extend the default metadata definition.
It's availabe threw IOpengrapMetatags adapter::

	from collective.opengraph.interfaces IOpengraphMetatags
	from collective.opengraph.viewlets import ATMetatags

        class MyATMetatags(ATMetatags):

	    implements(IOpengrapMetatags)

	    @property
	    def metatags(self):
		tags = super(MyATMetatags, self).metatags
                tags.update({'og:newtype': 'custom value'})
                return tags


You can also customize existing og values::

	from collective.opengraph.interfaces IOpengraphMetatags
	from collective.opengraph.viewlets import ATMetatags

        class AnotherMetatags(ATMetatags):

	    implements(IOpengrapMetatags)

	    @property
            def title(self):
                return '%s - Lorem ipsum' % self.context.Title()


TO DO: how to add extra metadatas to an AT
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
XXX

Authenticate Facebook users
---------------------------
This package has to be done.


How to install it
^^^^^^^^^^^^^^^^^

How to configure it
^^^^^^^^^^^^^^^^^^^