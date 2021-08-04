# Configuration File

As of v1.2.0, GramAdict supports a configuration file and **it is 100% recommended**. Let me repeat, if you use GramAddict, you should be using a configuration file. You should not be using arguments anymore. *You technically can, but we have up to 66 arguments now... so it's a lot easier if you use the configuration file.*

To make it easy, to get started... we have a configuration file with every single option argument available in it. You just need to comment out any lines that you don't want to use with a `#`. You can [download that file here](https://raw.githubusercontent.com/GramAddict/bot/master/config-examples/config.yml) (right click on the link -> save as). This file should be placed in a folder within your **GramAddict** folder, named after your username which is inside accounts main folder (if you don't create that folder, the bot will do it for you on the first run). e.g `accounts/username/config.yml` You can have multiple configuration files per user and are encouraged to do so. For example, I use one that is my normal "interaction" config and another that is a "clean up" config. e.g `accounts/username/interact.yml` and `accounts/username/unfollow.yml`.

<br/>

# Available Arguments

GramAddict can do many things and the list is constantly growing. This is a full list of the command line arguments that can be provided in order for you to get started using it.

## General Configuration

| Argument         | Type     | Description | Default |
| -----------------| :------: | ---         |---      |
| username         | Required | The username for which you are running the script | `None` |
| device           | Optional | Device identifier. Specifies which device should be used for the profile from `adb devices`. Use this argument only if you have multiple devices connected at the same time. | `None` |
| app-id           | Optional | Allows you to specify a custom app name for cloned apps | `com.instagram.android` |
| screen-sleep     | Optional | Set to true to turn device screen off once script has finished | `false` |
| screen-record    | Optional | Record the screen while using the bot. This is intended only for debug purposes | `false` |
| debug            | Optional | For troubleshooting. Debug is already sent to log file, this shows it in console | `false` |
| speed-multiplier | Optional | You can set the speed of the bot. > 1 will increase the speed, < 1 will slow down. It can also be a fraction: for example 1.3 | `1` |
| close-apps       | Optional | With this you can tell the bot to close all the background apps to avoid interferences | `true` |
| disable-filters  | Optional | Instead of deleting/renaming your filter.yml file, you can ignore it with this argument | `false` |
| disable-block-detection | Optional | You can disable the detection of action block by putting this paramether to `true` | `false` |
| scrape-to-file   | Optional | The bot will no longer interact with anyone, but it will collect and store all the usernames that fit your filters in a file. This is usually done by a fake account. The generated list will be used by your main account with the argument `--interact-from-file`  | `false` |


<br />

## Actions

