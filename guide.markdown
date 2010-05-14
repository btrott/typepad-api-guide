<!DOCTYPE html>
<html>
<head>
    <title>TypePad API Developer guide</title>
    <style type="text/css">
    body { background-color: #CCC; font-family: Helvetica, arial, sans-serif; text-align: center; }
    #container { text-align: left; width: 850px; padding: 15px; background-color: #FFF; margin-left: auto; margin-right: auto; }
    .codehilite  { background: #EEE; padding-left: 15px; }
    .codehilitetable { background: #EEE; padding-left: 15px; width: 100%;}
    .codehilite .c { color: #999988; font-style: italic } /* Comment */
    .codehilite .err { color: #a61717; background-color: #e3d2d2 } /* Error */
    .codehilite .k { font-weight: bold } /* Keyword */
    .codehilite .o { font-weight: bold } /* Operator */
    .codehilite .cm { color: #999988; font-style: italic } /* Comment.Multiline */
    .codehilite .cp { color: #999999; font-weight: bold } /* Comment.Preproc */
    .codehilite .c1 { color: #999988; font-style: italic } /* Comment.Single */
    .codehilite .cs { color: #999999; font-weight: bold; font-style: italic } /* Comment.Special */
    .codehilite .gd { color: #000000; background-color: #ffdddd } /* Generic.Deleted */
    .codehilite .gd .x { color: #000000; background-color: #ffaaaa } /* Generic.Deleted.Specific */
    .codehilite .ge { font-style: italic } /* Generic.Emph */
    .codehilite .gr { color: #aa0000 } /* Generic.Error */
    .codehilite .gh { color: #999999 } /* Generic.Heading */
    .codehilite .gi { color: #000000; background-color: #ddffdd } /* Generic.Inserted */
    .codehilite .gi .x { color: #000000; background-color: #aaffaa } /* Generic.Inserted.Specific */
    .codehilite .go { color: #888888 } /* Generic.Output */
    .codehilite .gp { color: #555555 } /* Generic.Prompt */
    .codehilite .gs { font-weight: bold } /* Generic.Strong */
    .codehilite .gu { color: #aaaaaa } /* Generic.Subheading */
    .codehilite .gt { color: #aa0000 } /* Generic.Traceback */
    .codehilite .kc { font-weight: bold } /* Keyword.Constant */
    .codehilite .kd { font-weight: bold } /* Keyword.Declaration */
    .codehilite .kp { font-weight: bold } /* Keyword.Pseudo */
    .codehilite .kr { font-weight: bold } /* Keyword.Reserved */
    .codehilite .kt { color: #445588; font-weight: bold } /* Keyword.Type */
    .codehilite .m { color: #009999 } /* Literal.Number */
    .codehilite .s { color: #d14 } /* Literal.String */
    .codehilite .na { color: #008080 } /* Name.Attribute */
    .codehilite .nb { color: #0086B3 } /* Name.Builtin */
    .codehilite .nc { color: #445588; font-weight: bold } /* Name.Class */
    .codehilite .no { color: #008080 } /* Name.Constant */
    .codehilite .ni { color: #800080 } /* Name.Entity */
    .codehilite .ne { color: #990000; font-weight: bold } /* Name.Exception */
    .codehilite .nf { color: #990000; font-weight: bold } /* Name.Function */
    .codehilite .nn { color: #555555 } /* Name.Namespace */
    .codehilite .nt { color: #000080 } /* Name.Tag */
    .codehilite .nv { color: #008080 } /* Name.Variable */
    .codehilite .ow { font-weight: bold } /* Operator.Word */
    .codehilite .w { color: #bbbbbb } /* Text.Whitespace */
    .codehilite .mf { color: #009999 } /* Literal.Number.Float */
    .codehilite .mh { color: #009999 } /* Literal.Number.Hex */
    .codehilite .mi { color: #009999 } /* Literal.Number.Integer */
    .codehilite .mo { color: #009999 } /* Literal.Number.Oct */
    .codehilite .sb { color: #d14 } /* Literal.String.Backtick */
    .codehilite .sc { color: #d14 } /* Literal.String.Char */
    .codehilite .sd { color: #d14 } /* Literal.String.Doc */
    .codehilite .s2 { color: #d14 } /* Literal.String.Double */
    .codehilite .se { color: #d14 } /* Literal.String.Escape */
    .codehilite .sh { color: #d14 } /* Literal.String.Heredoc */
    .codehilite .si { color: #d14 } /* Literal.String.Interpol */
    .codehilite .sx { color: #d14 } /* Literal.String.Other */
    .codehilite .sr { color: #009926 } /* Literal.String.Regex */
    .codehilite .s1 { color: #d14 } /* Literal.String.Single */
    .codehilite .ss { color: #990073 } /* Literal.String.Symbol */
    .codehilite .bp { color: #999999 } /* Name.Builtin.Pseudo */
    .codehilite .vc { color: #008080 } /* Name.Variable.Class */
    .codehilite .vg { color: #008080 } /* Name.Variable.Global */
    .codehilite .vi { color: #008080 } /* Name.Variable.Instance */
    .codehilite .il { color: #009999 } /* Literal.Number.Integer.Long */
    </style>
</head>

<body><div id="container">

<h1>Contents</h1>

[TOC]

# Users

## Retrieving a user's profile

You can look up a user by his profile alias or his user ID, or, in an authenticated request, using the `@self` token to represent the authenticated user.

By profile alias (raw HTTP request):

    GET /users/btrott.json
    Host: api.typepad.com

By user ID (raw HTTP request):

    GET /users/6p00d83455876069e2.json
    Host: api.typepad.com

In an authenticated request, you have an additional option: you can look up yourself (the authenticated user) using the special `@self` token.

Here's the raw HTTP request:

    GET /users/@self.json
    Host: api.typepad.com
    Authorization: ...

And, from Perl:

    #!perl
    # By profile alias...
    my $user = $tp->users->get( 'btrott' );

    # ... or by user ID ...
    my $user_id = '6p00d83455876069e2';
    my $user = $tp->users->get( $user_id );
    
    # ... or, with authentication, for the authenticated user.
    my $user = $tp->users->get( '@self' );

Endpoints of note:

* [/users/&lt;id&gt;](http://www.typepad.com/services/apidocs/endpoints/users/%253Cid%253E)

## Retrieving a user's profile events

The actions that a user has performed will show up on his/her profile ([example profile](http://profile.typepad.com/btrott)); these actions can also be retrieved from the TypePad APIs.

As with a user's profile itself, you can specify a user by his/her profile alias, user ID, or, in an authenticated request, the token `@self`.

Here's a raw HTTP request:

    GET /users/btrott/events.json
    Host: api.typepad.com

And, from Perl:

    #!perl
    my $events = $tp->users->events( 'btrott' );

Endpoints of note:

* [/users/&lt;id&gt;/events](http://www.typepad.com/services/apidocs/endpoints/users/%253Cid%253E/events)

# Blogs

## Listing a user's blogs

You can fetch the list of blogs for a user, with or without authentication (if you're requesting anyone's blogs but the authenticated user's, only the user's public blogs--those shown on the profile--will be returned).

For the authenticated user (raw HTTP request):

    GET /users/@self/blogs.json
    Host: api.typepad.com
    Authorization: ...

By user ID, with or without authentication:

    GET /users/6p00d83455876069e2/blogs.json
    Host: api.typepad.com

And, from Perl:

    #!perl
    # For the authenticated user...
    my $my_blogs = $tp->users->blogs( '@self' );

    # ... or by ID.
    my $user_id = '6p00d83455876069e2';
    my $his_blogs = $tp->users->blogs( $user_id );

Endpoints of note:

* [/users/&lt;id&gt;/blogs](http://www.typepad.com/services/apidocs/endpoints/users/%253Cid%253E/blogs)

## Retrieving a list of posts on a blog

With authentication as a user with author privileges on the specified blog, you can retrieve all posts (draft, published, or queued); without authentication, or if the authenticated user does not have privileges on the blog, you'll get only the published posts back.

Raw HTTP request, with authentication:

    GET /blogs/6a00d83455876069e200d8353717da69e2/post-assets.json
    Host: api.typepad.com

Raw HTTP request, without authentication:

    GET /blogs/6a00d83455876069e200d8353717da69e2/post-assets.json
    Host: api.typepad.com
    Authorization: ...

Perl sample:

    #!perl
    my $blog_id = '6a012877b13de7970c012877b13df1970c';
    my $asset = $tp->blogs->post_assets( $blog_id );

Endpoints of note:

* [/blogs/&lt;id&gt;/post-assets](http://www.typepad.com/services/apidocs/endpoints/blogs/%253Cid%253E/post-assets)

## Displaying recent published posts on a blog

Javascript sample, using jQuery:

    #!html
    <ul id="blog-widget"></ul>
    <script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.4.2/jquery.min.js"></script>
    <script type="text/javascript">
    var blogId = '6a00d83455876069e200d83455876369e2';
    $( '#blog-widget' ).ready( function() {
        $.getJSON(
            'http://api.typepad.com/blogs/' + blogId + '/post-assets/@published/@recent.js?callback=?',
            { 'max-results': 5 },
            function( data ) {
                var ul = $( '#blog-widget' );
                for ( var i = 0, len = data.entries.length; i < len; i++ ) {
                    ul.append( '<li><a href="' + data.entries[ i ].permalinkUrl + '">' + data.entries[ i ].title + '</a></li>' );
                }
            }
        );
    } );
    </script>

## Posting to a blog

Raw HTTP request:

    POST /blogs/6a00d83455876069e200d8353717da69e2/post-assets.json
    Host: api.typepad.com
    Authorization: ...
    Content-Length: 89
    Content-Type: application/json
    
    {"textFormat":"html","content":"<p>First paragraph.</p>","title":"Something interesting"}

Perl sample:

    #!perl
    my $blog_id = '6a012877b13de7970c012877b13df1970c';
    my $asset = $tp->blogs->new_post_asset( $blog_id, {
        title       => 'Something interesting',
        content     => '<p>First paragraph.</p>',
        textFormat  => 'html',
    } );

Endpoints of note:

* [/blogs/&lt;id&gt;/post-assets](http://www.typepad.com/services/apidocs/endpoints/blogs/%253Cid%253E/post-assets)

## Commenting

You can post a comment either anonymously (authentication using your anonymous access token, but not as a specific user) or as an authenticated user.

In both cases, you'll need to send an `Authorization` header with OAuth credentials; the difference is that, in the case of commenting anonymously, you'll send your "Anonymous Access Key" and sign your request using your "Anonymous Access Secret", and in the case of commenting as an authenticated user, you'll use the access token and secret that you received for the authenticated user.

Anonymously (raw HTTP request):

    POST /assets/6a00d83455876069e20133ec50b8fa970b/comments.json
    Host: api.typepad.com
    Authorization: ...
    Content-Length: 83
    Content-Type: application/json
    
    {"content":"This is my comment.","name":"Someone","href":"http://www.example.com/"}

With authentication (raw HTTP request):

    POST /assets/6a00d83455876069e20133ec50b8fa970b/comments.json
    Host: api.typepad.com
    Authorization: ...
    Content-Length: 33
    Content-Type: application/json
    
    {"content":"This is my comment."}

And, in Perl:

    #!perl
    # Posting a comment anonymously...
    my $tp_anon = WWW::TypePad->new(
        consumer_key        => 'your consumer key',
        consumer_secret     => 'your consumer secret',
        access_token        => 'your anonymous access key',
        access_token_secret => 'your anonymous access secret',
    );
    my $post_id = '6a012877b13de7970c012877b143d0970c';
    my $comment = $tp_anon->assets->new_comment( $post_id, {
        content => 'This is my comment.',
        name    => 'Someone',
        href    => 'http://www.example.com/',
    } );

    # ... or with authentication.
    my $post_id = '6a012877b13de7970c012877b143d0970c';
    my $comment = $tp->assets->new_comment( $post_id, {
        content => 'This is my comment.',
    } );

Endpoints of note:

* [/assets/&lt;id&gt;/comments](http://www.typepad.com/services/apidocs/endpoints/assets/%253Cid%253E/comments)

## Reblogging

To reblog a post on TypePad, you use the same endpoint that you use to create a new post, but you include an additional `reblogOf` property in the request. The `reblogOf.urlId` value should be the post ID of the TypePad post that you're reblogging.

In this request, `content` will, as when creating a new post, contain the entire contents of the new post. If you'd like to attribute the reblog to the original post--or include a snippet of text as a blockquote, etc--you should include the HTML for that attribution in `content`.

    #!perl
    my $blog_id = '6a012877b13de7970c012877b13df1970c';
    my $post_id = '6a012877b13de7970c012877b143d0970c';
    my $asset = $tp->blogs->new_post_asset( $blog_id, {
        title       => 'I read this',
        content     => '<p>Someone said...</p>',
        textFormat  => 'html',
        reblogOf    => {
            urlId   => $post_id,
        }
    } );

Endpoints of note:

* [/blogs/&lt;id&gt;/post-assets](http://www.typepad.com/services/apidocs/endpoints/blogs/%253Cid%253E/post-assets)

## Uploading Photos

    #!perl
    my $blog_id = '6a012877b13de7970c012877b13df1970c';
    my $filename = 'some-file.jpg';
    my $asset = $tp->blogs->upload_media_asset(
        $blog_id,
        { title => 'New Photo' },
        $filename,
    );

To embed a 500-pixel-wide version of that photo in a post, do this:

    #!perl
    ( my $img_uri = $asset->{imageLink}{urlTemplate} ) =~ s/{spec}/500wi/;
    
    my $body = <<HTML;
    <p><img src="$img_uri" class="at-xid-$asset->{urlId}" /></p>
    
    <p>I like this photo!</p>
    HTML
    
    my $blog_id = '6a012877b13de7970c012877b13df1970c';
    my $asset = $tp->blogs->new_post_asset( $blog_id, {
        title       => 'Nice photo',
        content     => $body,
        textFormat  => 'html',
    } );

The special <code>class</code> attribute on the <code>img</code> tag tells TypePad that the image you're embedding is tied to a photo on TypePad; specifically, the photo that you just uploaded. That allows TypePad to do more intelligent things with the structure of the post, and maintain a relationship between the post and the photo.

Endpoints of note:

* [/blogs/&lt;id&gt;/post-assets](http://www.typepad.com/services/apidocs/endpoints/blogs/%253Cid%253E/post-assets)
* [/blogs/&lt;id&gt;/media-assets](http://www.typepad.com/services/apidocs/endpoints/blogs/%253Cid%253E/media-assets)

# Favorites

You can add any asset to the list of favorites for the authenticated user.

Raw HTTP request:

    POST /users/@self/favorites.json 
    Host: api.typepad.com
    Authorization: ...
    Content-Length: 60
    Content-Type: application/json
    
    {"inReplyTo":{"urlId":"6a00d83455876069e20133ec50b8fa970b"}}

And, in Perl:

    #!perl
    my $user_id = '6p00d83455876069e2';
    my $post_id = '6a012877b13de7970c012877b143d0970c';
    $tp->users->new_favorite( '@self', {
        inReplyTo => { urlId => $post_id }
    } );

Endpoints of note:

* [/assets/&lt;id&gt;/favorites](http://www.typepad.com/services/apidocs/endpoints/assets/%253Cid%253E/favorites)
* [/users/&lt;id&gt;/favorites](http://www.typepad.com/services/apidocs/endpoints/users/%253Cid%253E/favorites)

</div></body>
</html>
