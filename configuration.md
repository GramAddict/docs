# Configuration File

As of v1.2.0, GramAdict supports a configuration file and **it is 100% recommended**. Let me repeat, if you use GramAddict, you should be using a configuration file. You should not be using arguments anymore. *You technically can, but we up to 63 arguments now... so it's a lot easier if you use the configuration file.*

To make it easy, to get started... we have a configuration file with every single option argument available in it. You just need to comment out any lines that you don't want to use with a `#`. You can [download that file here](https://raw.githubusercontent.com/GramAddict/bot/master/config-examples/config.yml). This file should be placed in a folder within your **GramAddict** folder, named after your username which is inside accounts main folder (if you don't create that folder, the bot will do it for you at the first run). e.g `accounts/username/config.yml` You can have multiple configuration files per user and are encouraged to do so. For example, I use one that is my normal "interaction" config and another that is a "clean up" config. e.g `accounts/username/interact.yml` and `accounts/username/unfollow.yml`.

<br/>

# Available Arguments

GramAddict can do many things and the list is constantly growing. This is a full list of the command line arguments that can be provided in order for you to get started using it.

## General Configuration

| Argument         |   Type   | Description                                                                                                                                                                                                                                             | Default                 |
| -----------------|:--------:|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------|
| username         | Required | The username for which you are running the script                                                                                                                                                                                                       | `None`                  |
| device           | Optional | Device identifier. Should be used only when multiple devices are connected at once                                                                                                                                                                      | `None`                  |
| app-id           | Optional | Allows you to specify a custom app name for cloned apps                                                                                                                                                                                                 | `com.instagram.android` |
| use-cloned-app   | Optional | if you have cloned app enabled in your device, a pop-up asking for which app to select could appear. With this parameter you can specify if use the cloned app instead of the original. (Works only on MUIU at this moment.)                             | `false`                      |
| screen-sleep     | Optional | Set to true to turn device screen off once script has finished                                                                                                                                                                                          | `false`                 |
| screen-record    | Optional | Record the screen while using the bot. This is intended only for debug purposes                                                                                                                                                                         | `false`                 |
| debug            | Optional | For troubleshooting. Debug is already sent to log file, this shows it in console                                                                                                                                                                        | `false`                 |
| speed-multiplier | Optional | You can set the speed of the bot. > 1 will increase the speed, < 1 will slow down                                                                                                                                                                       | `1`                     |
| close-apps       | Optional | Whith that you can tell the bot to close all the background apps for avoid interferences                                                                                                                                                                | `true`                  |
| disable-filters  | Optional | Instead of deleting/renaming your filter.json file, you can ignore it with that argument                                                                                                                                                                | `false`                 |
| scrape-to-file   | Optional | The bot will no longer interact anyone, but it will collect and store in a file usernames that fits your filters. That is usually done by a fake account. The generated list will be used by your main account with the argument `interact-from-file` | `false`                 |


<br />

## Actions

