MANDRILL
===================

CONTENTS OF THIS FILE
---------------------

 - Introduction
 - Tested
 - Known Issues
 - Special Thanks
 - Requirements
 - Installation
 - Coming From Drupal?
 - Usage
 - License
 - Credits
 - Maintainers

INTRODUCTION
------------

Integrates Backdrop's mail system with Mandrill transactional emails, a service
by the folks behind MailChimp. Learn more about Mandrill and how to sign up at
[their website](http://mandrill.com). (Or don't, but then this module isn't
terribly useful...)


The Mandrill module, as the name implies, provides integration with Mandrill transactional email, a service of MailChimp. For sites that send a significant amount of email, using a transactional email service is a great way to get modern analytics and reporting, spam compliance features, scale email to bulk levels, and have your email delivered more reliably.

With the Mandrill module, you can also do cool stuff like create rich email templates in Mandrill and assign them to different email-generating modules in Backdrop, so your different types of emails can all be branded differently.

Mandrill plays nice with other mail-system utilizing modules, particularly mailsystem, which is required for Mandrill configuration. Of course, the Mandrill module also plays well with the MailChimp module, which provides specific mass-email functionality like lists and campaigns.

Features Include:

Ability to route site emails through Mandrill, with granular configuration for different mail-generating modules.
A reporting dashboard.
Asynchronous sending options.
Integration with Mandrill's template system, with capacity for simultaneous use of different templates.
Email activity tracking for any Backdrop entity with a valid email address.
Developed by the friendly geeks from ThinkShout, sponsored by Freddy and the rest of the amazing team from MailChimp. Read more about the 1.3 release on the ThinkShout blog.

TESTED
-----

Email Modules
The following modules ported to Backdrop are inter-related to the mailing system:

simplenews

simplenews_scheduler

mimemail

mandrill

mailsystem

smtp

They have been converted from Drupal to Backdrop but are still not working.  They need debugging into what was changed between the systems and how to fix it. I, biolithic the one who did the intial conversion, lack the heart or time in the spring of 2015 to debug them currently.

Do you have a need or desire for email newsletters?  You are welcome to submit pull requests to finish these modules.  It may not be a lot of work.  Thanks!

KNOWN ISSUES
---------------------

@todo

Backdrop CMS removed this table and we are re-engineering the module to work within the Backdrop way.

SPECIAL THANKS
--------------

Developed by the friendly geeks from ThinkShout, sponsored by Freddy and the rest of the amazing team from MailChimp. Read more about the 1.3 release on the ThinkShout blog.

REQUIREMENTS
------------

MailSystem

INSTALLATION
------------

Install this module using the official Backdrop CMS instructions at https://backdropcms.org/guide/modules

* You need to have a Mandrill API Key.

* If you are upgrading from one of many previous versions, You may find an extra
  Mail System class in the Mailsystem configuration called "Mandrill module
  class". It's harmless, but feel free to delete it.


COMING FROM DRUPAL?
-------------------

@todo

PERMISSIONS
------------

@todo


USAGE
-----

### Set Mandrill API Key
Start by loading up the Mandrill admin page at Configuration -> Web
Services (or admin/config/services/mandrill) and adding your API key from
http://mandrillapp.com. Then you'll see more configuration options.

### Email Options
* **From address:** The email address that emails should be sent from
* **From name:** The name to use for sending (optional)
* **Subaccount:** This selection box appears if you have configured subaccounts
on your Mandrill account, and can be used to select the outgoing subaccount to
use for Mandrill sending.
* **_Input format_:** An optional input format to apply to the message body
before sending emails

### Send Options
* **Track opens:** Toggles open tracking for messages
* **Track clicks:** Toggles click tracking for messages
* **Strip query string:** Strips the query string from URLs when aggregating
tracked URL data
* **Log sends that are not registered in mailsystem:** Useful for configuring
Mail System and getting more granular control over emails coming from various
modules. Enable this and set the system default in Mail System to Mandrill,
then trigger emails from various modules and functions on your site. You'll
see Mandrill writing log messages identifying the modules and keys that are
triggering each email. Now you can add these keys in Mail System and control
each email-generating module/key pair specifically. WARNING: If you leave this
enabled, you may slow your site significantly and clog your log files. Enable
only during configuration.

