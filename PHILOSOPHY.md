**Philosophy**
*How bots should be programmed in order to be fast, efficient
 and manageable.*

*This document assumes that you are using the PRAW library in
python. Nevertheless, the points apply to a bot written in
any language, although the code examples are only applicable
to PRAW/Python.*

---

- **Store sensitive details as environment variables**  
  Git is not only a great revision control tool but also a
  great deployment tool. This makes it easier to deploy to
  Github or Bitbucket and a server at the same time. Saving
  details in a properties file makes it more cumbersome.
  It is also benficial for security; anyone who has your
  code cannot gain access to the bot or your database.

  ```python
    # This code example is a bit forgiving:
    def login(username=None, password=None):
      username = os.environ.get("REDDIT_USERNAME", username)
      password = os.environ.get("REDDIT_PASSWORD", password)
      if username == None or password == None:
        raise Exception("You did not provide a reddit username or password!")
      ...
  ```
  
- **Bots should be able to run in short bursts or continuous loops**  
  This should be kept in mind when writing a bot. There can
  be many errors that could terminate your bot, especially
  in the first few weeks of running the bot. For example,
  *never* store completed comment ids in a list in memory,
  since there is no way to retrieve them if the script
  terminates.

  ```python
    from requests import HTTPError
    
    try:
      comment.reply(reply)
    except HTTPError:
      print("Probably banned from /r/" + str(comment.subreddit), file=sys.stderr)
    except praw.errors.RateLimitExceeded as e:
      print("Rate limit %d seconds" % error.sleep_time, file=sys.stderr)
  	  time.sleep(error.sleep_time)
  ```
  
  ```python
    # a backup to determine if the bot has already commented
    
    comment = r.get_submission(url="...").comments[0]
    already_commented = any(reply.author != None or str(reply.author) != username for reply in comment.replies)
  ```
  
- **Only one instance of the bot is run simultaneously**  
  This is a possible problem of running your bot with a
  cron job. The scheduler may start another instance of
  your bot before the first one has completed. This may
  cause the bots to comment on the same submission/comment
  twice. There are many ways to solve this, such as using
  a PID file or using the `tendo` module as shown below.

  ```python
  # http://stackoverflow.com/a/1265445/898577
  from tendo import singleton
  me = singleton.SingleInstance()
  ```

- **Completed IDs should be stored in a persistent database**  
  This makes your application portable and also prevents you
  from losing your previous completed ids.

  ```python
  import bmemcached # or other key-value stores like redis  
  m = bmemcached.Client((os.environ['MEMCACHEDCLOUD_SERVERS'],), 
                         os.environ['MEMCACHEDCLOUD_USERNAME'],
                         os.environ['MEMCACHEDCLOUD_PASSWORD'])
                         
  comment.reply("Hello World")
  m.set(str(comment.id), "True")
  
  if m.get(str(comment.id)):
    comment.reply("Hello Again") # will not run
  ```
  
- **Bot should be very verbose and recent output should be logged**  
  This makes debugging or problem-solving much easier.
  All you need to do is to print output.

  ```python
  from __future__ import print_function
  import sys
  
  try:
    print("Reply to %s" % comment.permalink)
    comment.reply("Hello World")
  except praw.errors.RateLimitExceeded as e:
    print("Rate limit %d seconds" % e.sleep_time, file=sys.stderr)
  ```

- **Bot should not listen on /r/all**  
  The bot should not listen on r/all but a list of specified
  subreddits. This makes removing banned subreddits easier
  and the bot more targeted.

  ```python
  def listen(r, subreddits):
    multi = "+".join(subreddits)
    for comment in praw.helpers.comment_stream(r, multi, limit=None)
      print(comment.permalink)
  ```
