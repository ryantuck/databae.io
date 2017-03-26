+++
date = "2016-07-17T22:29:59-04:00"
draft = false
title = "build a hugo site"

+++

# tldr

I built this static site from scratch in about an hour and a half using [hugo](http://gohugo.it), hosted it in s3, and re-routed ryantuck.io traffic here.

# why

I wanted to revive my personal site after pygotham 2016. It's been something I've been meaning to do anyway so here we are. I have this weird hatred towards ruby and would never want to have to dig into `jekyll` source code if anything went awry, and I also would prefer to just host this site on s3. So [hugo](http://gohugo.it) it is.

# getting started

I generally followed the instructions here: https://gohugo.io/overview/quickstart/

## setup

```
brew install hugo
cd ~/src
hugo new site ryantuck.io  # build site
cd ryantuck.io
hugo new post/test.md
vim test.md  # write this article
git clone https://github.com/htdvisser/hugo-base16-theme.git base16
hugo server --theme=base16 --buildDrafts  # serve it up
```

Navigate to http://localhost:1313/.

## ship it

Cool. Now let's ship it.

```
hugo  # makes site
aws --profile personal s3 cp public/ s3://ryantuck.io/ --recursive
```

## aws

You'll need to enable web hosting in your bucket and add a bucket policy so you don't get shitty `403` errors:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AddPerm",
            "Effect": "Allow",
            "Principal": {
                    "AWS": "*"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::ryantuck.io/*"
        }
    ]
}
```

That may be way too open (shrug).

Now create a hosted zone in route53 and hook those 4 nameservers up to your domain provider. Wait a bit for DNS to propagate and you're cookin' with gas!



## notes

edit `config.toml` to add a default theme so you don't need to pass that arg in.

`hugo` automatically refreshes if you edit a `.md` file.

to fix, a lack of code syntax highlighting, `pip install pygments` and add `PygmentsCodeFences = "True"` to `config.toml`.


## other cool stuff


`brew install tree`

```
🔥  ~/in/ryantuck.io 🔥  tree -a
.
├── archetypes
├── config.toml
├── content
├── data
├── layouts
├── static
└── themes
```



### weird bug

Okay and after navigating to my site it looks like a turd. Must be lacking a theme. Tried `hugo undraft content/post/test.md` and `hugo --theme=base16` but the first just enabled the draft to be visible.

Looks like it's automatically expecting to pull the css from `ryantuck.io/css/...`, which is no bueno right now because i hadn't re-routed my site yet!