### Google Analytics
* **Domains:** One or more domains for which any matching URLs will
automatically have Google Analytics parameters appended to their query string.
Separate each domain with a comma.
* **Campaign:** The value to set for the utm_campaign tracking parameter. If
empty, the from address of the message will be used instead.

### Asynchronous Options
* **Queue Outgoing Messages** Drops all messages sent through Mandrill into a
queue without sending them. When Cron is triggered, a number of queued messages
are sent equal to the specified Batch Size.
* **Batch Size** The number of messages to send when Cron triggers. Must be
greater than 0.

### SEND TEST EMAIL

The Send Test Email function is pretty self-explanatory. The To: field will
accept multiple addresses formatted in any Backdrop mail system approved way.
By configuring the Mandrill Test module/key pair in Mail System, you can
use this tool to test outgoing mail for any installed mailer.

### Update Mail System settings
Mandrill Mail interface is enabled by using the
[Mail System module](http://drupal.org/project/mailsystem). Go to the
[Mail System configuration page](admin/config/system/mailsystem) to start
sending emails through Mandrill. Once you do this, you'll see a list of the
module keys that are using Mandrill listed near the top of the Mandrill
settings page.

Once you set the site-wide default (and any other module classes that may be
listed) to MandrillMailSystem, your site will immediately start using Mandrill
to deliver all outgoing email.

### Module/key pairs
The key is optional: not every module or email uses a key. That is why on the
mail system settings page, you may see some modules listed without keys. For
more details about this, see the help text on the mail system configuration
page.

# Sub-modules

## Templates

In order to use the mandrill_template module, start by creating some templates
in your Mandrill account. Once you do, you can add one or more Mandrill
Template Maps for that template, specifying where in the template to place
the email content and which module/key pair should be sent using the template.
If you want to send multiple module/key pairs through the same Template, you
can make Mandrill the default mail system and make that Template Map the
default template, or you can clone the Template Map for each module/key pair
and assign them individually.

You should also consider enabling the css-inline feature in your Mandrill
account under Settings -> Sending Options. For more info, see
"http://help.mandrill.com/entries/24460141-Does-Mandrill-inline-CSS-automatically-".

## Reports
The mandrill_reports sub-module provides reports on various metrics. It may
take a long time to load. This module is due for some attention.

### Dashboard
Displays charts that show volume and engagement, along with a tabular list of
URL interactions for the past 30 days.

### Account Summary
Shows account information, quotas, and all-time usage stats.

## Activity
The Mandrill Activity sub-modules allows users to view email activity for any
Backdrop entity with a valid email address. Configuration and usage details are in
sub-module's README file.

## Advanced Options
If you would like to use additional template (or other) Mandrill API
variables not implemented in this module, set them in hook_mail_alter under:
$params['mandrill']. Have a look at mandrill.mail.inc to learn more.
(Search for "mandrill parameters".)


If your Backdrop installation uses a .make file, see the example in mandrill.make.example.

Please Read:
If you are using the mandrill_templates sub-module to send html emails, you may see your emails displaying poorly on web-based email clients like gmail. It's important to enable Mandrill's CSS-inlining functionality to mitigate this issue.

LICENSE
-------

This project is GPL v2 software. See the LICENSE.txt file in this directory for complete text.

CREDITS
-----------

This module is based on the Mandrill module for Drupal, originally written and maintained by a large number of contributors, including:

 - levelos <https://www.drupal.org/u/levelos>
 - ruscoe <https://www.drupal.org/u/ruscoe>
 - gcb <https://www.drupal.org/u/gcb>

MAINTAINERS
-----------

- seeking

Ported to Backdrop by:

 - biolithic <https://github.com/biolithic>
