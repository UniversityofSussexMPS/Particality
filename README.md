# Particality
===================================PARTICALITY DOCUMENTATION==================================
[~1~] changes to hemingway theme

[~2~] plugins

[~3~] adding js to post

[~4~] accessing dashboard

[~5~] accessing server instance

[~6~] other notes and bugs









===============================================================================================


============================================[~1~]==============================================

the following changes were made to the hemingway defult theme files:



-----style.css:



[CHANGE 1]: the following code was added:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
@media screen and (min-width: 1024px) {
    .crunchify-whatsapp {
	display: none !important;
    }
}
 
.crunchify-link {
    padding: 2px 8px 4px 8px !important;
    color: white;
    font-size: 12px;
    border-radius: 2px;
    margin-right: 2px;
    cursor: pointer;
    -moz-background-clip: padding;
    -webkit-background-clip: padding-box;
    box-shadow: inset 0 -3px 0 rgba(0,0,0,.2);
    -moz-box-shadow: inset 0 -3px 0 rgba(0,0,0,.2);
    -webkit-box-shadow: inset 0 -3px 0 rgba(0,0,0,.2);
    margin-top: 2px;
    display: inline-block;
}
 
.crunchify-link:hover,.crunchify-link:active {
    color: white;
}
 
.crunchify-twitter {
    background: #00aced;
}
 
.crunchify-twitter:hover,.crunchify-twitter:active {
    background: #0084b4;
}
 
.crunchify-facebook {
    background: #3B5997;
}
 
.crunchify-facebook:hover,.crunchify-facebook:active {
    background: #2d4372;
}
 
.crunchify-googleplus {
    background: #D64937;
}
 
.crunchify-googleplus:hover,.crunchify-googleplus:active {
    background: #b53525;
}
 
.crunchify-buffer {
    background: #444;
}
 
.crunchify-buffer:hover,.crunchify-buffer:active {
    background: #222;
}
 
.crunchify-pinterest {
    background: #bd081c;
}
 
.crunchify-pinterest:hover,.crunchify-pinterest:active {
    background: #bd081c;
}
 
.crunchify-linkedin {
    background: #0074A1;
}
 
.crunchify-linkedin:hover,.crunchify-linkedin:active {
    background: #006288;
}
 
.crunchify-whatsapp {
    background: #43d854;
}
 
.crunchify-whatsapp:hover,.crunchify-whatsapp:active {
    background: #009688;
}
 
