**Bot-tiquette**
*A crowdsourced etiquette for reddit bots.*  
*[Reddit API's Access Rules](#reddit-apis-access-rules) |
[Bot-tiquette](#bot-tiquette) |
[Bots that Should Never be Created](#bots-that-should-never-be-created) |
[Links and Resources](#links-and-resources)*

---

##### Reddit API's Access Rules

- *Make no more than thirty requests per minute.*
- *Change your client's User-Agent string to something unique and descriptive*  
- *Don't hit the same page more than once per 30 seconds.*  
- *Requests for multiple resources at a time are always better than requests
for single-resources in a loop.*

---

##### Bot-tiquette

- **Do not disrupt the flow of the conversation**  
  A bot is meant to enchance the flow of a conversation, not destroy it. This is
  more or less the "golden rule" of bots and many of the following rules are
  based on it.

- **Blacklist certain subreddits unless requested by the subreddit's moderators**  
  Bots do not belong on some subreddits, especially those which encourage serious
  discussion, such as
    [/r/suicidewatch](http://reddit.com/r/suicidewatch) and
    [/r/depression](http://reddit.com/r/depression).
  Before adding a bot to a subreddit, read the sidebar or the wiki to make sure
  bots are allowed in the subreddit. A strong recommendation is to also avoid
  posts labeled "[SERIOUS]" in
    [/r/AskReddit](http://reddit.com/r/askreddit).  
  **Suggestion**: *It might be better for a bot to listen on certain selected
  subreddits rather than all subreddits except blacklisted ones. This makes it
  easier for you to remove the subreddits that you are banned from and eliminate
  wasted searches.*

- **Blacklist certain users on request**  
  There are always users that do not want to be part of your bot. If your bot is
  not explicitly "summoned" by the user, create a way to opt-out of the bot's
  services.  
  **Suggestion**: *Depending on the bot, you may also want to make it opt-in.*

- **Limit the number of replies per submission**  
  To make sure your bot doesn't saturate the thread with replies, keep a
  reasonable cap on the number of replies per submission.  
  **Suggestion**: *Usually, this should be around 5-10 replies depending on the
  size of the subreddit.*

- **Do not have the bot reply to every instance of a common word/phrase**  
  This would not only cause a great amount of "stress" on the bot, it would also
  derail conversations by appearing too frequently in threads. What constitutes
  a common word or phrase is up to the creator.  
  **Suggestion**: *There are many ways to limit the appearance of a bot. You can 
  use a narrower regular expression or only reply to comments with a lot of
  upvotes. __Consider making a bot appear only when specifically called.__*

- **Do not run a duplicate bot**  
  Before releasing your bot, make sure there are no other bots that serve a
  similar purpose to yours. If you are forking a person's code from pastebin or
  github, make sure the original bot is no longer functioning.  
  **Suggestion**: *Some bots are dead for a reason: either they were banned, no
  longer relevant or simply too expensive to run. If you launch a similar bot,
  it might suffer the same fate.*

- **Allow users or moderators to communicate with the creator/maintainer**
  Some subreddits will probably not like your bot or would like to either make
  a few suggestions or want your bot removed from the subreddit. Either list your
  username or a dedicated subreddit in the bot's replies.  
  **Suggestion**: *To make the mention smaller and your reply less bloated, try
  adding a horizontal rule and then put your mention in a caret bracket: ^(...)*

- **Do not evade bans**  
  Your bot has been banned for a reason. Do not try to evade bans by **running the
  same script under multiple usernames**, or **harrasing the moderators**.  
  **Suggestion**: *Do try contacting the moderators asking for a specific reason
  for the ban or offering to tone it down, but be prepared to take no for an
  answer.*

- **Do not upvote posts**  
  The reddit API specifically states that `votes must be cast by humans`. Bots
  should not upvote any posts or amplify a user's upvote.

---
##### Bots that Should Never be Created

- Bots that correct spelling or grammar.
- Bots that restore a deleted comment or post.
- Bots whose sole purpose is to harass a user or group of users.

---
##### Links and Resources

- [**Blacklisted subreddits**](https://raw.github.com/RequestABot/Bottiquette/master/blacklist.json):
  This JSON file can be downloaded and used to skip blacklisted subreddits.
- [**Setting up a bot on Heroku**](https://gist.github.com/avidw/9438841):
  Heroku is a powerful tool for running bots 24/7 with little to no maintenance.
- [**Anti-abuse functions for PRAW**](https://github.com/acini/praw-antiabuse-functions):
  Functions that help bot makers stick to the bottiquette above.
