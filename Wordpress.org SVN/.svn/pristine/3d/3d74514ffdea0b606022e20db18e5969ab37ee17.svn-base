<?php
/**
 * Plugin Name: Terms Before Download
 * Plugin URI: http://helgeklein.com/free-tools/terms-download/
 * Description: Shows a popup dialog with terms and conditions (EULA) that must be accepted before a file can be downloaded
 * Version: 1.0.0
 * Author: Helge Klein
 * Author URI: http://helgeklein.com
 * License: GPL2
 */
 
/*  Copyright 2014  Helge Klein  (email: info@helgeklein.com)

    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License, version 2, as 
    published by the Free Software Foundation.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program; if not, write to the Free Software
    Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
*/

// Register the shortcodes
add_shortcode('tbd_link', 'shortcode_handler_tbd_link');
add_shortcode('tbd_terms', 'shortcode_handler_tbd_terms');

//
// Shortcode handler function: add a div with the terms page content to the html
//
// Recognized attributes:
// -  terms_page_id     ->    ID of the terms page displayed in the dialog [required]
// -  dialog_title      ->    The title of the dialog to be displayed [optional]
// -  class             ->    CSS class of the div enclosing the dialog content [optional]
// -  padding           ->    Padding between the dialog frame and the inner content [optional]
// -  width             ->    Width of the dialog [optional]
// -  ok_button_text    ->    Text for the OK button [optional]
//
function shortcode_handler_tbd_terms($atts)
{
   // Set up attribute defaults where nothing has been specified
   extract(shortcode_atts(array(
         'dialog_title'    => 'Terms and Conditions',
         'class'           => 'entry',
         'padding'         => '20px',
         'width'           => '80%',
         'ok_button_text'  => 'I agree to the terms',
         'terms_page_id'   => 0,
      ), $atts));

   // Get the libraries we need
	wp_enqueue_script('jquery');
	wp_enqueue_script('jquery-ui-dialog');
   wp_enqueue_style('wp-jquery-ui-dialog');

   // Get the terms page
   if (empty($terms_page_id))
      return "";
   else
      $terms_page = get_post ($terms_page_id, "OBJECT", "display");

   // Get the terms page content
   $terms_page_content = $terms_page->post_content;
   // Convert double line breaks into paragraphs, replacing \n with <br /> to the string
   $terms_page_content = wpautop($terms_page_content);
   // Remove non-printable characters
   $terms_page_content = preg_replace('/[\x00-\x1F]/u', '', $terms_page_content);
   // HTML-encode double quotes because the string will be enclosed in double quotes
   $terms_page_content = str_replace ('"', "&quot;", $terms_page_content);

   // Build the output string
   $output = <<<EndOfHeredoc

   <script type="text/javascript">
      jQuery(document).ready(function ($)
      {
         if ($('#tbd_terms').length == 0)
            $('body').append("<div id='tbd_terms' title='{$dialog_title}' class='{$class}' style='display:none; padding: {$padding};'>{$terms_page_content}</div>");
      });
   </script>
   
   <script type="text/javascript">
      jQuery(document).ready(function ($)
      {
         // Show the dialog
         $('.tbd_link').click(function (e)
         {
            var url = $(this).data('url');
            var height = $(window).height() * 0.8;
            $("#tbd_terms").dialog(
            {
               dialogClass: 'wp-dialog',
               resizable: false,
               draggable: false,
               modal: true,
               width: "{$width}",
               maxHeight: height,
               buttons:
               {
                  "{$ok_button_text}": function() 
                  {
                     $(this).dialog("close");
                     window.location.href = url;
                  },
                  Cancel: function()
                  {
                     $(this).dialog("close");
                  }
               }
            });
            e.preventDefault();
            e.stopPropagation();
         });

         // Make the dialog stay in place when the user scrolls
         $(window).scroll(function()
         {
            $('#tbd_terms').dialog('option','position','center');
         });
      });
   </script>
   
EndOfHeredoc;

   return $output;
}


//
// Shortcode handler function: create a download link where the terms must be accepted
//
// Recognized attributes:
// -  url               ->    The URL to link to [required]
// -  text              ->    Link text [required if text is not enclosed]
// -  gacategory        ->    Google Analytics Category [optional]
// -  gaaction          ->    Google Analytics Action [optional]
// -  galabel           ->    Google Analytics Label [optional]
//
function shortcode_handler_tbd_link($atts, $content = null)
{
   // Set up attribute defaults where nothing has been specified
   extract(shortcode_atts(array(
         'url'          => '',
         'text'         => '',
         'gacategory'   => '',
         'gaaction'     => '',
         'galabel'      => '',
      ), $atts));
      
   // The link text can either be enclosed or specified via the 'text' parameter
   if (empty($content) == false)
   {
      // Link text is enclosed, ignore 'text' parameter -> allow for nested shortcodes
      $text = do_shortcode($content);
   }

   if (empty($url) || empty($text))
      return "";
      
   // Google Analytics if specified
   $gAnalytics = "";
   if (empty($gacategory) == false && empty($gaaction) == false && empty($galabel) == false)
      $gAnalytics = " onClick=\"_gaq.push(['_trackEvent', '{$gacategory}', '{$gaaction}', '{$galabel}']);\"";

   // Build the output string
   $output = "<a class='tbd_link' href='#' data-url='{$url}'{$gAnalytics}>{$text}</a>";
   
   return $output;
}?>