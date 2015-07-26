# blogBashCommandlineClient

Edits wordpress blog entries, offline and completely from bash, creating an editions cache. user can upload changes when online. Uses the Incutio php library ().

## Installation

* On your linux box, put both files on a directory with executable permissions (you can use /usr/local/bin or ~/bin; we'll use the last one). For example, my own home directory is `/home/rodolfoap`, so I installed it like this:

```
    /home/
    └── rodolfoap
        └── bin
            ├── blog
            └── class-IXR.php
```

The PATH variable was modified on the last line of my ~/.bashrc like this:

    export PATH=~/bin:$PATH

Configure this three lines on the ~/bin/blog file:

	public $user = 'rodolfoap';
	public $pass = 'NotHere,MyFriend';
	public $site = 'http://blog.ydor.org';

## Usage 

### Help

To ask for help, just type the **blog** or **blog help** command.

    $ blog
    Usage:	/home/rodolfoap/bin/blog [ help | download | list | listcat | edit [ID] | new | upload [ID] | publish [ID] | unpublish [ID] | delete [ID] ]

    $ blog help
    Usage:	/home/rodolfoap/bin/blog [ help | download | list | listcat | edit [ID] | new | upload [ID] | publish [ID] | unpublish [ID] | delete [ID] ]

### Download posts

To download all posts to your PC's cache, just write the **blog download** command:

    $ blog download
    /home/rodolfoap/.blog created.
    Getting posts... done.
    Writing /home/rodolfoap/.blog/post_47
    Writing /home/rodolfoap/.blog/text_47
    Writing /home/rodolfoap/.blog/post_44
    Writing /home/rodolfoap/.blog/text_44
    Writing /home/rodolfoap/.blog/post_42
    Writing /home/rodolfoap/.blog/text_42
    Writing /home/rodolfoap/.blog/post_40
    Writing /home/rodolfoap/.blog/text_40
    Writing /home/rodolfoap/.blog/post_37
    Writing /home/rodolfoap/.blog/text_37
    Writing /home/rodolfoap/.blog/post_29
    Writing /home/rodolfoap/.blog/text_29
    Writing /home/rodolfoap/.blog/post_26
    Writing /home/rodolfoap/.blog/text_26
    Getting categories... done.
    Writing /home/rodolfoap/.blog/categories

### Lists posts

You can see a list of posts with the **blog list** command:

    $ blog list

     [26]	(draft) 	Mental issues are about Interaction
     [29]	(publish) 	The Theory of Interaction and Science
     [37]	(publish) 	The Theory of Interaction and Kisses
     [40]	(publish) 	The Theory of Interaction and Economic Molecules
     [42]	(draft) 	Time and TOI
     [44]	(draft) 	Can the good guys defeat the bad guys?
     [47]	(draft) 	The Theory Of Interaction and Time

### List categories

You can see a list of categories with the **blog listcat** command:

    $ blog listcat

     [Society]: Social issues
     [Theory Of Interaction]: Issues related to the TOI

### Add a new post

To create a new post, use the **blog new** command.

    $ blog new

The application will show you the file created:

    Draft /home/rodolfoap/.blog/draft_1077 was created.

You can list the titles, and this will be classified as *(local)*.

    $ blog list
     ...
     [1077]	(local) 	POST_TITLE[1834736437]

### Posts edition

To edit posts, use the **blog edit [ID]** command.

    $ blog edit 1077

The format is like this:

    POST_TITLE[1834736437] (This line holds the title, change it as you wish)
    -----
    Society, Theory Of Interaction (This line holds the categories)
    -----
    Write here... (The actual post starts here)

*Do not delete the hypens!* they are used to detect the format.

You can use the **blog edit [ID]** as well to edit posts already on the site. But they are not updated online. You need to upload them manually.

    $ blog edit 26

* Please notice that the editor uses the "vi" command. You can change that on the app.

### Upload

After you have edited the new post with the **blog edit [ID]** command...

    $ blog edit 1077

... you need to upload it:

    $ blog upload 1077

    Posting... Post added successfully.
    Post state is: unpublish

    Getting posts... done.
    Writing /home/rodolfoap/.blog/post_80
    Writing /home/rodolfoap/.blog/text_80
    Writing /home/rodolfoap/.blog/post_47
    Writing /home/rodolfoap/.blog/text_47
    Writing /home/rodolfoap/.blog/post_44
    Writing /home/rodolfoap/.blog/text_44
    Writing /home/rodolfoap/.blog/post_42
    Writing /home/rodolfoap/.blog/text_42
    Writing /home/rodolfoap/.blog/post_40
    Writing /home/rodolfoap/.blog/text_40
    Writing /home/rodolfoap/.blog/post_37
    Writing /home/rodolfoap/.blog/text_37
    Writing /home/rodolfoap/.blog/post_29
    Writing /home/rodolfoap/.blog/text_29
    Writing /home/rodolfoap/.blog/post_26
    Writing /home/rodolfoap/.blog/text_26

    Getting categories... done.
    Writing /home/rodolfoap/.blog/categories

    $ blog list

     [26]	(draft) 	Mental issues are about Interaction
     [29]	(publish) 	The Theory of Interaction and Science
     [37]	(publish) 	The Theory of Interaction and Kisses
     [40]	(publish) 	The Theory of Interaction and Economic Molecules
     [42]	(draft) 	Time and TOI
     [44]	(draft) 	Can the good guys defeat the bad guys?
     [47]	(draft) 	The Theory Of Interaction and Time
     [80]	(draft) 	A new post

### Publishing posts

In this example, the uploaded post is the *80*. So, the old local-ID (1077) is lost. After upload, the post changes its ID (80).

After uploading a new post, its status is always *unpublish*. To publish it, use the **blog publish [ID]** command:

    $ blog publish 80

    Post updated successfully.
    Post 80 state is: publish
    Getting posts... 

### UNpublishing posts

To unpublish a post (wordpress status to draft), use the **blog unpublish [ID]** command:

    $ blog unpublish 80

    Post updated successfully.
    Post 80 state is: unpublish
    Getting posts... 

### Deleting posts

To delete a post (wordpress status to draft), use the **blog delete [ID]** command:

    $ blog delete 80

    Deleting... Post 80 deleted successfully.
    Getting posts... 

I don't know if you can recover a deleted post on Wordpress, so verify it before deleting posts.
