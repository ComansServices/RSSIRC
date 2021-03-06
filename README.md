--------------------------------------------------------------------------------
# Eggdrop RSS Syndication

# Setup:
======

 Follow the examples below. It is possible to define values in either the default variable or within the individual rss feed variables. You can define values in both places, but each feeds individual settings will overwrite the default ones.

# Values:
=======

 Required:
 ---------
  `url`              The URL of the RSS/ATOM feed.
                   Example: http://www.example.tld/feed.xml
                            https://www.example.tld/feed.xml
                            http://username:password@www.example.tld/feed.xml

  `channels`         List of channels the feed (and trigger) are to be active in.
                    (Use space to separate multiple channels)

  `database`         Full (or relative from your eggdrops path) path to where you
                    want to store the database file.
                   Example: ./scripts/feedname.db

  `output`           The format you would like the RSS to be outputted to you
                    channel in.

  `max-depth`        Maximum amount of times the script should follow Location:
                    headers. Keep this relatively low.
                   Default: 5

  `timeout`          Timeout f connections (in milliseconds).
                   Default: 60000

  `user-agent`       User agent to send in the http request.

  `announce-type`    How you want the announce updates to be sent to your
                    channels.
                    Options:
                     0 = Message Channel
                     1 = Notice Channel
                   Default: 0

  `announce-output`  Maximum articles to output to channel on announce.
                   Default: 3

  `trigger-type`     How you want the trigger replies to be sent when triggered
                    both in channel and via private message.
                    The format is: <channel>:<privmsg>
                    Options:
                     0 = Message Channel
                     1 = Notice Channel
                     2 = Message User
                     3 = Notice User
                   Default: 0:2

  `trigger-output`   Maximum articles to output when triggered.
                   Default: 3

  `update-interval`  How often (in minutes) you want the feed to be checked. Try
                    and keep this number sensible, something above 15 minutes.
                    Some websites will ban you for hammering their feeds.
                   Default: 30

 Optional:
 ---------
  `trigger`          Public trigger to list feeds. (if you only want to define it
                    once in default use @@feedid@@, this will be replaced by
                    each individual feeds id)

  `evaluate-tcl`     Evaluate the output before sending it to channel.
                   Default: 0 (Off)

  `enable-gzip`      Enable gzip decompression for this feed.
                   Default: 0 (Off)

  `remove-empty`     Remove empty cookies from the output.
                   Default: 1 (On)

  `output-order`     The order you want the articles to be announced in channel.
                   Options:
                    0 = Ascending (Oldest -> Newest)
                    1 = Descending (Newest -> Oldest)

  `charset`          This is the charset you want the feed to be outputted using.
                    The default charset is what your local system charset is set
                    to use. In most cases, if you're having problems with output
                    just use utf-8.
                   Example: utf-8
                            cp1251
                            iso8859-1

# Cookies:
========

  Output works on a cookie system, in this case its dynamic so it depends on
   what data the feed contains as to what you can output.

  As of version 0.3 you are able to reference any tag within each article, or if you really want the whole feed. The format is ``@@<tag>!<subtag>!...@@,@@item@@ and @@entry@@`` cookies are 'shortcuts' and will always point to the current article. If you wish to output an attribute of a tag you can do that by using the attribute name with an = in front of it (eg: ``@@entry!link!=href@@``). This would get the 'href' attribute from the
   <link> tag. Refer to rss-synd.tcl for more examples.

# Dependencies:
=============

 This script will run perfectly fine without any of these dependencies, but
  if you want any of these features you'll need to download and install the
  respective package(s).

 HTTP Authorisation:
 -------------------
  Requires: base64 package from tcllib to be installed.
  URL: http://tcllib.sourceforge.net/

 HTTPS:
 ------
  Requires: TLS package to be installed.
  URL: http://www.sensus.org/tcl/

 Gzip Decompression:
 -------------------
  Requires: Trf package to be installed.
  URL: http://tcltrf.sourceforge.net/

# Frequently Asked Question:
==========================

 Q: The output to my channel has a lot of random \'s everywhere.
 A: set the 'eval-tcl' option to 0 (off).

 Q: My feeds announce all the articles in the feed, not just the news ones.
 A: You've either used the same database file for two feeds, or there isnt one
     set that's working. Make sure the path where your putting your files is
     writable!

 Q: The output to my channel has the annoying cookies still in it.
 A: set the 'remove-cookies' option to 1 (on)

 Q: I cant see what cookies are wrong! what can I do?
 A: set the 'remove-cookies' option to 0 (off)

 Q: The feed wont work properly and I'm not sure why!
 A: Make sure the feed is valid check it with http://feedvalidator.org/. If the
     feed has errors, it probably wont work.

 If there are any other questions you have, feel free to email me.

--------------------------------------------------------------------------------
