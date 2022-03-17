# Configuration File

As of v1.2.0, GramAdict supports a configuration file and **it is 100% recommended**. Let me repeat, if you use GramAddict, you should be using a configuration file. You should not be using arguments anymore. *You technically can, but we have up to 66 arguments now... so it's a lot easier if you use the configuration file.*

To make it easy, to get started... we have a configuration file with every single option argument available in it. You just need to comment out any lines that you don't want to use with a `#`. You can [download that file here](https://raw.githubusercontent.com/GramAddict/bot/master/config-examples/config.yml) (right-click on the link -> save as). This file should be placed in a folder within your **GramAddict** folder, named after your username which is inside accounts main folder (if you don't create that folder, the bot will do it for you on the first run). e.g. `accounts/username/config.yml` You can have multiple configuration files per user and are encouraged to do so. For example, I use one that is my normal "interaction" config and another that is a "clean up" config. e.g. `accounts/username/interact.yml` and `accounts/username/unfollow.yml`.

<br/>

# Available Arguments

GramAddict can do many things and the list is constantly growing. This is a full list of the command line arguments that can be provided in order for you to get started using it.

## General Configuration

| Argument                 |   Type   | Description                                                                                                                                                                                                                                                       | Default                 |
|--------------------------|:--------:|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| username                 | Required | The username for which you are running the script                                                                                                                                                                                                                 | `None`                  |
| device                   | Optional | Device identifier. Specifies which device should be used for the profile from `adb devices`. Use this argument only if you have multiple devices connected at the same time.                                                                                      | `None`                  |
| app-id                   | Optional | Allows you to specify a custom app name for cloned apps                                                                                                                                                                                                           | `com.instagram.android` |
| use-cloned-app           | Optional | if you have cloned app enabled in your device, a pop-up asking for which app to select could appear. With this parameter you can specify if use the cloned app instead of the original. (Works only on MUIU at this moment.)                                      | `false`                 |
| screen-sleep             | Optional | Set to true to turn device screen off once script has finished                                                                                                                                                                                                    | `false`                 |
| screen-record            | Optional | Record the screen while using the bot. This is intended only for debug purposes                                                                                                                                                                                   | `false`                 |
| debug                    | Optional | For troubleshooting. Debug is already sent to log file, this shows it in console                                                                                                                                                                                  | `false`                 |
| speed-multiplier         | Optional | You can set the speed of the bot. > 1 will increase the speed, < 1 will slow down. It can also be a fraction: for example 1.3                                                                                                                                     | `1`                     |
| close-apps               | Optional | With this you can tell the bot to close all the background apps to avoid interferences                                                                                                                                                                            | `true`                  |
| disable-filters          | Optional | Instead of deleting/renaming your filter.yml file, you can ignore it with this argument                                                                                                                                                                           | `false`                 |
| disable-block-detection  | Optional | You can disable the detection of action block by putting this parameter to `true`                                                                                                                                                                                 | `false`                 |
| dont-type                | Optional | Instead of typing, the bot will paste text                                                                                                                                                                                                                        | `false`                 |
| scrape-to-file           | Optional | The bot will no longer interact with anyone, but it will collect and store all the usernames that fit your filters in a file. This is usually done by a fake account. The generated list will be used by your main account with the argument `interact-from-file` | `false`                 |
| total-crashes-limit      | Optional | Limit on total amount of crashes during the session you are willing to accept. Reaching this limit will stop the bot.                                                                                                                                             | `5`                     |
| count-app-crashes        | Optional | You can tell the bot to count app crashes as a crash for `total-crashes-limit`                                                                                                                                                                                    | `false`                 |
| shuffle-jobs             | Optional | Instead of following the order of the jobs you write, this argument will allow the bot to shuffle the jobs.                                                                                                                                                       | `false`                 |
| truncate-sources         | Optional | If you have a lot of sources, with this argument you're able to pick n random from the list and interact only with them, for that session.                                                                                                                        | `0`                     |

