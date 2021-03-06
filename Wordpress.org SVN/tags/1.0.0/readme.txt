=== Terms Before Download ===
Contributors: hiroprot
Tags: download,terms,eula,license
Requires at least: 3.5
Tested up to: 3.8.1
Stable tag: 1.0.0
License: GPL2

Shows a popup dialog with terms and conditions (EULA) that must be accepted before a file can be downloaded

== Description ==
Terms Before Download adds a shortcode that can be used instead of HTML anchors to link to downloadable files. If such a link is clicked a popup dialog shows terms and conditions (EULA) which must be accepted for the download to start.

The terms and conditions are read from a Wordpress page. That way there is only a single place to maintain the terms and they can easily be displayed independently of the plugin.

The plugin supports Google Analytics to keep track of the number of downloads.

An example of the plugin in action can be found here: http://helgeklein.com/download/

# Usage

Add the shortcode *tbd_terms* once (!) to each page or post where terms need to be displayed and configure the ID of the page that contains the terms. Example:

[tbd_terms terms_page_id=5670]

The page ID is part of the URL when editing a page in the admin UI. *Example: http://domain.com/wp-admin/post.php?post=5670&action=edit*

Create a link to a downloadable file like this:

[tbd_link url=\"URL\"]link text[/tbd_link]

# Parameters

The following parameters can be used with the shortcode *tbd_terms*:
   
* terms_page_id: ID of the terms page displayed in the dialog [required] 
* dialog_title: The title of the dialog to be displayed [optional] 
* class: CSS class of the div enclosing the dialog content [optional]   
* padding: Padding between the dialog frame and the inner content [optional] 
* width: Width of the dialog [optional] 
* ok_button_text: Text for the OK button [optional]

The following parameters can be used with the shortcode *tbd_link*:
   
* url: The URL to link to [required]
* text: Link text [required if text is not enclosed]
* gacategory: Google Analytics Category [optional]
* gaaction: Google Analytics Action [optional]
* galabel: Google Analytics Label [optional]

== Installation ==

Install the plugin directly through the WordPress Admin dashboard.

== Frequently Asked Questions ==


== Other Notes ==


== Screenshots ==


== Upgrade Notice ==

Upgrades are in line with Wordpress standards.

== Changelog ==

= 1.0.0 =
* Initial release
