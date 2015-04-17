Setting up Mutt
---------------

Installation: `(apt-get|yum|brew) install mutt`

Mutt is a rich e-mail client with tons of features. Here are some
highlights:

 * [Macros](http://www.mutt.org/doc/manual/manual-3.html#ss3.6)
 * [Message and folder hooks](http://www.mutt.org/doc/manual/manual.html#toc4.4)
   to control mutt's behavior when sending, reading, and moving mail,
   and when changing folders
 * Good threading support
 * POP/IMAP support
 * [Bulk operation on many messages using tagging](http://www.mutt.org/doc/manual/manual-4.html#ss4.3)
 * [S/MIME support/PGP/GPG support](http://equiraptor.com/smime_mutt_how-to.html) (see also the [mutt guide page on this](http://dev.mutt.org/trac/wiki/MuttGuide#Advancedstuff))
 * Support for getting contacts from external sources (e.g. [LDAP](https://github.com/wking/mutt-ldap))

Noteworthy key bindings in this configuration (most are just defaults):
 * `?` Help (then `q` to leave help)
 * `j`/`k` Movement keys in message lists
 * `TAB` Select next unread message
 * `m` Begin composing a new message
 * `/` Search messages in the current folder using a [search pattern](http://www.mutt.org/doc/manual/manual-4.html#patterns)
 * `RET` View selected message, then
   * `i` Go back to message list
   * `RET` Scroll down one line
   * `BKSPC` Scroll up one line
   * `PGUP` / `PGDOWN` The usual
   * `r` Reply
 * `I` Go to Inbox and refresh
 * `c` Enter folder to view (`=`-`TAB` tab-completes server-side
   folders). If any folders have new mail, this will default to one of
   them.
 * `N` Mark the selected message as unread
 * `d` Mark the selected message for deletion
 * `r` Reply to the selected message
 * `$` Save pending changes to mailbox (e.g. delete marked messages) and
   check for new mail in the current folder
 * `s` Move (save) the selected message to another folder (e.g. `s`
   `=foo` `RET` saves to the `foo` folder)
 * `t` Tag a message for a future batch operation (`T` tags messages
   matching an expression)
 * `;` Specify an operation to perform on tagged messages (e.g. `;` `s`
   `=foo` `RET` will save all tagged messages to the `foo` folder)
 * `f` Forward the selected message

In message review mode, after you've finished composing in your editor:

 * `e` Edit the message again
 * `c` Set the CC field
 * `b` Set the BCC field
 * `a` Attach a file
 * `y` Send
 * `q` Abort composition and return to message list

Other things to try
-------------------

There is a [sidebar patch](http://zanshin.net/2015/01/19/teaching-a-homely-mutt-new-tricks/) for `mutt`.  If you want to install it easily on OS X with Homebrew, run this instead of `brew install mutt`:
```
brew install kevwil/patches/mutt --with-sidebar-patch
```

[Mutt can be used with GPG, PGP, and SMIME.](http://dev.mutt.org/trac/wiki/MuttGuide#Advancedstuff)

If someone is discourteous enough to send you an HTML-only e-mail and you must read it, [that can be done](http://unix.stackexchange.com/questions/42712/open-html-attachments-externally-in-mutt).

If you don't want to store your passwords in your `muttrc` (you don't,
right?) and you don't want to enter them once each time you start
`mutt`, you can make mutt get your IMAP and SMTP passwords
[from the OS X keychain](https://blog.aedifice.org/2009-10-18-use-mac-os-xs-keychain-for-password-retrieval-in-mutt.html), although YMMV.

Server-side mail filtering with [procmail](http://userpages.umbc.edu/~ian/procmail.html):
```
# In ~/.procmailrc on the mail server:
:0:
* ^From:.*somebody@somewhere.com
somebody

:0:
* ^From:.*somebody-else@somewhere.com
somebody-else

:0:
* ^(To|Cc):.*some-list@mailman.blah.com
some-mailing-list
```