> Attention: the speed-multiplier has a [low limit](https://github.com/GramAddict/bot/blob/54ea82775a68956058c9bc3194a2772219d0892b/GramAddict/core/utils.py#L453) for the sleep time! 
> That means that if you put 100 or 100000 it will go at the same speed. It was introduced in order not to crash the bot.

<br />

## Actions

No particular action is required, but at least one action is required. If you specify multiple actions, the actions will be executed in the order specified or shuffled with `shuffle-jobs: true`. The logistics of multiple action support is discussed [below](#multiple-action-support) with examples.

What an "interaction" is depends on your [source limits](#source-limits), but generally the following types are supported at this time:

- Like Photos/Videos
- Follow
- Comment a post
- Send a PM
- Watch and like Stories

### Interaction (active Jobs)

| Argument                   | Description                                                                                                          | Example                                              |
|----------------------------|----------------------------------------------------------------------------------------------------------------------|------------------------------------------------------|
| blogger-followers          | List of usernames with whose followers you want to interact.                                                         | `[username1, username2]`                             |
| blogger-following          | List of usernames with whose following you want to interact.                                                         | `[username1, username2]`                             |
| blogger-post-likers        | List of usernames with whose post likers you want to interact.                                                       | `[username1, username2]`                             |
| blogger                    | List of usernames with whom you want to interact.                                                                    | `[username1, username2]`                             |
| hashtag-likers-top         | List of hashtags in top results with whose likers you want to interact.                                              | `[hashtag1, hashtag2]`                               |
| hashtag-likers-recent      | List of hashtags in recent results with whose likers you want to interact.                                           | `[hashtag1, hashtag2]`                               |
| hashtag-posts-top          | List of hashtags in top results with whose posts you want to interact.                                               | `[hashtag1, hashtag2]`                               |
| hashtag-posts-recent       | List of hashtags in recent results with whose posts you want to interact.                                            | `[hashtag1, hashtag2]`                               |
| place-likers-top           | List of places in top results with whose likers you want to interact.                                                | `[place1, place2]`                                   |
| place-likers-recent        | List of places in recent results with whose likers you want to interact.                                             | `[place1, place2]`                                   |
| place-posts-top            | List of places in top results with whose posts you want to interact.                                                 | `[place1, place2]`                                   |
| place-posts-recent         | List of places in recent results with whose posts you want to interact.                                              | `[place1, place2]`                                   |
| interact-from-file         | Path to a text file of usernames that will be interacted with.                                                       | `[usernames_list1.txt 10-15, usernames_list2.txt 3]` |
| posts-from-file            | Path to a text file of posts that will be liked. More actions will come in the future. Useful for engagement groups. | `[posts_list1.txt, posts_list2.txt]`                 |
| feed                       | Interact with your own feed. After that argument you can specify how many likes you want to give. It accepts ranges. | `2-5`                                                |

>Waning: from version 3.0.0 you gain control over how many users have to be processed in the `interact-from-file` job. Just specify that number after the *.txt.

#### Modifier for Interaction jobs (active Jobs)
 Argument                           | Description                                                                                                                                                    | Example    |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| watch-video-time                  | Instead of liking videos without watching them, you can fake it and pause the bot for a given time (in seconds). Set to 0 to disable it.                       | `15-35`    |
| watch-photo-time                  | Instead of liking photos without looking them, you can fake it and pause the bot for a given time (in seconds). Set to 0 to disable it.                        | `3-4`      |
| can-reinteract-after              | With that feature you can re-interact someone who has already interacted. You have to specify the amount of hours that have to pass from the last interaction. 
| delete-interacted-users           | An option for jobs that involves a *.txt to remove users/urls from it after they have been interacted with.                                                    | `true`     |
<br />

### Unfollow

| Argument                        | Description                                                                                                                                                                       | Example                                              |
|---------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------|
| unfollow                        | Unfollow at most the given number of users. Only users followed by this script will be unfollowed.                                                                                | `10-20`                                              |
| unfollow-any                    | Unfollow at most the given number of users. Any user is eligible to be unfollowed regardless of if this script followed them.                                                     | `10-20`                                              |
| unfollow-non-followers          | Unfollow at most the given number of users, that don't follow you back. Only users followed by this script will be unfollowed.                                                    | `10-20`                                              |
| unfollow-any-non-followers      | Unfollow at most the given number of users, that don't follow you back. Any user is eligible to be unfollowed regardless of if this script followed them.                         | `10-20`                                              |
| unfollow-any-followers          | Unfollow at most the given number of users, that follow you back. Any user is eligible to be unfollowed regardless of if this script followed them.                               | `10-20`                                              |
| unfollow-from-file              | Unfollow usernames from a list (.txt)                                                                                                                                             | `[usernames_list1.txt 10-15, usernames_list2.txt 3]` |

>Waning: from version 3.0.0 you gain control over how many users have to be processed in the `unfollow-from-file` job. Just specify that number after the *.txt.

#### Modifier for Unfollow jobs
 Argument                           | Description                                                                                                                                                  | Example      |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|
| sort-followers-newest-to-oldest   | An option for all unfollow types except the one from file to sort users from newest to oldest instead of oldest to newest which is the default choice        | ` false `    |                                                                                                                                                                                 |                                                      |
| unfollow-by-date                  | With this option you can specify the number of days that have to have passed since the last interaction it work with `unfollow` and `unfollow-non-followers` | `10-20`      |
<br />

### Remove followers
| Argument                   | Description                                                                     | Example                                        |
|----------------------------|---------------------------------------------------------------------------------|------------------------------------------------|
| remove-followers-from-file | Path to a text file of usernames that are following you and you want to remove. | `[remove_list1.txt 10-15, remove_list2.txt 3]` |

#### Modifier for Remove followers

| Argument                          | Description                                    | Example   |
|-----------------------------------|------------------------------------------------|-----------|
| delete-removed-follower-from-file | Remove from the *.txt the removed follower.    | `true`    |

### Post Processing

| Argument         | Description                                                                                                                                                                                                                                                                                                                                                  | Default        |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|
| analytics        | Generates a PDF analytics report for current username session data. For using this feature you have to install the dependencies: `pip3 install gramaddict[analytics]`                                                                                                                                                                                        | `false`        |
| telegram-reports | Generates a report for current username session data and send it to your telegram channel. <br /> For using this feature you have first to configure the file `telegram.yml` in your account folder. <br /> [Instructions here](#telegram-reports). For using this feature you have to install the dependencies: `pip3 install gramaddict[telegram-reports]` | `true`         |

<br />

## Source Limits

| Argument              | Description                                                                                                                    | Default |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------|---------|
| interactions-count    | Number of interactions per source in each action.                                                                              | `70`    |
| likes-count           | Number of likes for each interacted user.                                                                                      | `2`     |
| likes-percentage      | Chance of liking posts on a particular profile.                                                                                | `100`   |
| stories-count         | Number of stories for each interacted user.                                                                                    | `0`     |
| stories-percentage    | Chance of watching stories on a particular profile. Supported by plugins: hashtag-likers, hashtag-posts, blogger-followers.    | `30`    |
| carousel-count        | Number of available carousel items to browse.                                                                                  | `0`     |
| carousel-percentage   | Chance of browsing a carousel.                                                                                                 | `0`     |
| max-comments-pro-user | Number of comments you can do for each user you interact.                                                                      | `0`     |
| comments-percentage   | Chance of commenting on a user post.                                                                                           | `0`     |
| pm-percentage         | Chance of sending a private message to a user you're interacting with.                                                         | `0`     |
| interact-percentage   | Chance to interact with user/hashtag when applicable. Supported by plugins: hashtag/place-posts and feed".                     | `50`    |
| follow-percentage     | Follow the given percentage of interacted users.                                                                               | `0`     |
| follow-limit          | Limit on amount of follows per source in each action.                                                                          | `0`     |
| skipped-list-limit    | Limit how many scrolls tried, with already interacted users, until we move to the next source. Does not apply for unfollows.   | `10-15` |
| skipped-post-limit    | Control how many skips in jobs with posts (e.g.: hashtag-post-top) are allowed before moving to another source / job           | `5`     |
| fling-when-skipped    | Fling (instead of scroll) after "X" many scrolls tried, with already interacted users. (not recommended - disabled by default) | `0`     |
| min-following         | Minimum amount of followings, after reaching this amount unfollowing stops                                                     | `0`     |
| blogger-post-limits   | Limit of blogger post which likers you are interacting (`blogger-post-likers`) before ending job. **NOT YET DEVELOPED**        | `2`     |


<br />

## Total Limits

| Argument                              | Description                                                                                                           | Default   |
|---------------------------------------|-----------------------------------------------------------------------------------------------------------------------|-----------|
| total-likes-limit                     | Limit on total amount of likes during the session across all sources.                                                 | `300`     |
| total-follows-limit                   | Limit on total amount of follows during the session across all sources.                                               | `50`      |
| total-unfollows-limit                 | Limit on total amount of unfollows during the session across all sources.                                             | `50`      |
| total-watches-limit                   | Limit on total amount of story watches during the session across all sources.                                         | `50`      |
| total-successful-interactions-limit   | Limit on total amount of successful interactions during the session across all sources.                               | `100`     |
| total-interactions-limit              | Limit on total amount of successful and non-successful interactions during the session across all sources.            | `1000`    |
| total-comments-limit                  | Limit on total amount of comments during the session across all sources.                                              | `300`     |
| total-pm-limit                        | Limit on total amount of private-messages during the session across all sources.                                      | `300`     |
| total-scraped-limit                   | Limit on total amount of scraped users you will collect during the session across all sources.                        | `300`     |

>Suggestion: you can pass ranges as argument. For example `total-likes-limit: 300-400` will take a random number between 300 and 400.

<br />

### What's the difference between total-interactions-limit and total-successful-interactions-limit?
- total-interactions-limit
>every time you open a profile, it counts as an interaction, even if you don't interact

- total-successful-interactions-limit
>when you open a profile and perform an action such as a like, follow, comment, PM or watch a story, this counts as a successful interaction



## Special actions

| Argument      | Description                                          | Example                         |
|---------------|------------------------------------------------------|---------------------------------|
| pre-script    | Specify the pre script file path to be executed.     | `pre_file.bat`, `pre_file.sh`   |
| post-script   | Specify the post script file path to be executed.    | `post_file.bat`, `post_file.sh` |
<br />

## Ending Session Conditions

| Argument                      | Description                                               | Example   |
|-------------------------------|-----------------------------------------------------------|-----------|
| end-if-likes-limit-reached    | the session will end when likes limit has been reached    | `true`    |
| end-if-follows-limit-reached  | the session will end when follows limit has been reached  | `false`   |
| end-if-watches-limit-reached  | the session will end when watches limit has been reached  | `false`   |
| end-if-comments-limit-reached | the session will end when comments limit has been reached | `false`   |
| end-if-pm-limit-reached       | the session will end when pm limit has been reached       | `false`   |
> ATTENTION: session will end in any case if `total-successful-interactions-limit` or `total-interactions-limit` have been reached!
<br />

## Scheduling

| Argument       | Description                                                                                                                                                                                                                       | Example                      |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|
| repeat         | Repeat the same session again after N minutes after completion, disabled by default.                                                                                                                                              | `120-180`                    |
| working-hours  | Scheduler for bot activity. You can specify the interval (one or more) of time in which you want the bot to run. You must use the time notation 0-24. You can use with the above argument `repeat` to have a never stop bot.      | `[10.15-16.40, 18.15-22.46]` |
| time-delta     | This is intended to be used with `working-hours` and allows to change the start and the end point of each interval. A random value, positive or negative, will be generated. Math example: `bot-will-run-at = working-hours ± ΔT` | `10-15`                      |
| total-sessions | You can specify how many sessions you want to perform before the bot stops. By default it's infinite sessions. It works only if `repeat` argument is provided.                                                                    | `3-4`                        | 

## Available Filters

We know that you want to make sure that you only interact with a specific set of users. When you leave it up to a bot, you never know what will happen. We try to make this easier for you by giving you a wide subset of filters to help weed out the undesirables. The full list is below. This guide refers to the file `filters.yml`, just edit it to accomplish what you need.


### Filters on profile type
- **skip_if_private: false**

    If it is set to true, private accounts will not be interacted with.

- **skip_if_public: false**

    If it is set to true, public accounts will not be interacted with.

- **skip_business: true**

    If it is true, business accounts won't be interacted.

- **skip_non_business: true**

    If it is true, private accounts and public accounts won't be interacted.
  
- **skip_following: true**
  
    If it is true, accounts that you follow won't be interacted with.
        
- **skip_following: true**

    If it is true, accounts that follow you won't be interacted with. Note, if you follow someone, the filter won't be able  to tell if that person follows you.
  
- **skip_if_link_in_bio: true**

    Skip the profile if it has a link in bio.
              
- **follow_private_or_empty: false**

    If it is false, private accounts or public accounts that have no posts will not be interacted with.

### Filters on profile stats
- **min_followers: 100**

    It is the lower follower bound for an account that can be interacted. If an account has fewer followers than this amount, it won't be interacted. 

- **max_followers: 1000**

    It is the upper follower bound for an account that can be interacted. If an account has more followers than this amount, it won't be interacted.

- **min_followings: 300**

    It is the lower following bound for an account that can be interacted. If an account has fewer followings than this amount, it won't be interacted.
  
- **max_followings: 800**

    It is the upper following bound for an account that can be interacted. If an account has more followings than this amount, it won't be interacted.

- **min_potency_ratio: 1**

    If an account's followers/following ratio is not above this ratio, then they will not be interacted with. Combine with `max_potency_ratio` to specify a range. 

    Example: username has 500 followers and 1000 followings. That means its ratio is 0.5 If you set your `min_potency_ratio: 0.2` it will be interacted with.

- **max_potency_ratio: 2**

    If an account's followers/following ratio is not below this ratio, then they will not be interacted with. Combine with `min_potency_ratio` to specify a range.

    Example: username has 500 followers and 1000 followings. That means its ratio is 0.5 If you set your `max_potency_ratio: 0.7` it will be interacted with.

- **min_posts: 7**

    You can specify the minimum post number that an account should have.

- **mutual_friends: 5**

    With that filter you can interact with a profile only if it has at least n mutual friends with your account `mutual_friends: -1` # -1 for ignore that filter)
                             
### Filters on biography and name
- **blacklist: ["sex", "furry"]**

    Checks a biography for specified words. If anyone words is found in the bio, the user will not be interacted with. Otherwise, the user will be interacted with.
       
- **mandatory_words: ["cat", "kitten", "meow"]**

    Checks a biography for specified words. If anyone words is found in the bio, the user will be interacted with. Otherwise, the user will not be interacted with.
        
- **specific_alphabet: ["LATIN", "ARABIAN"]**

    If a type is specified, the bio will be inspected and the primary character type will be matched against the one specified. If they do not match, you will not interact with them. This is commonly used to avoid people whose biography's don't match your language.

    From version 2.0 you can set more than one.

- **biography_language: [it, en]**

    Check the language of the biography, if it matches the list you are likely to interact.
        
- **biography_banned_language: [es, ch]**

    Check the language of the biography, if it matches the list you will skip that account.
### Filters for enabling comments
#### Action specific   
- **comment_hashtag_likers_top: false**
- **comment_hashtag_likers_top: false**
- **comment_hashtag_likers_recent: false**
- **comment_hashtag_posts_top: false**
- **comment_hashtag_posts_recent: false**
- **comment_place_likers_top: false**
- **comment_place_likers_recent: false**
- **comment_place_posts_top: false**
- **comment_place_posts_recent: false**
- **comment_blogger_followers: false**
- **comment_blogger_followings: false**
- **comment_interact_usernames: false**
- **comment_blogger_post_likers: false**
- **comment_interact_from_file: false**
- **comment_feed: false**

    You can specify for which job you want to comment. Every interaction type has his own filter.

    For example if you set your `comments_list.txt` with text that fits place posts, you don't want to say something about Rome in other circumstances.
        
#### Content specific
- **comment_photos: true**
- **comment_videos: true**
- **comment_carousels: true**

    You can also turn on/off commenting videos, photos and carousels.

- **pm_to_private_or_empty: false**

    You can specify if you want to send PM also to private/empty accounts

- **min_likers: 1** 
- **max_likers: 250**

    You can specify the span of likers a post must have to be interacted with.

>If you don't want to use a specific filter, you can comment it by putting a '#' in front of it!
For example, if you don't want to skip people by checking their followers count your filters.yml will look like this:
```
...
# min_followers: 50
# max_followers: 2500
min_followings: 50
max_followings: 2500
...
```

## Possible errors in your config.yml and filters.yml:
- `found character '\t' that cannot start any token in "accounts/your-username/{config.yml|filters.yml}", line xx, column xx` means that in that line you have a TAB, rewrite that line to fix it
- you wrote a parameter more than 1 time, in that case, the last entry will be used

## Blacklist and whitelist
Inside the [config-example folder](https://github.com/GramAddict/bot/tree/master/config-examples) there are two important txt you should consider when you start the bot:
* **blacklist.txt**
      This file contains the usernames you don't want to interact with. Every interacting job will check this file before interacting. If someone is inside, it will get skipped.
* **whitelist.txt**
      This file is intended for all kind of unfollow jobs. If someone is inside that list, it will not get unfollowed.

So if you want to skip someone from bot activities, these files are made for this.
Place them inside `accounts/yourusername/` and don't forget that each line should contain only a username.

Example of white/blacklist.txt:
```
mybrotherusername
myexgirlfriend
therudeguyfromschool
mybestfriend
```
> These lists are hot reloaded everytime we look into!

## Comments
In order to comment post, you also have to set your comments_list.txt which is located inside the folder with your nickname. Every username has its own comments_list.txt file.
I've divided that file into 3 sections: %PHOTO, %VIDEO and %CAROUSEL. The reason for that is to allow you to have 3 different types of comments in relation to what you're effectively commenting. A lot of time other bots commented on my videos with "nice photo!". In this way you will be less detectable.
I also made it possible to use emoji [look here for emoji list supported.](https://www.webfx.com/tools/emoji-cheat-sheet/)
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

> That list is hot reloaded everytime we look into!

## Private message
You can send private message to people you're interacting with. You just have to set your pm_list.txt file, always in the folder with your nickname (accounts/yournickname/pm_list.txt). Every username has its own pm_list.txt file. Emoji are supported. [Look here for emoji list supported.](https://www.webfx.com/tools/emoji-cheat-sheet/)
In PM, you can go next line by placing a `\n` in the text. Look at the 3rd line of the example.

For example:
```
Hello there! I'm bla bla consider following me! :smile:
Sorry for bothering you, can you pls take part in my survey? 
Hello!\nThanks for following me back!\nWhere are you from?
:fu:
```
A random line will be picked each time. 

> That list is hot reloaded everytime we look into!

## Spintax support
From version 2.7.0 this bot support spintax (thanks to an [external module](https://github.com/AceLewis/spintax), no needs to reinvent the wheel...)

An extract from their documentation:

Spintax (also known as spin syntax) is a way to create random strings that have the same or similar meaning.
Spintax is very useful as it can be used in programs such as chatbots or video game character speach, it allows the dialog to not sound so repetitive and robotic.

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

   To use this module encloses {your|words} in those brackets and use a | to separate them


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
   * invite it in the group you created before, at this time you should be in 3 there
   * use the command /getgroupid for getting your group id (you will get something like '-123456789')
   * save the chat-id in your telegram.yml (don't forget the minus (-) in front of the chat-id!)

IMPORTANT: [telegram.yml](https://raw.githubusercontent.com/GramAddict/bot/master/config-examples/telegram.yml) (if you don't have it right-click on the link -> save as) must be in your account folder!

Example of how telegram.yml should look like:
```
telegram-api-token: 123456789:ABCDEFGHILMNOPQRSTUVZ-1AB2CD3
telegram-chat-id: -123456789
```
If you get errors sending the report, please refer to this: https://core.telegram.org/api/errors
  
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

When honoring limits, the bot refers to the [ending conditions](#ending-session-conditions).

- **Total Interactions or Total Successful Interactions**:  If either of these are met, the current run will stop without interacting through any additional sources. If no repeat is enabled, the script will stop.
- **Total *Type* Limit**: If a total *type* limit is met, no more of that *type* will be done. If possible, the bot will continue running.
- **Individual Limits (e.g. interaction-count, unfollow, follow)**: If the limit is met, but the total limits are not met, the bot will continue on another source (if possible) or possibly continue until the other individual limits are met.