.crunchify-social {
    margin: 20px 0px 25px 0px;
    -webkit-font-smoothing: antialiased;
    font-size: 12px;
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

this was added in order to create the style for custom share buttons at the bottom of posts.

[CHANGE 2]: in block '.blog-title a' font-weight was commented out:

this was to make the title text 'particality' appear thinner.

[CHANGE 3]: in block '.blog-menu a' text-transform and letter-spacing was commented out, display was changed from block to inline:

commenting out was to make the menu option not so large and overpowering and block to inline change was made to make menu thinner.

[CHANGE 4]: in block '.post-meta' font-size was changed from 0.8em too 1.4em and text-transform was commented out:

change from 0.8 too 1.4 was to fix error on iPhone and comment out was so author name was not overpowering.



-----comments.php:



[CHANGE 1]: the whole file has been commented out in the fist line:

this was to remove comments from the website, comment funtionality is still present on the website it it just inaccessable.



-----content.php:




[CHANGE 1]: the following code was commented out:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<span class="post-date"><a href="<?php the_permalink(); ?>" title="<?php the_title(); ?>"><?php the_time(get_option('date_format')); ?></a></span>
		
		<span class="date-sep"> / </span>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

this was to remove the post date from under the title on the home page.

[CHANGE 2]: the following code was commented out:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<span class="date-sep"> / </span>
	
	        <?php comments_popup_link( '<span class="comment">' . __( '0 Comments', 'hemingway' ) . '</span>', __( '1 Comment', 'hemingway' ), __( '% Comments', 'hemingway' ) ); ?>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

this was to remove the comment number from under the title on the home page.



-----footer.php:



[CHANGE 1]: the following code was commented out:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<div class="footer section large-padding bg-dark">
	
		<div class="footer-inner section-inner">
		
			<?php if ( is_active_sidebar( 'footer-a' ) ) : ?>
			
				<div class="column column-1 left">
				
					<div class="widgets">
			
						<?php dynamic_sidebar( 'footer-a' ); ?>
											
					</div>
					
				</div>
				
			<?php endif; ?> <!-- /footer-a -->
				
			<?php if ( is_active_sidebar( 'footer-b' ) ) : ?>
			
				<div class="column column-2 left">
				
					<div class="widgets">
			
						<?php dynamic_sidebar( 'footer-b' ); ?>
											
					</div> <!-- /widgets -->
					
				</div>
				
			<?php endif; ?> <!-- /footer-b -->
								
			<?php if ( is_active_sidebar( 'footer-c' ) ) : ?>
			
				<div class="column column-3 left">
			
					<div class="widgets">
			
						<?php dynamic_sidebar( 'footer-c' ); ?>
											
					</div> <!-- /widgets -->
					
				</div>
				
			<?php endif; ?> <!-- /footer-c -->
			
			<div class="clear"></div>
		
		</div> <!-- /footer-inner -->
	
	</div> <!-- /footer -->
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

this was to make the footer smaller as it was origanaly 5 times as big. >IMPORTANT:- IF YOU WANT TO INCLUED WIDGETS IN THE FOOTER THIS CODE NEEDS TO BE ACTIVE<



-----functions.php:



[CHANGE 1]: the following code was added:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
function crunchify_social_sharing_buttons($content) {
	global $post;
	if(is_singular() || is_home()){
	
		// Get current page URL 
		$crunchifyURL = urlencode(str_replace("ec2-52-205-143-146.compute-1.amazonaws.com/particality/","particality.org/",get_permalink()));
 
		// Get current page title
		$crunchifyTitle = str_replace( ' ', '%20', get_the_title());
		
		// Get Post Thumbnail for pinterest
		$crunchifyThumbnail = wp_get_attachment_image_src( get_post_thumbnail_id( $post->ID ), 'full' );
 
		// Construct sharing URL without using any script
		$twitterURL = 'https://twitter.com/intent/tweet?text='.$crunchifyTitle.'&amp;url='.$crunchifyURL;
		$facebookURL = 'https://www.facebook.com/sharer/sharer.php?u='.$crunchifyURL;
		$googleURL = 'https://plus.google.com/share?url='.$crunchifyURL;
		$bufferURL = 'https://bufferapp.com/add?url='.$crunchifyURL.'&amp;text='.$crunchifyTitle;
		$whatsappURL = 'whatsapp://send?text='.$crunchifyTitle . ' ' . $crunchifyURL;
		$linkedInURL = 'https://www.linkedin.com/shareArticle?mini=true&url='.$crunchifyURL.'&amp;title='.$crunchifyTitle;
 
		// Based on popular demand added Pinterest too
		$pinterestURL = 'https://pinterest.com/pin/create/button/?url='.$crunchifyURL.'&amp;media='.$crunchifyThumbnail[0].'&amp;description='.$crunchifyTitle;
 
		// Add sharing button at the end of page/page content
		$content .= '<!-- Crunchify.com social sharing. Get your copy here: http://crunchify.me/1VIxAsz -->';
		$content .= '<div class="crunchify-social">';
		$content .= '<h5>SHARE ON</h5> <a class="crunchify-link crunchify-twitter" href="'. $twitterURL .'" target="_blank">Twitter</a>';
		$content .= '<a class="crunchify-link crunchify-facebook" href="'.$facebookURL.'" target="_blank">Facebook</a>';
		$content .= '<a class="crunchify-link crunchify-whatsapp" href="'.$whatsappURL.'" target="_blank">WhatsApp</a>';
		$content .= '<a class="crunchify-link crunchify-googleplus" href="'.$googleURL.'" target="_blank">Google+</a>';
		$content .= '<a class="crunchify-link crunchify-buffer" href="'.$bufferURL.'" target="_blank">Buffer</a>';
		$content .= '<a class="crunchify-link crunchify-linkedin" href="'.$linkedInURL.'" target="_blank">LinkedIn</a>';
		$content .= '<a class="crunchify-link crunchify-pinterest" href="'.$pinterestURL.'" target="_blank">Pin It</a>';
		$content .= '</div>';
		
		return $content;
	}else{
		// if not a post/page then don't include sharing button
		return $content;
	}
};
add_filter( 'the_content', 'crunchify_social_sharing_buttons');
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

this was to add the functionality of the custom share buttons. Custom share buttons were needed as plugins would always share naked dns address instead of particality.org addresses the line 

$crunchifyURL = urlencode(str_replace("ec2-52-205-143-146.compute-1.amazonaws.com/particality/","particality.org/",get_permalink()));

fixes this using str_replace.



-----single.php:



[CHANGE 1]: the following code was commented out:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<span class="post-date"><a href="<?php the_permalink(); ?>" title="<?php the_title(); ?>"><?php the_time(get_option('date_format')); ?></a></span>
							
							<span class="date-sep"> / </span>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

this was to remove the post date from under the title on a post page.

[CHANGE 2]: the following code was commented out:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<span class="date-sep"> / </span>

						
				
							
							<?php comments_popup_link( '<span class="comment">' . __( '0 Comments', 'hemingway' ) . '</span>', __( '1 Comment', 'hemingway' ), __( '% Comments', 'hemingway' ) ); ?>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

this was to remove the comment number from under the title on a post page.

[CHANGE 3]: the following code was commented out:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<p class="post-categories"><span class="category-icon"><span class="front-flap"></span></span> <?php the_category(', '); ?></p>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

this was to remove the post categories at the bottom of the screen.











===============================================================================================


============================================[~2~]==============================================


Active pluggins are:

>Google Analytics - connects the wordpress sight to google analyitics easy to use very simple. Settings for this are in settings on the dashboard.

>Jetpack - has lots of extra useful features that are helpful no need to edit (make sure share buttons and beautiful math are turned off though).Jetpack has its own tab on the dashboard.

>Mailchimp forms - used to provide the mail chimp widget settings are very easy to edit. Has its own tab on the dashboard.

>MathJax - automaticaly detects latex in a post and renders it using mathjax very useful and requires knowlage of latex. latex can be just written straight into the post and it will be rendered. Settings for this are in settings on the dashboard.

>Menu Image - allows you to add an image to a menu item used to put 46 px by 46 px image in the sticky header. options for this can be found on the dashboard menu option.

>myStickymenu - this allows you to make the menu bar at the top of the screen a sticky header the name of the menu in css is '.blog-menu'.

>Widget Manager - this allows you to controle which page a widget will show up on, for example it's used to stop the mailchimp form showing on the thankyou page. Has its own tab on the dashboard.

>Wp-D3 - this pluggin allows you to create small javascript files and include extra css and js files by providing links. you can then embed these files into the post. a full description as to how this works is in the next section.










===============================================================================================


============================================[~3~]==============================================

to add javascript to post do the following:

-start on wordpress dashboard and open posts tab.

-click edit on post you wish to edit.

-in the post editor in the toolbar click the wp-d3 button to open up the editor.

-in this window you can type javascript or paste required javascript.

-if external resources are required use the include button and provide the url.

-to perview or update code you must press save first and wait till small 'chart content saved' window shows up.

-if chart content saved does not apprear you must go through the javascript and change all instances of 'function() {' to 'function(){' as space between function and { seems to always cause this error.

-to make code show in post you must use the insert button in the desired location.

-if code does not show make sure that you have changed all code like the following 'select("body").append("svg")' to 'select(".wpd#-##-#").append("svg")' note the .wpd numbers must be the same as in the tab of the editor for example '.wpd3-35-1'

-if moving code from one post to other make sure you change all .wpd for example .wpd0-8-1 change to .wpd3-35-0.

-if you cannot do this like for the case of three js you can create a html file like the one bellow in notepad:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<!doctype html>

<head>
	<title>Title Gose Here</title>
	<meta charset="utf-8">
	
</head>
<body>

<script src="url to include"></script>

<script>

*write js program here*
######################
######################
**********************


</script>
</body>
</html>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-then upload the html file to the server in a desired location using filezilla or some other FTP method.(to do this follow guide on the internet eg. search: filezilla ec2)

-you can then put the program in an iframe by finding the url of the html file and pasting the following line inside the post while the editor is set to text (top right visule/text):
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
<iframe src="url here" width="desired width here" height="desired height here"></iframe>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-this should include with visulisation in the post.














===============================================================================================


============================================[~4~]==============================================

to access the dashboard of wordpress all you need to do is go to the url: http://ec2-52-205-143-146.compute-1.amazonaws.com/particality/wp-admin and use the login details hopefully provided to you.

if the link does not work then you can find the link by going to particality.org right clicking page source. Click the link that is in the source code and on the end of the url type /wp-admin.

if this still doen't work or particality.org is pointing at the wrong url then you must log into amazon web services account at this url: 836573983991.signin.aws.amazon.com/console and use the login details 

hopefully already provided. Navigate to ec2 and make sure your location is set to N. Virginia click on running instances and look for the running instaces public dns.











===============================================================================================


============================================[~5~]==============================================

To connect to the instance you need the .ppk file hopefully provided to you:

-open up PuTTY

-in the host name paste the public ip or dns found on amazon web services as described in 4

-then click and expand the SSH category and select the Auth category

-press the browse button and select the .ppk file.

-click connect.

-in the terminal type ec2-user.

-if you need other things such as the root user password ect they should be provided to you.










===============================================================================================


============================================[~6~]==============================================


if you try and include html in the title eg. <sup>2</sup> it will break the share buttons and the side bar. this is an error to do with the custom share button javascript 
that i couldn't fix.
