---
layout: post
title:  "Workflow, Neomutt, Lei, Notmuch, Getmail, Gmail"
date:   2025-09-21 20:00:00 +0530
categories: linux workflow neomutt notmuch getmail lei gmail
---

This is a mail setup for terminal UI users. This uses combination of tools,  
`neomutt` for viewing mails,  
`notmuch` for filtering mails,  
`getmail` for fetching mails from gmail,  
`lei` for fetching mails from lore.kernel.org.  
For convinience, lets keep all the config files in ~/.lkml folder  
```mkdir -p ~/.lkml/mail```

# lei:  
Installation in Debian/Ubuntu:  
```sudo apt install -y lei```  

lei, helps with fetching mail from lore.kernel.org without subscribing to any
mailing list.  
lei, also has query features which helps in filtering the mails.  
For example to fetch mails from linux-block,linux-fsdevel mailing
list from last one day,  
below command should be useful.

```$ lei q -I https://lore.kernel.org/all -o ~/.lkml/mail --threads 
    --dedupe=mid 
    '(tc:linux-block OR tc:linux-fsdevel) AND rt:1.days.ago..'```

Here t and c indicate to and cc mail recipient respectively.  
Above query also edited later using lei edit-search.

Once the query is finalized, next time to fetch the mails, simply use  
```$ lei up ~/.lkml/mail```

# notmuch:
Installation in Debian/Ubuntu:  
```sudo apt install -y notmuch```  

Above lei setup usually fetches and notmuch helps in filtering the mails  
Typically a notmuch has a config file in ~/.notmuch-config  
This file contains the path to fetch and store the filtered mails  

With notmuch we can filter mails and attach tags to mails.
And this tag will be used by neomutt to create different virtual mailboxes.

To filter mails to/cc to linux-block and attach tag linux-block, we use
$ notmuch tag +linux-block -- to:linux-block@vger.kernel.org

For more tagging batch queries, an input file can be passed.  
Lets say we create a file by name notmuch-tag-rules,  
```$ cat ~/.lkml/notmuch-tag-rules```  
+linux-block -- to:linux-block@vger.kernel.org  
+linux-fsdevel -- to:linux-fsdevel@vger.kernel.org  

This file looks similar to command line query, without 'notmuch tag'
To run this batch tagging,  
```$ notmuch tag --batch --input=~/.lkml/notmuch-tag-rules```

# neomutt:
Installation in Debian/Ubuntu:  
```sudo apt install -y lei```  

neomuttrc is config file, which can be passed to neomutt as argument.  
#### virtual mailbox:
virtual mailboxes help to arrange the mails.
lets say we want to put mails from linux-block under linux-block mailing list.  
    virtual-mailboxes "linux-block" "notmuch://?query=tag:linux-block"  
    virtual-mailboxes "linux-fsdevel" "notmuch://?query=tag:linux-fsdevel"

#### sync/fetch mails  
we make use of bash script to check and sync the mails.  
This script is combination fetching mails from lei and filtering mail
using notmuch.  
let's say we name the script fetch.sh  
```$cat ~/.lkml/sync.sh```  
lei up ~/.lkml/mail  
notmuch new  
notmuch tag --batch --input=~/.lkml/notmuch-tag-rules  
notmuch tag --remove-all +deleted tag:deleted  

we assign F to fetch mail using, and save this in neomuttrc   
macro index F "<shell-escape>path_fetchmail_script 2>&1<enter>" "sync email and notmuch"  

Next I plan to add information about the neomuttrc and linking all together.  
I plan to update improvements here. Stay tuned !!  
