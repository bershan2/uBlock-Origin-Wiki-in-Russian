- Back to [Wiki home](https://github.com/gorhill/uBlock/wiki)
- Back to [Dashboard](https://github.com/gorhill/uBlock/wiki/Dashboard)

***

The _Whitelist_ pane lists all the _whitelist directives_. The purpose of a whitelist directive is to tell on which page uBlock Origin ("uBO") should disable itself completely. When uBO is disabled on a page, there will be no filtering applied to that page.

When uBO is disabled for a site, its toolbar icon will be grayed, and the large blue "power" button in the popup panel is dimmed.

When you visit a web page, uBO will try to match the URL of the page in the address bar against the existing whitelist directives. When there is a match, uBO will be disabled for that page.

The easiest way to create a whitelist directive is by toggling the large "power" button in uBO's popup panel -- this will cause a site-wide whitelist directive for the current site to be automatically created and added to the _Whitelist_ pane.

The _Whitelist_ pane allows you to review or edit the exisiting whitelist directives, or to manually add new ones.

### Important: read carefully

There are predefined whitelist directives when you first install uBO:

    about-scheme
    behind-the-scene
    chrome-extension-scheme
    chrome-scheme
    moz-extension-scheme
    opera-scheme
    vivaldi-scheme

You should not remove these predefined whitelist directives, unless you know _exactly_ the consequences of doing so.

Removing the predefined whitelist directives without understanding the consequences could cause your browser to malfunction. **This is especially true for the `behind-the-scene` whitelist directive.**

If despite this warning you still want to remove one or more of the predefined whitelist directives, I strongly suggest to comment out an entry rather than outright delete it. To comment out an entry, just prefix it with `# `. This way you do not have to remember which predefined whitelist directive you removed, it will be just a matter of removing the `# ` prefix if ever you want to restore an entry.

### Whitelist directive syntax

Further details about the supported syntax for whitelist directives can be found at ["How to whitelist a web site"](https://github.com/gorhill/uBlock/wiki/How-to-whitelist-a-web-site).