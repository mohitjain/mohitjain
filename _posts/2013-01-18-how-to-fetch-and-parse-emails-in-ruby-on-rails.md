---
title: How to fetch and parse emails in ruby on rails
author: Mohit Jain
layout: post
comments: true
categories: quick-solution tips-and-tricks
---

Last weekend I was working on a mini hackathon and launched a group emailing service. [EmailList.io][1]. The task was to setup an email server, how to fetch and parse emails in ruby on rails forward it to respective group members. Last part was pretty simple. In this post, I am just talking about “How to fetch and parse emails in ruby on rails.”

 [1]: http://emaillist.io/?utm_source=codebeerstartups&utm_medium=blogpost&utm_campaign=codebeerstartups

To fetch email using POP/IMAP you check out a gem ie [mailman][2].
Here is the sample code for the same:

 [2]: https://github.com/titanous/mailman

1. Install the gem
2. Create a script file in scripts folder ie mailman_server and just paste the code below,
   which itself is pretty clear. Check inline comments.



## Basic Parsing

{% highlight ruby %}

  #!/usr/bin/env ruby
  require "rubygems"
  require "bundler/setup"
  require "mailman"
  #Mailman.config.logger = Logger.new("log/mailman.log")  # uncomment this if you can want to create a log file
  Mailman.config.poll_interval = 3  # change this number as per your needs. Default is 60 seconds
  Mailman.config.pop3 = {
    server: 'pop.gmail.com', port: 995, ssl: true,
    username: "GMAIL_USERNAME",
    password: "GMAIL_PASSWORD"
  }
    Mailman::Application.run do
    default do
      begin
      p "Found a new message"
      p message.from.first # message.from is an array
      p message.to.first # message.to is an array again..
      p message.subject
      rescue Exception => e
        Mailman.logger.error "Exception occurred while receiving message:n#{message}"
        Mailman.logger.error [e, *e.backtrace].join("n")
      end
    end
  end

{% endhighlight %}

So far it's pretty easy, but the question is how to parse the email body as HTML, text and parse attachments. Now take a look on this. Pretty simple.

## Get attachments, HTML and Text Body

{% highlight ruby %}

  if message.multipart?
    email_html = message.html_part.body.decoded  #parsing of html content of the email
    email_text = message.text_part.body.decoded  # parsing of text content of the email
    email_attachments = []   # an array which can be used to store object records of the attachments..
    message.attachments.each do |attachment|
      file = StringIO.new(attachment.decoded)
      file.class.class_eval { attr_accessor :original_filename, :content_type }
      file.original_filename = attachment.filename
      file.content_type = attachment.mime_type
      attachment = Attachment.new    # an attachment model and all the attachments are saved here...
      attachment.attached_file = file
      attachment.save
      email_attachments << attachment   # adding all attachment objects one by one in the array...
    end
  else
    email_html = message.body.decoded    # in this case its a plain email so html body is same as text body..
    email_text = message.body.decoded
    email_attachments = []   # no attachments :)
  end

{% endhighlight %}
Once you have parsed all the attributes from the email ie to, from, email attachments now you can easily pass it to delayed job or something like creating a ticket or whatever you want to do as per you needs ;)

If you are facing any issues. Check out the source code files at [github][3]. Still, if you have any doubts contact me or you can comment on the blog post itself.

  [3]: https://github.com/mohitjain/mailman_example_code
