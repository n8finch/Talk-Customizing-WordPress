# Customizing Your WordPress Site:
### The What, Where, How, and Why of Making Your Site Yours
### Understanding Where, Why, and How to Make Your Site Unique


WP for ~6 years, ~5 years full-time
The Digital Ring, toptal, Codeable, and other clients for fun and profit
Currently residing in Madison
Texas >> Kansas >> Spain ( a little time in Morocco) >> France >> Illinois >> S. Korea >> and now Madison
“I’d be a professional student if I could…”
Married w/ 1.5 year old daughter


## 0. The Questions

- Where do I make changes to my theme (CSS or PHP)?
- Should I just put everything in `functions.php`?
- How can I add a JS library to my site?
- How can I update my site safely and not worry about losing customizations?
- How should I be thinking about customizations?
- What is the general structure of WordPress?


This is meant for all different skill levels. There are solutions for beginners and intermediate developers here.
This is an overview with some specific examples of how to implement this framework of customization.
These decisions will ultimately be left up to you, or whoever is managing the development of your site


## 1. The Initial Problem

**Demo**

- You've made changes directly to a free/premium theme that you've downloaded
- You see that there's an update
- You update, all your changes get wiped!
- ARGH!!!! Small sick vomit felling
- And even worse, if the update also caused a DB update, change and you try and roll back the code, your databse may have also changed, and you can't get all that back unless you've also get a DB backup.
- In general, custom CSS, PHP, and JS shouldn't be store in the Databse (unless you have a really good reason for doing so). It's ***not*** data, and could lead to uninteded consequences.

**Aside**

**Axioms**


- Themes handle Form, Plugins handle Function
- Code should go in Codebase
- Data should go in Databse
- Media Files should be processed through the Media Library (and reside in the `wp-content/uploads` directory)
- ABC: Always Be Closing... Wait... Always Be CheckingYouHaveABackupOfYourCodeAndDatabaseBeforeYouRunAnyUpdatesOrChangeAnything

0. Manually backup prior
1. Get a good host!!!
2. Seriously, get a good host!!!!!!!!!!!
3. Manually backup prior to updating
4. Make sure you've got a good backup plugin running (BackupBuddy, Duplicator, whatever, I don't know because I use good hosting)



## 2. Understanding the Structure and Intent

***"Form and Function "***

The Theme handles Form:

- layout/structure (templates and hierarchy)
- styles CSS
- Theme supports (Freatured Images, Content Types)
- Post Types (maybe better to put in a plugin, but typically put into a theme)
- Think things that are specific to the current display of the site that you would want/need to transfer if you did a "site redesign"

Plugins handle Function:

- Basic: Add widgets, custom fields, post meta boxes, etc.
- Admin Tasks: Backups, Cron Jobs, Analytics and tracking
- CRM/Marketing: MailChimp signups, Monster Insights, whatever
- Ecommerce and Memberships: WooCommerce, Easy Digital Downloads, Restrict Content Pro, Paid Memberships pro....
- And whatever else you need.


Where do these things live?

- `wp-content/themes`
- `wp-content/plugins`
- `wp-content/uploads`
- `wp-content/mu-plugins`
- `wp-content/*`

**Aside**

- Your customizations should always be made in the `wp-content` folder. This does not cet updated on WP Core updates (I'm pretty sure about this).
- Unless you've got a good reason to put things somwhere else, do not put things in the root folder (use the wp-content "namespace"). Think of your permalink structure.
- And as always:

> Don't Hack Core!


## Our Example:

> A styled "After Post" box.

Title: What to next

- Adds functionality
- Adds style

Several ways to deal with this:

- override and hard code the single.php template file in child theme
- ~~~use an action hook in your theme's function.php file~~~
- create a plugin and hook into the theme's action hook


##2.5 Befor Customizing

1. Make sure you have a code and databse backup
2. Work on a Local Environment or Staging Enviornment (Local or VVV)
3. Maybe even look at the Pantheon Work Flow



## 3. Making Style or Theme-Based Changes

0. Make a Child Theme (cf. WP Codex on Child Themes or Beth's Talk)
1. Are the changes I want to make Form or Function?
2. If they're Form, I should add them to my theme
3. Use your Child Theme's style.css file for changes
4. Overriding a template file (Template Hierarchy)


*Should I use the Custom CSS in the customizer?*
- You can if you don't want to make a child theme
*Should I use a Custom CSS/JS plugin?*
- You can if you don't want to make a child theme or custom plugin
*Should I use a Custom PHP plugin?*
- You can, but you probably shouldn't
ALL of the above break the AXIOMS that Code should be in the Codebase and Data should be in the Database.


**DEMO**

0. Make child theme
1. copy `single.php` to child
2. find part after post
3. copy in template
4. style in style.css
5. copy in styles



## 4. Making Functional Changes

Maybe we want to keep this functionality after a site redesign. If you've made this and 50+ other changes in your child theme, it's not hard, but it could be cumbersome to migrate these to a new theme.

**DEMO**

1. Create a single file plugin (reference Hello Dolly)
2. Activate it in wp-admin
3. Copy over the template, leave the styles
3. Use action hook (or add your own!!)

**Bonus Points**
Create a multifile plugin with inc. PHP, JS and CSS
Review wp_enque_script/style

**Notes on custom JS stuff**

- don't add your own version of jQuery!!! WordPress does this already. Make it a dependecy in your array.
