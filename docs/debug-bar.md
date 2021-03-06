# Debug Bar
The debug bar shows non-fatal errors, dumps, and provides access to all the custom panels/tools for ProcessWire development. You can set the default panels for both frontend and backend versions of the bar and also add / remove them on-the-fly via the [Panel Selector](#panel-selector).

![Tracy Debug Bar Kitchen Sink](img/debug-bar-kitchen-sink.png 'Tracy Debug Bar')

## ![Admin Tools](icons/admin-tools.svg ':no-zoom')Admin Tools
 The available actions are context sensitive so you only get tools that are relevant to where you are in the admin (or frontend in some cases).

Current tools are:

**Delete all children**

This lets you delete all children of the current page without deleting the page itself which can be very helpful when you're testing API creation of page and you have forgotten to enable Tracy's Page Recorder panel.

![Admin Tools Pages](img/admin-tools-pages.png)

**Delete field**

If you're on the edit interface for a field, this action will let you delete a field even if it is already added to templates, so you don't have to deal with the "This field may not be deleted because it is in use by one or more templates." notice you get when trying to delete the field.

**Change field type**

Again, if you're on the edit interface for a field, this lets you change the field to any installed field type. This ignores the compatible field type check that you are normally subject to. This is probably not good to use if you already have page data in this field, but it's really handy when you have already set up a field and added it to templates but decide you want to change its type to a non-compatible type.

![Admin Tools Fields](img/admin-tools-fields.png)

**Delete template**

Like the delete field, this bypasses the "This template may not be deleted" because there are pages already using it. This takes care of deleting any pages using the template and then deletes the template, all with one click.

![Admin Tools Templates](img/admin-tools-templates.png)

**Uninstall module**

This will take care of deleting any associated fields (for Fieldtype modules) and modules that require the one you are trying to uninstall so that you can uninstall the module with one click.

![Admin Tools Templates](img/admin-tools-modules.png)

Hopefully it goes without saying that these can be extremely destructive and bypass core protections against data loss so use with extreme caution. Each action has a confirmation dialog that you must confirm to reduce any accidental clicks and the entire panel is restricted to superusers only, but you must still use with extreme caution.

***

## ![Adminer](icons/adminer.svg ':no-zoom')Adminer
Adminer is a MySQL database management tool similar to PHPMyAdmin.

You can access it via a panel from the debug bar, or from your PW admin Setup menu.

You will be automatically connected to the database table for the current ProcessWire installation using the credentials in your /site/config.php file.

There are several direct links from within Tracy to open Adminer to specific tables / rows. Look for these links in the Request Info panel in the following sections:

* Page Info
* Module Settings
* Template Settings
* Template Info
* Field Settings

![Adminer Panel](img/adminer.png)

***

## ![API Exporer](icons/api-explorer.svg ':no-zoom')API Explorer
Generates a searchable list of all methods and properties in your ProcessWire install.

Results are cached for speed, but will be updated whenever you update your ProcessWire version or install a new module.

* Class::method links to ProcessWire API docs, either on processwire.com or locally if you have the API Explorer module installed
* Line number links to the method in your code editor, or via the File Editor Panel or the ProcessFileEdit module
* Method / property summary which can optionally toggle the full docblock

![API Explorer Panel](img/api-explorer.png)

***

## ![Captain Hook](icons/captain-hook.svg ':no-zoom')Captain Hook
Generates a list of hookable methods in your ProcessWire install, including site modules.

Results are cached for speed, but will be updated whenever you update your ProcessWire version or install a new module.

* Method/ Property links to ProcessWire API docs, either on processwire.com or locally if you have the API Explorer module installed
* Line number links to the method in your code editor, or via the File Editor Panel or the ProcessFileEdit module
* Method summary which can optionally toggle the full docblock

![Captain Hook Panel](img/captain-hook.png)

***

## ![Console](icons/console.svg ':no-zoom')Console

* Code highlighting and syntax checking
* Access to all PW variables: $pages, $page, $user, $input, $fields, $templates, $modules, etc
* Autocomplete for all PW methods and properties.
* Access to $field, $template, $module when viewing the settings for a field, template, or module in the ProcessWire admin
* Access to all template defined variables and functions
* Works with `bd()`, `d()`, `fl()`, and `l()` calls, and `echo`. `d()` is recommended in most scenarios because output will appear in the results panel below the code
* Also works with `bdb()`, `bdl()`, and `db()` big/live variants
* Supports PHP, HTML, or mixed HTML/PHP syntax
* All output is generated via ajax, and so no page load required
* Only available to superusers
* Caches code so it stored between page reloads, navigation to other pages, and even browser restarts
* Use CTRL + Enter or CMD + Enter or the "Run Code" button to run the code
* In-code search & replace with CMD/CTRL + F
* History stack
	* ALT + PageUp | back
	* ALT + PageDown | forward
* Fullscreen editing mode with quick toggles between: all code, all results, and mixes of both.
	* CTRL + SHFT + Enter | toggle fullscreen mode
	* CTRL + SHFT + ↑ | collapse code pane
	* CTRL + SHFT + ↓ | collapse results pane
	* CTRL + SHFT + ← | restore split to last saved position
	* CTRL + SHFT + → | split to show all the lines of code
	* CTRL + SHFT + PageUp	| one less row in code pane (saves position)
	* CTRL + SHFT + PageDown | one more row in code pane (saves position)
	* SHFT + Enter | Expand to fit all code and add new line (saves position)
	* SHFT + Backspace | Contract to fit all code and remove line (saves position)
* Snippets storage for regularly used code
* Options to run code instead at `init`, `ready`, or `finished` - useful for testing hooks. To use this, click Run, select `init`, `ready`, or `finished` and then execute whatever action in ProcessWire that is needed to trigger the hook. An orange icon will indicate this feature is active. You can switch to `off` manually when you are done. It will also expire automatically after 5 minutes.


Remember that this allows you to run any PHP code, so be careful!

![Console Panel](img/console-1.png)

***

## ![Custom PHP](icons/custom-php.svg ':no-zoom')Custom PHP
This panel lets you output anything you want. Primarily I see this being used for creating links to things like Google PageSpeed, but use your imagination.

```php
return '<a href="https://developers.google.com/speed/pagespeed/insights/?url='.$page->httpUrl.'">Google PageSpeed</a>';
```

![Custom PHP Panel](img/custom-php.png)

***

## ![Debug Mode](icons/debug-mode.svg ':no-zoom')Debug Mode
Provides access to most of the information that is available in the back-end "Debug Mode Tools" section of your PW admin. This panel makes it available on the front-end and even when Debug Mode is off. Note that with Debug Mode Off, you won't have access to the "Database Queries", "Timers", and "Autload" sections. This is a ProcessWire core restriction.

Other information from the back-end "Debug Mode Tools" (POST, GET, REQUEST, COOKIE, SESSION) have been moved to the [Request Info Panel](#request-info).

The icon color on the debug bar is red when debug mode is on and green when it is off. This may seem opposite, but the idea is that when the icon is green, it is OK for production mode, whereas red indicates something that you need to be alerted to. This is particularly useful if you have the "Superuser Force Development Mode" option enabled because you will see the debug bar even in Production mode.

![Debug Mode Panel](img/debug-mode.png)

***

## ![Diagnostics](icons/diagnostics.svg ':no-zoom')Diagnostics
### Filesystem Folders
Overview of the filesystem access permissions for all the key folders and files in your PW install. It also provides status and notes about these. These should not be taken as definitive (especially if you are on a Windows system), but rather as a guide and reminder to check these. The debug bar icon for this panel is colored to match the most serious status level - OK, Warning, or Failure.

![Diagnostics Filesystem Folders](img/diagnostics-filesystem-folders.png)

### Filesystem Files
Generally not recommended to enable this (in the module config settings), because it is very slow to generate, but if needed, it shows the permissions for all files within the site.

### MySQL Info
Some basic details about your MySQL server and client setup.

![Diagnostics MySQL Info](img/diagnostics-mysql-info.png)

***

## ![Dumps](icons/dumps.svg ':no-zoom')Dumps
This panel is only displayed when you have called the barDump() method and contains the contents of that dump.

Note the second optional parameter used to name the outputs in the Dumps panel.

```php
bd($page->body, 'Body');
bd(array('a' => array(1,2,3), 'b' => array(4,5,6)), 'Test Array');
```

![Dumps Panel Example](img/dumps-panel-1.png)

> For more details, see the [barDump()](debug-methods.md#bardump) and other associate debug methods

***

## ![Dumps Recorder](icons/dumps-recorder.svg ':no-zoom')Dumps Recorder
If this panel is enabled, any calls to bd() will be sent to this panel instead of the main dumps panel. This is useful in several situations where you want to compare dumps from various page requests. Dumps will be preserved until the session is closed, or until you click the "Clear Dumps" button. It can also be useful in some situations where dumps are not being captured with the regular dumps panel which can sometimes happen with modules, complex redirects, or other scenarios that are hard to pin down.

***

## ![Errors](icons/errors.svg ':no-zoom')Errors
The errors panel is only displayed when there are non-fatal errors and you are not in Strict Mode. All PHP notices and warnings will be displayed in this panel.

![Errors panel](img/errors.png)

***

## ![Event Interceptor](icons/event-interceptor.svg ':no-zoom')Event Interceptor

> This panel lets you define any Hook that you want to intercept.

```
@Hook
@options: Before | After
@default: Before

@Return
@options: Default | False
@default: Default
```

Returns the contents of $event->object and $event->arguments in the panel.

**CAUTION  with Return False**

`Return: False` prevents the chosen hook from being executed.
For example, setting the hook to `Pages::save` and then deleting a page can result in some pages ending up having the trashed status, but their parent still listed as the home page. This is a situation that requires some careful database manipulation to fix.

* **Green:** no hook set
* **Orange:** hook set, but nothing intercepted
* **Red:** hook set and event intercepted

![Event Interceptor](img/event-interceptor.png)

***

## ![File Editor](icons/file-editor.svg ':no-zoom')File Editor

* Supports editing all files in your PW install (you can define the root as /, /site, or /site/templates
* Can be used as the handler for opening editor links from the debug bar (errors, log files, Captain Hook, ToDo, Template editor, etc), rather than your code editor
* Can be enabled as the link handler for live sites only, or local as well if you prefer
* Has "Test" functionality for all files so if you make a change, it will only appear for you and not other users
* Red icon: Test code is being rendered
* Makes a backup of the old version each time you save a change and provides a "Restore Backup" button to instantly revert
* Supports in-code search & replace with CMD + F
* Syntax highlighting/linting for PHP, CSS, and JS
* This replaces the Template Editor panel, so that one has been removed
* Handles fatal errors gracefully - this is the biggest feature in my opinion. The problem with most online file editors is that if you accidentally make a code change that results in a fatal error, it can be impossible to fix and resave because the system is not functional. This editor gets around this problem by using Tracy's custom error handling which allows debug bar panels to continue to work, so you can manually fix the problem, or click the "Restore Backup" button. Of course if you used the "Test" option, you don't even need to worry, because you are the only one to see the version with the error anyway.

**Action buttons (some only available when relevant):**
* **Test**: reloads the page using the code in the editor - no changes are made to the template file or the code served to all other users of the site.
* **Save**: saves the editor code to the template file, making this a live and permanent change.
* **Reset**: re-loads the page (and the code in the editor) with the code from the saved file. This is no different from loading the page again, but different from clicking the "reload" button in your browser which will actually send the test code again.
* **Restore**: returns the code for the file to the last saved version (restored from automatic backup of the file)

**Possible use scenarios**
* Use this panel similarly to your dev console for tweaking CSS/HTML - it still requires a page reload, but there are likely less clicks than your normal workflow.
* Tweak a live site if you're away from your computer and need a quick way to fix something, but want the ability to test first without breaking something temporarily due to a simple syntax error mistake or more serious code mistakes.
* Add debug statements: `bd()`, `d()`, `fl()` etc to your file code without editing touching the actual files.

![File Editor panel](img/file-editor.png)

***

## ![Git Info](icons/git-info.svg ':no-zoom')Git Info

Displays the Git branch, latest commit message, etc for your site (assuming you have it under Git version control).

![Git Info panel](img/git-info.png)

***

## ![Mail Interceptor](icons/mail-interceptor.svg ':no-zoom')Mail Interceptor
Intercepts all outgoing emails sent using `wireMail()` and displays them in the panel. Ideal for form submission testing. This panel is activated when enabled, so it's best to enable it from the Panel Selector using the sticky option when needed. If you'd also like to receive the email at a test address (but not the original recipients), you can enter an address and click "Set Email".

![Mail Interceptor Panel](img/mail-interceptor.png)

***

## ![Methods Info](icons/methods-info.svg ':no-zoom')Methods Info
Lists available logging methods you can call in your PHP code.<br />Links to Tracy Debugger docs (this site) and [Tracy Nette docs](https://tracy.nette.org/)

![Methods Info panel](img/methods-info.png)

***

## ![Module Disabler](icons/module-disabler.svg ':no-zoom')Module Disabler
This panel makes use of the ProcessWire core "disabled" flag for disabling autoload modules for testing / debugging purposes. It can potentially result in a fatal error on your site (this is a ProcessWire core issue, rather than specific to this panel). Because of this, it is only available when ProcessWire's advanced and debug modes are enabled.

If you do end up with a fatal error after disabling a module, this panel provides a script for automatically restoring the modules database table. Whenever you disable any modules, a backup of the "modules" database table is automatically saved.

To restore you have two choices:

Copy "/site/assets/cache/TracyDebugger/restoremodules.php" to the root of your site and load it in your browser

OR

Execute "/site/assets/cache/TracyDebugger/modulesBackup.sql" manually (via PHPMyAdmin, the command line, etc)

![Module Disabler panel](img/module-disabler.png)

***

## ![Output Mode](icons/output-mode.svg ':no-zoom')Output Mode
Indicates which mode Tracy is in - DEVELOPMENT or PRODUCTION - this is determined at runtime so if you have configured it to "Detect" mode, you can easily see which mode it has automatically switched to. This is useful if you have the "Superuser Force Development Mode" option enabled because you will see the debug bar even in Production mode.

![Output Mode panel](img/output-mode.png)

* Note that no matter what mode you are in, guest users will always be in PRODUCTION mode which means no debug bar and no detailed error reporting.

***

## ![Page Files](icons/page-files.svg ':no-zoom')Page Files
Shows (and links) to all the files that belong to the current page (including those in repeater items and even nested repeaters).

It warns (orange) about files that are orphans - these are files that are in the /site/assets/files/xxxx folder for the page, but which don't belong to any of the file/image fields on the page.

It alerts (red) you of files which are missing from the /site/assets/files/xxxx folder but are referenced by one of the file/image fields on the page. Obviously missing files are more important and critical than orphans, so they are red as an alert, rather than a warning.

The icon on the debug bar tells you how many files there are and how many are orphans and how many are missing.

There are "Delete Orphans" and "Delete Missing" buttons for easy cleanup.

Note that the results are divided up into page IDs, starting with the ID of the page you are currently viewing/editing and followed by pages for any repeater field items. It also shows the name of the field that each file belongs to (except the orange orphans because obviously these don't belong to a field).

![Page Files panel](img/page-files.png)

***

## ![Page Recorder](icons/page-recorder.svg ':no-zoom')Page Recorder
This panel records the ID of all pages added whenever it is enabled (so this is one you'll want off by default and just enabled via "Sticky" when you need it).

This is perfect for all sorts of testing, whether you need to create a LOT of pages for performance testing or you are testing a form which is automatically creating pages. Once you are done with the testing session, simply click the "Trash Recorded Pages" button and they will all be moved to the Trash.

If you decide you want to keep the pages, you can click "Clear Recorded Pages List" instead.

![Page Recorder panel](img/page-recorder.png)

***

## ![Panel Selector](icons/panel-selector.svg ':no-zoom')Panel Selector
Allows you to set up a default set of panels in the module config settings and then easily enable / disable other panels from the debugger bar.

Your page loading speed will be better if you limit the default panels to those you use all the time and load others as needed via this selector.

There are three options: Once, Sticky, and Reset
* **Once** will only make the selection change for one page load
* **Sticky** will keep the changes for the browser session
* **Reset**  will return to the default set defined in the module config settings

There are indicators if:

**\*** the panel is set in the default list in the module config settings

![Once icon](img/once-icon.svg) the state of the panel is different for the current view, ie you have made a "Once" change

![Panel Selector panel](img/panel-selector.png)

***

## ![Performance](icons/performance.svg ':no-zoom')Performance
Performance Panel is a third party extension for Tracy developed by Martin Jirásek. It adds support for inserting named breakpoints in your code and reports execution time and various memory usages stats between the various breakpoints. This is where calls to addBreakpoint() are rendered.

```
bp('A');
for($i = 0; $i < 10000000; $i++) {
     $a += $i;
}
bp('B');
sleep(2);
bp('C', 'B');
for($i = 0; $i < 10000000; $i++) {
     $a += $i;
}
bp('D');
```

![Performance panel](img/performance.png)

***

## ![PHP Info](icons/php-info.svg ':no-zoom')PHP Info
Provides all the output from PHP's `phpinfo()`. Probable best to leave disabled unless you need to check something.

CTRL/CMD + F works well to find relevant entries within this panel (and all panels actually), although this seems to be browser specific. It works in Chrome and Safari, but not Firefox.

![PHP Info panel](img/php-info.png)

***

## ![ProcessWire Info](icons/processwire-info.svg ':no-zoom')Processwire Info
Provides a wide variety of links, information and search features for all things ProcessWire.

![ProcessWire Info panel](img/processwire-info.png)

***

## ![ProcessWire Logs](icons/processwire-logs.svg ':no-zoom')ProcessWire Logs
Displays the most recent entries across all ProcessWire log files with links to view the log in the PW logs viewer, as well as direct links to view each entry in your code editor. By default it shows the last 10, but this can be changed in the config settings. A red icon indicates the last page load contained an errors or exceptions log entry. An orange icon is for all other log types.

![ProcessWire Logs panel](img/processwire-logs.png)

***

## ![ProcessWire Version](icons/processwire-version.svg ':no-zoom')ProcessWire Version
Lets you instantly switch your PW version. This is probably most useful for module developers, but can also be helpful for other users to help debug PW core or module problems. It's probably obvious, but the switcher is not recommended for live sites, so don't blame me if a version change breaks your site (especially between the 2.x and 3.x branch)!

The available versions come from Ryan's ProcessWire Upgrades module - so any version that you installed via it will be available.

When you click "Change", it swaps the names of: wire/, .htaccess, and index.php - much easier than manually renaming.

The icon is green when you are using the latest version that is available on your system, and orange for any other version.

![ProcessWire Version panel](img/processwire-version.png)

***

## ![Request Info](icons/request-info.svg ':no-zoom')Request Info

Provides very detailed infomation and links related to the current page. It contains several expandable sections listed below.

### Page Info
Links to view (from page name) and edit the page (from page ID), template, parent and sibling pages, etc. Also includes page status, creation, modified, and published username and datetime.

![Request Info panel - Page Info](img/request-info-page-info.png)

### Language Info
Details about the languages of the current page (title, name, and status). Also includes a link to edit each language.

![Request Info panel - Language Info](img/request-info-language-info.png)

### Template Info
Details about the template of the current page and its settings, includes a link to open the template for editing in the PW admin, and the template file for editing in your code editor.

![Request Info panel - Template Info](img/request-info-template-info.png)

### Fields List & Values
Complete list of all available fields for the page and their values - all arrays/objects are presented as expandable trees. For image fields it provides additional information, such as filesize and dimension attributes. There is also Settings column for each field - truncated in this screenshot so that everything else is legible.

![Request Info panel - Field List & Values](img/request-info-field-list-values.png)

### Server Request

![Request Info panel - Server Request](img/request-info-server-request.png)

### Input GET

![Request Info panel - Input GET](img/request-info-input-get.png)

### Input POST

![Request Info panel - Input POST](img/request-info-input-post.png)

### Input COOKIE

![Request Info panel - Input COOKIE](img/request-info-input-cookie.png)

### SESSION

![Request Info panel - SESSION](img/request-info-session.png)

### Template Settings

This section is only available when viewing the settings page for a template in the admin

![Request Info panel - Template Settings](img/request-info-template-settings.png)

### Field Settings

This section is only available when viewing the settings page for a field in the admin

![Request Info panel - Field Settings](img/request-info-field-settings.png)

### Module Settings

This section is only available when viewing the settings page for a module in the admin

![Request Info panel - Module Settings](img/request-info-module-settings.png)


***

## ![Request Logger](icons/request-logger.svg ':no-zoom')Request Logger

This panel logs incoming requests to your pages. In particular, this can be used to log webhook requests and you can use logged requests in your code while developing so you don't need to continually trigger them. Very handy if you waiting on a response from a payment gateway :)

1. In the PW admin, edit the page you want to log incoming requests for.
2. Open the Request Logger panel.
3. Click the "Enable logging on this page" button.

![Request Logger enable dialog](img/request-logger-enable-dialog.png)

4. Send a request to that page. This may be something like a confirmation of payment webhook call from Paypal etc.

5. Reload the edit page in the PW admin to see the logged request. The reason we say to edit the page, rather than visit it on the frontend is because visiting the page would result in a logged request.

![Request Logger results](img/request-logger-results.png)

Note that you can easily test incoming requests using the Postman app (https://www.getpostman.com/). You can choose POST or GET and under "Body" you'll want to specify Raw / JSON

![Request Logger results](img/request-logger-postman.png)

You'll notice the json supplied in the Postman Body is what shows up in the Request Logger panel under "input" and "inputParsed".

This is all well and good, but here's where the magic really comes in 🙂 There is a new getRequestData() method added to $page so you can get the logged data in your code. You can get logged requests by:

ID (shown in the title of the logged entry in the Request Logger panel)
ALL requests (an array of all logged requests for the page)
The last logged request by passing "true"
The current live request
This allows you to have access to the data sent by the webhook without constantly having to trigger it each time - ie no need to continually make test payments over and over as you refine and debug the your scripts that consume/parse this data! You can even make use of $page->getRequestData() in your final live code if you want - this does not rely on Tracy being enabled - it just has to be installed. So you could potentially execute one request and then use the "true" option while testing, and then when you're ready to go live, you can remove the "true" so it returns the live request.

There is a config setting to determine whether this method returns an array or an object.

![Request Logger results](img/request-logger-api-calls.png)

You can also use this panel on non-ProcessWire pages, so if you use a php script like payment_confirmation.php in the root of your site, so long as it bootstraps PW (include ./index.php), it will let you log and retrieve request data. The only catch is that you need to trigger the logging manually by adding `$page->logRequests();` to the script file.

In the config settings you can define which types of request methods are logged: GET, POST, PUT, DELETE, PATCH. By default, all are checked, but I think in most cases unchecking GET is probably helpful as it will prevent page views from being logged.


***

## ![Snippet Runner](icons/snippet-runner.svg ':no-zoom')Snippet Runner
This is similar to the [Console Panel](#console), but instead lets you run snippets stored on the server's filesystem which allows for easier version control, and also for editing snippets in your code editor. It has access to all the same ProcessWire system variables that the Console panel has, so please see it's documentation for details.

Snippets can be stored in either of these. Visit the config settings to set which you prefer. You can also make use of subfolders to categorize your snippets.
* /site/templates/TracyDebugger/snippets/
* /site/assets/TracyDebugger/snippets/

![Snippet Runner panel](img/snippet-runner.png)

***

## ![System Info](icons/system-info.svg ':no-zoom')System Info
Provides a table of basic stats about the current page and your system.

![System Info panel](img/system-info.png)

***

## ![Template Path](icons/template-path.svg ':no-zoom')Template Path
The template path panel allows you to temporarily choose an alternate template file for rendering the current page. It provides a list of files in the site/templates folder that match the name of the default template file, but with a "-suffix" extension. You can have several different versions and quickly test each one. You can make the change last for the browser session (sticky), or just for one reload (once). You can reset to the default template file for the current page, or all changes you may have made to other pages/template files on the site.

Additionally, it automatically swaps out files included via `$config->prependTemplateFile` and `$config->appendTemplateFile` to use the same suffix at the replaced template, eg `_init-dev.php` or `_main-dev.php`

Not only is this useful for debugging (especially on a live production server), but it could also be used for sharing different versions of a page among trusted users.

* **Red:** The current page is using a different template file.
* **Orange:** The current page is using it's default template file, but there are other pages on the site that are using a different template file (obviously via the Sticky option). Use "Reset All" to clear this when you're done testing.
* **Green:** All pages on the site are using their default template files.

![Template Path panel](img/template-path.png)

### User Dev Template Option
This is not reliant on the Template Path Panel, but its functionality is similar and its status is integrated into the panel, so it is presented here.

It makes it really easy to show authorized users development versions of template files. To make this work, all you need to do is enable the checkbox. Then setup a `tracy-template-****` permission and assign that to the required users.

Obviously this is not the best approach for major changes (you should set up a dev subdomain for that), but I think it could be quite handy for certain site changes.

Additionally, it automatically swaps out files included via `$config->prependTemplateFile` and `$config->appendTemplateFile` to use the same suffix at the replaced template, eg `_init-dev.php` or `_main-dev.php`

![Template Path panel](img/template-path-2.png)

In this screenshot, you can see the reminder detailing why the icon is orange. Currently we are not viewing a page with an alternate template, but it is letting us know that:

* the "User Dev Template" option is enabled in module settings
* the `tracy-basic-page-dev` (or `tracy-all-dev`) permission exists
* the permission has been assigned to at least one user
* there are template files with a "-dev" suffix

So if this is expected then great, but if not, then you can prevent the alternate templates from being rendered by doing one or more of the following:

* disabling the "User Dev Template" option
* removing the template-dev permission from the system
* remove the template-dev permission from all roles
* delete alternate template files with the "-dev" suffix

If you are on a page that is using an alternate template due to user permissions, then you will see the PW permission cog icon:

![Template Resources panel 3](img/template-path-3.png)

***

## ![Template Resources](icons/template-resources.svg ':no-zoom')Template Resources
Displays the names, types, and values of all variables defined in the template file (and any other included files) for the current page. It also shows any defined constants and functions (linked to open in your code editor), as well as a list of included files (also linked to open in your code editor).

![Template Resources panel 1](img/template-resources-1.png)

![Template Resources panel 2](img/template-resources-2.png)

***

## ![TODO](icons/todo.svg ':no-zoom')Todo
The ToDo Panel report the following comment types: 'todo', 'fixme', 'pending', 'xxx', 'hack', 'bug'. See the config settings for determining which folders and files will be scanned.

If you have your editor configured, the comment text link opens the file to the line of the comment.

The icon reports the number of items in the template file for the current file / the total number of items across all files.

* **Red:** there are items for the current page's template file.
* **Orange:** there are items in other files, but none in the current page's template file.
* **Green:** no items in any files under /site/templates/

![TODO panel](img/todo.png)

***

## ![Tracy Logs](icons/tracy-logs.svg ':no-zoom')Tracy Logs
Displays the most recent entries from the Tracy log files. These log files can be written to automatically when Tracy is in Production mode, or manually using `TD::log()` or `l()` calls. Includes direct links to view each entry in your code editor. By default it shows the last 10, but this can be changed in the config settings. A red icon indicates the last page load contained an error, exception, or critical log entry. An orange icon is for all other log types.

![Tracy Logs panel](img/tracy-logs.png)

***

## ![Tracy Toggler](icons/tracy-toggler.svg ':no-zoom')Tracy Toggler
Not really a panel, but this button on the debug bar lets you toggle Tracy on / off without needing to visit the module config settings. If you don't want another button always taking up room, you can also use the "Disable Tracy" button on the Panel Selector. Another alternative is the Hide/Show toggle icon at the far right of the debug bar, although this one doesn't actually turn Tracy off, but it gets the debug out of the way.

***

## ![User Switcher](icons/user-switcher.svg ':no-zoom')User Switcher
Allows you to instantly switch to any user in the system without knowing their password. After switching, you will still have full access to the Tracy debug bar, which can be very useful for debugging issues with other users and even guest (not logged in) visitors.

* You need to be a superuser to have access to the panel until a session is started, so even when Development mode is enabled, other users still won't be able to use it.
* It only works for the duration of user switcher session (max 60 minutes) and only a superuser can start a session.
* Starting the session makes use of PW's CSRF protection.
* The switcher session has a unique ID and expiry time which is stored in the database and must match the ID in the user's session.
* Once the session has expired, it is no longer possible to switch users. You can manually end the session, or if you forget it will expire automatically based on the session length you set.

As usual, icon colors are meaningful, telling you what type of user is currently logged in:
* Green: superuser
* Orange: non-superuser
* Red: guest / logged out

![User Switcher panel](img/user-switcher.png)

***

## ![Users](icons/users.svg ':no-zoom')Users
Lists all the users/roles with access to the Tracy Debugger bar. A green debug bar icon indicates that only superusers can access the debug bar. An orange icon indicates that others have the tracy-debugger permission and may be able to see the debug bar. Another good reason to have the "Superuser Force Development Mode" option enabled because you will see this warning even in Production mode.

![Users panel](img/users.png)

***

## ![Validator](icons/validator.svg ':no-zoom')Validator
Validates the HTML of the page using the validator.nu service. This works with local development sites as well as live sites.

![Validator panel](img/validator.png)

***
