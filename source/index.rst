Plone and Facebook integration Documentation
============================================

This document is intended for Plone developers who want to:

* let facebook user be authenticated in Plone
* let Plone contents be OpenGraph enabled


Table of Content
================

How to configurate Facebook
===========================

The very first thing you have to do is to create a Facebook application. 

1. Open https://developers.facebook.com/app. Look at that 'Create new app' button. It's your friend.

2. Fill the popover form that appears

.. image:: _static/facebookapp/new-facebook-app.png

3. Pass the security check (captcha).
   This is what you get:

.. image:: _static/facebookapp/myplonefbapp.png

4. Edit the settings and complete the basic configuration with few more data:

   * the domain of your website (e.g. mywebsite.com)
   * (opt.) if you want to have Facebook autentication, select "Website with Facebook Login" and set the URL of your website.
   * (opt.) choose a category

.. image:: _static/facebookapp/basics-myplonefbapp.png


Debug your HTML pages
=====================
There a useful tool that checks how Facebook sees your page: https://developers.facebook.com/tools/debug

For example, checking a News object on a Plone website, this what you can get.

.. image:: _static/facebookapp/debug-page.png

Please, note all of those 'og:xxx' properties that has to be added to a standard Plone page.

There is also a warning about the image loaded in that news. It's about the fact that the usual image_mini is 140x200 and Facebook wants to have at least one 200x200 image set on the 'og:image' property.


Understanding and configuring Facebook permissions
==================================================



TO DO
=====

* Leverage on ATstandard in a custom way
* Custom ATmycustomcontenttype




OpenGraph metadata
------------------
in pratica è la roba di borelli: collective.opengraph risistemata da andrew
- a cosa serve
- come si installa
- come si configura
- i metadati og x un at standard

come customizzare il comportamento di AT
- un adapter es x le img

TODO come avere metadati extra 
- su un altro AT
- su AT standard


Authenticate Facebook users
---------------------------
il PAS plugin di FA
- come si installa
- cosa ottieni
schermate


Other
-----

.. toctree::
   :maxdepth: 1

   glossary