No particular action is required, but at least one action is required. If you specify multiple actions, the actions will be executed in the order specified or shuffled with `--shuffle-jobs`. The logistics of multiple action support is discussed [below](#multiple-action-support) with examples.

What an "interaction" is depends on your [source limits](#source-limits), but generally the following types are supported at this time:

- Like Photos/Videos
- Follow
- Comment a post
- Send a PM
- Watch Stories

### Interaction

| Argument                  | Description | Example |
|-------------------------  |---          |---      |
| blogger-followers         | List of usernames with whose followers you want to interact. | `[username1, username2]` |
| blogger-following         | List of usernames with whose following you want to interact. | `[username1, username2]` |
| blogger-post-likers       | List of usernames with whose post likers you want to interact. | `[username1, username2]` |
| blogger                   | List of usernames with whom you want to interact. | `[username1, username2]` |
| hashtag-likers-top        | List of hashtags in top results with whose likers you want to interact. | `[hashtag1, hashtag2]` |
| hashtag-likers-recent     | List of hashtags in recent results with whose likers you want to interact.  | `[hashtag1, hashtag2]` |
| hashtag-posts-top         | List of hashtags in top results with whose posts you want to interact. | `[hashtag1, hashtag2]` |
| hashtag-posts-recent      | List of hashtags in recent results with whose posts you want to interact. | `[hashtag1, hashtag2]` |
| place-likers-top          | List of places in top results with whose likers you want to interact. | `[place1, place2]` |
| place-likers-recent       | List of places in recent results with whose likers you want to interact.  | `[place1, place2]` |
| place-posts-top           | List of places in top results with whose posts you want to interact. | `[place1, place2]` |
| place-posts-recent        | List of places in recent results with whose posts you want to interact. | `[place1, place2]` |
| interact-from-file        | Path to a text file of usernames that will be interacted with. | `[usernames_list1.txt, usernames_list2.txt]` |
| posts-from-file           | Path to a text file of posts that will be liked. More actions will come in the future. Useful for engagement groups. | `[posts_list1.txt, posts_list2.txt]` |
| delete-interacted-users   | Not actually an action, but an option for `interact-from-file`, `posts-from-file` and `unfollow-from-file` to remove users/urls from file after they are interacted with | ` ` |
| feed                      | Interact with your own feed. After that argument you can specify how many likes you want to give. It accepts ranges | `2-5` |

<br />

### Unfollow

| Argument                    | Description | Example |
|---------------------------- |---          |---      |
| unfollow                    | Unfollow at most the given number of users. Only users followed by this script will be unfollowed. | `10-20` |
| unfollow-any                | Unfollow at most the given number of users. Any user is eligible to be unfollowed regardless of if this script followed them. | `10-20` |
| unfollow-non-followers      | Unfollow at most the given number of users, that don't follow you back. Only users followed by this script will be unfollowed. | `10-20` |
| unfollow-any-non-followers  | Unfollow at most the given number of users, that don't follow you back. Any user is eligible to be unfollowed regardless of if this script followed them. | `10-20` |
| unfollow-from-file          | Unfollow usernames from a list (.txt)  | `[usernames_list1.txt, usernames_list2.txt]` |
| sort-followers-newest-to-oldest   | Not actually an action, but an option for all unfollow types except the one from file to sort users from newest to oldest instead of oldest to newest which is the default choice | ` ` |

<br />

### Post Processing

| Argument        | Description                 | Default       |
|--------------   |--------------------------   |---------      |
| analytics       | Generates a PDF analytics report for current username session data. For using this feature you have to install the dependencies: `pip3 install gramaddict[analytics]`  | `false` |
| telegram-report | Generates a report for current username session data and send it to your telegram channel. <br /> For using this feature you have first to configure the file `telegram.yml` in your account folder. <br /> [Instructions here](#telegram-reports). For using this feature you have to install the dependencies: `pip3 install gramaddict[telegram-reports]`| `true` |

<br />

## Source Limits

| Argument            | Description | Default |
|-------------------- |---          |---      |
| interactions-count  | Number of interactions per source in each action. | `70` |
| likes-count         | Number of likes for each interacted user. | `2` |
| likes-percentage    | Chance of liking posts on a particular profile. |`100`|
| stories-count       | Number of stories for each interacted user. | `0` |
| stories-percentage  | Chance of watching stories on a particular profile. Supported by plugins: hashtag-likers, hashtag-posts, blogger-followers. | `30` |
| carousel-count      | Number of available carousel items to browse. | `0` |
| carousel-percentage | Chance of browsing a carousel. | `0` |
| max-comments-pro-user | Number of comments you can do for each user you interact. | `0` |
| comments-percentage | Chance of commenting on a user post. | `0` |
| pm-percentage       | Chance of sending a private message to a user you're interacting with. | `0` |
| interact-percentage | Chance to interact with user/hashtag when applicable. Supported by plugins: hashtag/place-posts and feed". | `50` |
| follow-percentage   | Follow the given percentage of interacted users. | `0` |
| follow-limit        | Limit on amount of follows per source in each action. | `0` |
| skipped-list-limit  | Limit how many scrolls tried, with already interacted users, until we move to the next source. Does not apply for unfollows. | `10-15` |
| fling-when-skipped  | Fling (instead of scroll) after "X" many scrolls tried, with already interacted users. (not recommended - disabled by default) | `0` |
| min-following       | Minimum amount of followings, after reaching this amount unfollowing stops | `0` |
| blogger-post-limits | Limit of blogger post which likers you are interacting (`--blogger-post-likers`) before ending job. **NOT YET DEVELOPED** | `2` |


<br />

## Total Limits

| Argument                            | Description | Default |
|---                                  |---          |---      |
| total-likes-limit                   | Limit on total amount of likes during the session across all sources. | `300` |
| total-follows-limit                 | Limit on total amount of follows during the session across all sources. | `50` |
| total-unfollows-limit               | Limit on total amount of unfollows during the session across all sources. | `50` |
| total-watches-limit                 | Limit on total amount of story watches during the session across all sources. | `50` |
| total-successful-interactions-limit | Limit on total amount of successful interactions during the session across all sources. | `100` |
| total-interactions-limit            | Limit on total amount of successful and non-sucessful interactions during the session across all sources. | `1000` |
| total-comments-limit                | Limit on total amount of comments during the session across all sources. | `300` |
| total-pm-limit                      | Limit on total amount of private-messages during the session across all sources. | `300` |
| total-scraped-limit                 | Limit on total amount of scraped users you will collect during the session across all sources. | `300` |
| total-crashes-limit                 | Limit on total amount of crashes during the session you are willing to accept. Reaching this limit will stop the bot. | `300` |

<br />

### What's the difference between total-interactions-limit and total-successful-interactions-limit?
- total-interactions-limit
>every time you open a profile, it counts as an interaction, even if you don't interact

- total-successful-interactions-limit
>when you open a profile and perform an action such as a like, follow, comment, PM or watch a story, this counts as a successful interaction



## Special modifiers for jobs and sources

| Argument | Description | Example |
|---       |---          |---      |
| shuffle-jobs                  | Instead of following the order of the jobs you write, this argument will allow the bot to shuffle the jobs | `300` |
| truncate-sources              | If you have a lot of sources, with this argument you're able to pick n random from the list and interact only with them, for that session | `2-3` |
| watch-video-time       | Instead of liking videos without watching them, you can fake it and pause the bot for a given time (in seconds). Set to 0 to disable it. | `15-35` |
| watch-photo-time       | Instead of liking photos without looking them, you can fake it and pause the bot for a given time (in seconds). Set to 0 to disable it. | `3-4` |
| can-reinteract-after   | With that feature you can re-interact someone who has already interacted. You have to specify the amount of hours that have to pass from the last interaction | `36` or even fractions `5.5` |
| pre-script | Specify the pre script file path to be executed | `pre_file.bat` |
| post-script | Specify the post script file path to be executed | `post_file.bat` |
<br />

## Scheduling

| Argument | Description | Example |
|---       |---          |---      |
| repeat   | Repeat the same session again after N minutes after completion, disabled by default. | `120-180` |
| working-hours   | Scheduler for bot activity. You can specify the interval (one or more) of time in which you want the bot to run. You must use the time notation 0-24. You can use with the above argument `--repeat` to have a never stop bot.  | `[10.15-16.40, 18.15-22.46]` |
| time-delta   | This is intended to be used with `working-hours` and allows to change the start and the end point of each interval. A random value, positive or negative, will be generated. Math example: `bot-will-run-at = working-hours ± ΔT` | `10-15` |
|total-sessions |  You can specify how many sessions you want to perform before the bot stops. By default it's infinite sessions. It works only if `repeat` argument is provided. | `3-4` | 

## Available Filters

We know that you want to make sure that you only interact with a specific set of users. When you leave it up to a bot, you never know what will happen. We try to make this easier for you by giving you a wide subset of filters to help weed out the undesirables. The full list is below, but if you need some inspiration - there is a filter.example file included with some sensible defaults. You can copy/paste this file from config-example folder (available with git installation) in your account folder or [download it from here](https://raw.githubusercontent.com/GramAddict/bot/master/config-examples/filters.yml)(right click on the link -> save as) and place in your account folder. 
I'll repeat another time: in order to work, that file must be located in `accounts/yourusername` folder.

The following is an exhaustive explanation of what the filters are for:
```
skip_business             
      If it is true, business acounts won't be interacted with.
      (e.g. skip_business: true)

skip_non_business       
      If it is true, private accounts and public accounts 
      won't be interacted with.
      (e.g. skip_non_business: true)

skip_following
      If it is true, accounts that you follow won't be interacted
      with. 
      (e.g. skip_following: true)

skip_follower
      If it is true, accounts that follow you won't be interacted
      with. Note, if you follow someone, the filter won't be able
      to tell if that person follows you.
      (e.g. skip_following: true)

skip_if_link_in_bio
      If it is true, you will skip accounts if they have a link in bio
      (It's located under the biography)
      (e.g. skip_if_link_in_bio: true)

min_followers             
      It is the lower follower bound for an account that can 
      be interacted. If an account has less followers than 
      this amount, it wont be interacted with. 
      (e.g. min_followers: 100)

max_followers             
      It is the upper follower bound for an account that can 
      be interacted. If an account has more followers than 
      this amount, it wont be interacted with. 
      (e.g. max_followers: 1000)

min_followings            
      It is the lower following bound for an account that can 
      be interacted. If an account has less followings than 
      this amount, it wont be interacted with. 
      (e.g. min_followings: 300)

max_followings            
      It is the upper following bound for an account that can 
      be interacted. If an account has more followings than 
      this amount, it wont be interacted with. 
      (e.g. max_followings: 800)

min_potency_ratio         
      If an account's followers/following ratio is not above 
      this ratio, then they will not be interacted with. 
      Combine with "max_potency_ratio" to specify a range.
      Example: username has 500 followers and 1000 
      followings. That means its ratio is 0.5 If you set your 
      "min_potency_ratio": 0.2 it will be interacted with. 
      (e.g. min_potency_ratio: 1)

max_potency_ratio         
      If an account's followers/following ratio is not below 
      this ratio, then they will not be interacted with. 
      Combine with "min_potency_ratio" to specify a range.
      Example: username has 500 followers and 1000 
      followings. That means its ratio is 0.5.
      If you set your max_potency_ratio: 0.7 it will be interacted with.
      (e.g. max_potency_ratio: 2)

follow_private_or_empty   
      If it is false, private accounts or public accounts 
      that have no posts will not be interacted with. 
      (e.g. follow_private_or_empty: false)

interact_only_private     
      If it is set to true, only private accounts will be    
      interacted with. No public accounts will be interacted 
      with.
      (e.g. interact_only_private: true)

blacklist_words
      Checks a biography for specified words. If any one word 
      is found in the bio, the user will not be interacted with.
      Otherwise the user will be interacted with. 
      (e.g. blacklist: [sex, furry, santa])

mandatory_words     
      Checks a biography for specified words. If any one word 
      is found in the bio, the user will be interacted with.
      Otherwise the user will not be interacted with. 
      (e.g. mandatory_words: [cat, kitten, meow])

specific_alphabet
      If a type is specified, the bio will be inspected and
      the primary character type will be matched against the
      one specified. If they do not match, you will not interact
      with them. This is commonly used to avoid people whose
      biographys don't match your language.
      From version 2.0 you can set more then one.
      (e.g. specific_alphabet: [LATIN, ARABIAN])

 biography_language
      As for specific_alphabet we are inspecting the biograpy
      but this time we are looking for the language itself.
      That's more powerful than the character_set but may be inconsistent if the bio is not a real text (such as a list of words without verbs). 
      In any case the bot does a best of 5 (BO5) and take the most likely language.
      for example: 'italian  and russian devops engineer ️guitarist nerd ' returns 'nl' instead of 'en' most of the time.
      55 language are supported:
      af, ar, bg, bn, ca, cs, cy, da, de, el, en, es, et, fa, fi, fr, gu, he,
      hi, hr, hu, id, it, ja, kn, ko, lt, lv, mk, ml, mr, ne, nl, no, pa, pl,
      pt, ro, ru, sk, sl, so, sq, sv, sw, ta, te, th, tl, tr, uk, ur, vi, zh-cn, zh-tw
      Look there for more info: https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
      You can also specify more then one.
      (e.g. biography_language: [it, en]

min_posts                 
      You can specify the minumum post number that an account 
      should have. 
      (e.g. min_posts: 7)
      
mutual_friends
      You can specify how many mutual friends that the target account should have to be interracted
      (e.g mutual_friends: 3)

pm_to_private_or_empty
      You can specify if you want to send PM also to private/empty accounts
      (e.g. pm_to_private_or_empty: false)
comment_hashtag_likers_top
comment_hashtag_likers_top
comment_hashtag_likers_recent
comment_hashtag_posts_top
comment_hashtag_posts_recent
comment_place_likers_top
comment_place_likers_recent
comment_place_posts_top
comment_place_posts_recent
comment_blogger_followers
comment_blogger_followings
comment_interact_usernames
comment_blogger_post_likers
comment_interact_from_file
comment_feed
      You can specify for which job you want to comment.
      Every interaction type has his own filter.
      For example if you set your comments_list.txt with 
      text that fits place posts, you don't want to say 
      something about Rome in other circumstances.
      (e.g. comment_place_likers: false)
comment_photos
comment_videos
      You can also turn on/off commenting videos or photos.
      (e.g. comment_photos: true)

min_likers
max_likers
      You can specify the range of likers that a post must have for interact with it (or its likers). 
      By default it's 1 to 1000000 likers.
      For using this feature you should activate like counts in your ig app: 
      settings -> privacy -> posts -> Hide Like and View Counts -> OFF
      It works with ..-likers-.. and ..-posts-.. jobs.
      If there isn't any number but only "an_username and others" you will interact by default
      (in this case we can't know how many likers are there)
```
*If you don't want to use a specific filter, you can comment it by putting a '#' in front of it!
For example, if you don't want to skip people by checking theit followers count your filters.yml will look like this:*
```
...
# min_followers: 50
# max_followers: 2500
min_followings: 50
max_followings: 2500
...
```
## Blacklist and whitelist
Inside the [config-example folder](https://github.com/GramAddict/bot/tree/master/config-examples) there are two important txt you should consider when you start the bot:
* **blacklist.txt**
      This file containes the usernames you don't want to interact with. Every interacting job will check this file before interacting. If someone is inside, it will get skipped.
* **whitelist.txt**
      This file is intendend for all kind of unfollow jobs. If someone is inside that list, it will not get unfollowed.

So if you want to skip someone from bot activities, these files are made for this.
Place them inside `accounts/yourusername/` and don't forget that each line should contains only an username.

Example of white/blacklist.txt:
```
mybrotherusername
myexgirlfriend
therudeguyfromschool
mybestfriend
```

## Comments
In order to comment post, you also have to set your comments_list.txt which is located inside the folder with your nickname. Every username has its own comments_list.txt file.
I've divided that file into 3 sections: %PHOTO, %VIDEO and %CAROUSEL. The reason for that is to allow you to have 3 different types of comments in relation to what you're effectively commenting. A lot of time other bots commented on my videos with "nice photo!". In this way you will be less detectable.
I also made it possibile to use emoji [look here for emoji list supported.](https://www.webfx.com/tools/emoji-cheat-sheet/).
From version 2.7.0 comments support spintax! 

For example:
```
%PHOTO
Very nice picture!
Love that photo!

%VIDEO
Incredible video!
:smile: very nice!

%CAROUSEL
I love that collection! :heart:
```
When interacting a photo, for example, you will use one (randomly) of the comments you specified in the %PHOTO section.
Ps. you can use emoji even for hashtag searches.
Pps. You can change that file even while the bot is running if you need to.

## Private message
You can send private message to people you're interacting with. You just have to set your pm_list.txt file, always in the folder with your nickname (accounts/yournickname/pm_list.txt). Every username has its own pm_list.txt file. Emoji are supported. [Look here for emoji list supported.](https://www.webfx.com/tools/emoji-cheat-sheet/)

For example:
```
Hello there! I'm bla bla consider following me! :smile:
Sorry for bothering you, can you pls take part in my survey? 
:fu:
```
A random line will be picked each time. 
Ps. You can change that file even while the bot is running if you need to.

## Spintax support
From version 2.7.0 this bot support spintax (thanks to an [external module](https://github.com/AceLewis/spintax), no needs to reinvent the wheel...)

An extract from their documentation:

Spintax (also known as spin syntax) is a way to create random strings that have the same or similar meaning.
Spintax is very useful as it can be used in programs such as chat bots or video game character speach, it allows the dialog to not sound so repetitive and robotic.

### The syntax
Spintax replaces braces (also known as curly brackets, {}) containing text with a random predefined string. The random string is defined withing the braces by using a pipe | as a seperator.

##### Simple example:

    "{Hey|Hello|Hi} this is {spin syntax|spintax}{.|!|}"

##### Can produce:
* Hey this is spintax.
* Hi this is spin syntax
* Hello this is spintax
* Hi this is spintax!

Unlike other modules, you can escape the special characters used in spintax by placing an odd number of "\\"'s before the character.

##### Example:

    r"""{Hey|Hello|Hi}{,|} this is {spin syntax|spintax}{.|!|}
    To use {this module|spintax} enclose \{your|words\} in {those brackets|braces} and use {a \||the \||a pipe (\|)} to separate them
    """

##### Can produce:

 - Hi this is spintax!

   To use spintax enclose {your|words} in braces and use the | to separate them

 - Hi, this is spin syntax

   To use this module enclose {your|words} in those brackets and use a | to separate them


 - Hello this is spintax.

   To use spintax enclose {your|words} in those brackets and use a pipe (|) to separate them

##### Example of Nested Spintax:

       "This is nested {{s|S}pintax|spin syntax}"

##### Can produce:

  - This is nested Spintax
  - This is nested spin syntax
  - This is nested spintax

## Telegram reports
From version 2.2.0 you can have telegram reports of your activity and stats directly in your telegram group. Reports will generated at the end of each session.
For accomplish that you have to:
1. set telegram-reports: true in config.yml
2. create your bot in telegram https://t.me/botfather
   * at the end of process, open the chat with it (press on <span>t.me</span>/yourbotname from botfather) and press START (or command /start)
   * save the bot api-token in your telegram.yml
   * crate a group and invite your bot inside it
3. in order to know the chat-id of your group you can use this bot https://t.me/myidbot
   * invite it in the group you created before, at this time your should be in 3 there
   * use the command /getgroupid for getting your group id (you will get something like '-123456789')
   * save the chat-id in your telegram.yml (don't forget the minus (-) in front of the chat-id!)

IMPORTANT: [telegram.yml](https://raw.githubusercontent.com/GramAddict/bot/master/config-examples/telegram.yml) (right click on the link -> save as) must be in your account folder!

Example of how telegram.yml should looks like:
```
telegram-api-token: 123456789:ABCDEFGHILMNOPQRSTUVZ-1AB2CD3
telegram-chat-id: -123456789
```

  
## Argument Glossary

Because there are some words that have special meaning to GramAddict, here is a glossary to reference back to if you run into any questions while reading about the options. 

- **Source**: The *thing* being interacted with, primarily usernames or hashtags 
- **Interaction**: Any profile that is interacted with for a particular **source** (successful or unsuccessful)
- **Successful Interaction**: Any profile that was actioned (e.g. like, follow, PM, watch stories, commented) for a particular **source**
- **Unsuccessful Interaction**: Any profile that was opened, but not actioned (e.g. like, follow, PM, watch stories, commented) for a particular **source**

- **Total Interactions**: Number of profiles with **successful interactions** or **unsuccessful interactions** across all **sources**
- **Total Successful Interactions**: Number of profiles with **successful interactions** across all **sources**
- **Other "Total" Limits**: Number of *item* done, across all **sources**

## Limit Logic

When honoring limits, the bot uses the following priority:

- **Total Interactions or Total Successful Interactions**:  If either of these are met, the current run will stop without interacting through any additional sources. If no repeat is enabled, the script will stop.
- **Total *Type* Limit**: If a total *type* limit is met, no more of that *type* will be done. If possible, the bot will continue running.
- **Individual Limits (e.g. interaction-count, unfollow, follow)**: If the limit is met, but the total limits are not met, the bot will continue on another source (if possible) or possibly continue until the other individual limits are met.

# Multiple Action Support

As of v1.1.0, GramAddict can have multiple actions specified in one command. This means you can interact with @justinbieber's followers, following 50% of them. Then afterwards, unfollow the same amount of followers. All in the same session. This allows you to use the native repeat ability instead of building a custom cron job. 

> Note: if you do the method outlined above, make sure you have a buffer of followers so you aren't unfollowing the people you just followed. Typically you want to wait at least a couple of days before you unfollow to increase the chance that people will follow you back.

When using multi-action system, the actions are executed in the order they are specified in the command. Meaning in the above sequence your command would look similar to:

```
python3 run.py --blogger-followers justinbieber --interactions-count 50 --follow-percentage 20 --unfollow 10 --repeat 200-260
```

This command would:
- Interact with 50 of @justinbieber's followers, following 20% of them (~10 follows). 
- Unfollow 10 people in order of oldest to newest. 
- The above will repeat the above steps every 200-260 minutes.

As an added note, you can also do things like interact with multiple followers and hashtags in the same run. When doing this, you want to be careful to not exceed sensible limits. To help with this, there were "Total" session limits introduced. The following total limits are available:

```
  --total-likes-limit 300
        limit on total amount of likes during the session across all
        actions, 300 by default

  --total-follows-limit 50
        limit on total amount of follows during the session across all
        actions, 50 by default

  --total-watches-limit 50
        limit on total amount of watches during the session across all
        actions, 50 by default

  --total-successful-interactions-limit 100
        when you open a profile and perform an action such as a like,
        follow, comment, PM or watch a story, this counts as a successful action

  --total-interactions-limit 1000
        every time you open a profile, it counts as an interaction, 
        even if you don't interact, 1000 by default
```

So if you wanted to interact with multiple bloggers, multiple hashtags, unfollow followers, and generate a report after - you can do a command similar to below:

```
python3 run.py --blogger-followers justinbieber selenagomez --hashtag-likers-top popmusic bestartists --interactions-count 20 --follow-percentage 20 --total-successful-interactions-limit 80 --total-interactions-limit 700 --total-likes-limit 160 --total-follows-limit 20 --unfollow 16 --analytics --repeat 200-260 --working-hours [8.07-16.33]
--time-delta 10-15
```

This command would:
- Interact with 20 each of @justinbieber's and @selenagomez's followers, following 20% of them (~4 follows each, ~8 total). The order of @justinbieber and @selenagomez will be randomized each time. 
- Interact with 20 each of likers of posts in top results of #popmusic and #bestartists, following 20% of them (~4 follows each, ~8 total). The order of #popmusic and #bestartists will be randomized each time. 
- Unfollow 16 people in order of oldest to newest. 
- Generate a PDF report for current user using the session data from previous runs.
- The above will repeat the above steps every 200-260 minutes when inside working hours.