No particular action is required, but at least one action is required. If you specify multiple actions, the actions will be executed in the order specified or shuffled with `shuffle-jobs: true`. The logistics of multiple action support is discussed [below](#multiple-action-support) with examples.

What an "interaction" is depends on your [source limits](#source-limits), but generally the following types are supported at this time:

- Like Photos/Videos
- Follow
- Comment a post
- Send a PM
- Watch Stories

### Interaction

| Argument                | Description | Example                                              |
|-------------------------|---          |------------------------------------------------------|
| blogger-followers       | List of usernames with whose followers you want to interact. | `[username1, username2]`                             |
| blogger-following       | List of usernames with whose following you want to interact. | `[username1, username2]`                             |
| blogger-post-likers     | List of usernames with whose post likers you want to interact. | `[username1, username2]`                             |
| blogger                 | List of usernames with whose you want to interact. | `[username1, username2]`                             |
| hashtag-likers-top      | List of hashtags in top results with whose likers you want to interact. | `[hashtag1, hashtag2]`                               |
| hashtag-likers-recent   | List of hashtags in recent results with whose likers you want to interact.  | `[hashtag1, hashtag2]`                               |
| hashtag-posts-top       | List of hashtags in top results with whose posts you want to interact. | `[hashtag1, hashtag2]`                               |
| hashtag-posts-recent    | List of hashtags in recent results with whose posts you want to interact. | `[hashtag1, hashtag2]`                               |
| place-likers-top        | List of places in top results with whose likers you want to interact. | `[place1, place2]`                                   |
| place-likers-recent     | List of places in recent results with whose likers you want to interact.  | `[place1, place2]`                                   |
| place-posts-top         | List of places in top results with whose posts you want to interact. | `[place1, place2]`                                   |
| place-posts-recent      | List of places in recent results with whose posts you want to interact. | `[place1, place2]`                                   |
| interact-from-file      | Path to a text file of usernames that will be interacted with. | `[usernames_list1.txt 10-15, usernames_list2.txt] 3` |
| posts-from-file         | Path to a text file of posts that will be liked. More actions will come in the future. Useful for engagement groups. | `[posts_list1.txt, posts_list2.txt]`                 |
| delete-interacted-users | Not actually an action, but a option for `interact-from-file`, `posts-from-file` and `unfollow-from-file` to remove users/urls from file after they are interacted with | ` `                                                  |
| feed                    | Interact with your own feed. After that argument you can specify how many like you want to give. It accepts ranges | `2-5`                                                |
>Waning: from version 3.0.0 you gain control over how many users have to be processed in the `interact-from-file` job. Just specify that number after the *.txt.

### Unfollow

| Argument                    | Description | Example                                             |
|---------------------------- |---          |-----------------------------------------------------|
| unfollow                    | Unfollow at most the given number of users. Only users followed by this script will be unfollowed. | `10-20`                                             |
| unfollow-any                | Unfollow at most the given number of users. Any user is eligible to be unfollowed regardless of if this script followed them. | `10-20`                                             |
| unfollow-non-followers      | Unfollow at most the given number of users, that don't follow you back. Only users followed by this script will be unfollowed. | `10-20`                                             |
| unfollow-any-non-followers  | Unfollow at most the given number of users, that don't follow you back. Any user is eligible to be unfollowed regardless of if this script followed them. | `10-20`                                             |
| unfollow-from-file          | Unfollow usernames from a list (.txt)  | `[usernames_list1.txt 10-15, usernames_list2.txt 3]` |
| sort-followers-newest-to-oldest   | Not actually an action, but a option for all unfollow type except the one from file to sort user from newest to oldest instead that oldest to newst which is the default choice | ` `                                                 |

>Waning: from version 3.0.0 you gain control over how many users have to be processed in the `unfollow-from-file` job. Just specify that number after the *.txt.

### Post Processing

| Argument   | Description                                                        | Example  |
|------------|--------------------------------------------------------------------|----------|
| analytics  | Generates a PDF analytics report for current username session data | `true`   |


## Source Limits

| Argument            | Description                                                                                                                      | Default  |
|-------------------- |----------------------------------------------------------------------------------------------------------------------------------|----------|
| interactions-count  | Number of interactions per source in each action.                                                                                | `70`     |
| likes-count         | Number of likes for each interacted user.                                                                                        | `2`      |
| stories-count       | Number of stories for each interacted user.                                                                                      | `0`      |
| stories-percentage  | Chance of watching stories on a particular profile. Supported by plugins: hashtag-likers, hashtag-posts, blogger-followers.      | `30`     |
| carousel-count      | Number of available carousel items to browse.                                                                                    | `0`      |
| carousel-percentage | Chance of browsing a carousel.                                                                                                   | `0`      |
| max-comments-pro-user | Number of comments you can do for each user you interact.                                                                        | `0`      |
| comments-percentage | Chance of commenting an user post.                                                                                               | `0`      |
| pm-percentage       | Chance of send a private message to an user you're interacting with.                                                             | `0`      |
| interact-percentage | Chance to interact with user/hashtag when applicable. Supported by plugins: hashtag/place-posts and feed".                       | `50`     |
| follow-percentage   | Follow the given percentage of interacted users.                                                                                 | `0`      |
| follow-limit        | Limit on amount of follows per source in each action.                                                                            | `0`      |
| skipped-list-limit  | Limit how many scrolls tried, with already interacted users, until we move to next source. Does not apply for unfollows.         | `10-15`  |
| fling-when-skipped  | Fling (instead of scroll) after "X" many scrolls tried, with already interacted users. (not recommended - disabled by default)   | `0`      |
| min-following       | Minimum amount of followings, after reaching this amount unfollowing stops                                                       | `0`      |
| blogger-post-limits | Limit of blogger post which likers you are interacting (`--blogger-post-likers`) before ending job. **NOT YET DEVELOPED**        | `2`      |

<br />

## Total Limits

| Argument                            | Description                                                                                                           | Default   |
|---                                  |-----------------------------------------------------------------------------------------------------------------------|-----------|
| total-likes-limit                   | Limit on total amount of likes during the session across all sources.                                                 | `300-400` |
| total-follows-limit                 | Limit on total amount of follows during the session across all sources.                                               | `50-60`   |
| total-unfollows-limit               | Limit on total amount of unfollows during the session across all sources.                                             | `50-60`   |
| total-watches-limit                 | Limit on total amount of story watches during the session across all sources.                                         | `50-60`   |
| total-successful-interactions-limit | Limit on total amount of successful interactions during the session across all sources.                               | `100-120` |
| total-interactions-limit            | Limit on total amount of successful and non-sucessful interactions during the session across all sources.             | `1000`    |
| total-comments-limit                | Limit on total amount of comments during the session across all sources.                                              | `300-350` |
| total-pm-limit                      | Limit on total amount of private-messages during the session across all sources.                                      | `300-350` |
| total-scraped-limit                 | Limit on total amount of scraped users you will collect during the session across all sources.                        | `300-350` |
| total-crashes-limit                 | Limit on total amount of crashes during the session you are willing to accept. Reaching this limit will stop the bot. | `300-350` |

<br />

## Ending Session Conditions

| Argument                      | Description                                      | Default |
|-------------------------------|--------------------------------------------------|---------|
| end-if-likes-limit-reached    | end session when likes limit has been reached    | true    |
| end-if-follows-limit-reached  | end session when follows limit has been reached  | false   |
| end-if-watches-limit-reached  | end session when watches limit has been reached  | false   |
| end-if-comments-limit-reached | end session when comments limit has been reached | false   |
| end-if-pm-limit-reached       | end session when pm limit has been reached       | false   |


## Special modifier for jobs and sources

| Argument | Description | Example |
|---       |---          |---      |
| shuffle-jobs                  | Instead of follow the order of the jobs you write, that argument will allow the bot to shuffle the jobs | `300` |
| truncate-sources              | If you have a lot of sources, with this argument you're able to pick n random from the list and interact only with them, for that session | `2-3` |
| watch-video-time       | Instead of liking video without watching them, you can fake it and pause the bot for a given time (in seconds). Set to 0 to disable it. | `15-35` |

<br />

## Scheduling

| Argument        | Description                                                                                                                                                                                                                     | Example                      |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|
| repeat          | Repeat the same session again after N minutes after completion, disabled by default.                                                                                                                                            | `120-180`                    |
| working-hours   | Scheduler for bot activity. You can specify the interval (one or more) of time in which you want the bot to run. You must use the time notation 0-24. | `[10.15-16.40, 18.15-22.46]` |
| time-delta      | This is intended to be used with `working-hours` and allows to change the start and the end point of each interval. A random value, positive or negative, will be generated.                                                    | `10-15`                      |
| total-sessions  | You can specify how many session do. When the bot reached the specified number of sessions, it stops. You can set -1 or comment this line for infinite sessions.                                                                | `5`                           |

>**Warning**: if you want to use `working-hours` feature, you **MUST** specify a `repeat` value!

<br />

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

    You can also turn on/off commenting videos, photos and caroulsels.

- **pm_to_private_or_empty: false**

    You can specify if you want to send PM also to private/empty accounts

- **min_likers: 1** 
- **max_likers: 250**

    You can specify the span of likers a post must have to be interacted with.

<br />

## Comments
In order to comment post, you have also to set your comments_list.txt which is located inside the folder with your nickname. Every username has his own comments_list.txt file.
I've dived that file in 3 sections: %PHOTO, %VIDEO and %CAROUSEL. The reason of that is for allow you to have 3 different type of comment in relation of what you're effectively commenting. A lot of time other bots commented on my videos with "nice photo!". In this way you will be less detectable.
I also made possible to use emoji [look here for emoji list supported](https://www.webfx.com/tools/emoji-cheat-sheet/).

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
When interacting a photo, for example, you will use one (randomly) of the comments you specified in the `%PHOTO` section.
Ps. you can use emoji even for hashtag searches.
Pps. You can change that file even while the bot is running if you need to.

## Private message
You can send private message to people you're interacting with. You just have to set your pm_list.txt file, always in the folder with your nickname (accounts/yournickname/pm_list.txt). Every username has his own pm_list.txt file. Emoji are supported. [look here for emoji list supported](https://www.webfx.com/tools/emoji-cheat-sheet/)

For example:
```
Hello there! I'm bla bla consider follow me! :smile:
Sorry for bothering you, can you pls take part of my survey? 
:fu:
```
A random line will be picked each time. 
Ps. You can change that file even while the bot is running if you need to.

### Argument Glossary

Because there are some words that have special meaning to GramAddict, here is a glossary to reference back to if you run into any questions while reading about the options. 

- **Source**: The *thing* being interacted with, primarily usernames or hashtags 
- **Interaction**: Any profile that is interacted with for a particular **source** (successful or unsuccessful)
- **Successful Interaction**: Any profile that was actioned (e.g. like or follow) for a particular **source**
- **Unsuccessful Interaction**: Any profile that was opened, but not actioned (e.g. like or follow) for a particular **source**

- **Total Interactions**: Number of profiles with **successful interactions** or **unsuccessful interactions** across all **sources**
- **Total Successful Interactions**: Number of profiles with **successful interactions** with across all **sources**
- **Other "Total" Limits**: Number of *item* done, across all **sources**

## Limit Logic

You can specify which are the limits that makes the bot stop his activity.
Only two limits can't be changed: the `total-successful-interactions-limit` and `total-interactions-limit`. When the bot reach them, it will stop. No matter what.
Refer to [this section](##ending-session-conditions) to learn about ending conditions.

# Multiple Action Support

As of v1.1.0, GramAddict can have multiple actions specified in one command. This means you can interact with @justinbieber's followers, following 50% of them. Then afterwards, unfollow the same amount of followers. All in the same session. This allows you to use the native repeat ability instead of building a custom cron job. 

> Note: if you do the method outlined above, make sure you have a buffer of followers so you aren't unfollowing the people you just followed. Typically you want to wait at least a couple days before you unfollow to increase the chance people will follow you back.

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
        limit on total amount of likes during the session across all
        actions, 50 by default

  --total-watches-limit 50
        limit on total amount of likes during the session across all
        actions, 50 by default

  --total-successful-interactions-limit 100
        limit on total amount of likes during the session across all
        actions, 100 by default

  --total-interactions-limit 1000
        limit on total amount of likes during the session across all
        actions, 1000 by default
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
