# Configuration File

As of v1.2.0, GramAdict supports a configuration file and **it is 100% recommended**. Let me repeat, if you use GramAddict, you should be using a configuration file. You should not be using arguments anymore. *You technically can, but we up to 63 arguments now... so it's a lot easier if you use the configuration file.*

To make it easy, to get started... we have a configuration file with every single option argument available in it. You just need to comment out any lines that you don't want to use with a `#`. You can [download that file here](https://raw.githubusercontent.com/GramAddict/bot/master/config-examples/all-parameters.yml). This file should be placed in a folder within your **GramAddict** folder, named after your username. e.g `username/config.yml` You can have multiple configuration files per user and are encouraged to do so. For example, I use one that is my normal "interaction" config and another that is a "clean up" config. e.g `username/interact.yml` and `username/unfollow.yml`.

<br/>

# Available Arguments

GramAddict can do many things and the list is constantly growing. This is a full list of the command line arguments that can be provided in order for you to get started using it.

## General Configuration

| Argument         | Type     | Description | Default |
| -----------------| :------: | ---         |---      |
| username         | Required | The username for which you are running the script | `None` |
| device           | Optional | Device identifier. Should be used only when multiple devices are connected at once | `None` |
| app-id           | Optional | Allows you to specify a custom app name for cloned apps | `com.instagram.android` |
| screen-sleep     | Optional | Turns on the phone screen when the script is running and off when when it's ended or sleeping | `False` |
| screen-record    | Optional | Record the screen while using the bot. This is intended only for debug purposes | `False` |
| debug            | Optional | For troubleshooting. Debug is already sent to log file, this shows it in console | `False` |
| speed-multiplier | Optional | You can set the speed of the bot. > 1 will increase the speed, < 1 will slow down | `1` |
| close-apps       | Optional | Whith that you can tell the bot to close all the background apps for avoid interferences | `true` |
| disable-filters  | Optional | Instead of deleting/renaming your filter.json file, you can ignore it with that argument | `false` |
| scrape-to-file   | Optional | The bot will no longer interact anyone, but it will collect and store in a file usernames that fits your filters. That is usually done by a fake account. The generated list will be used by your main account with the argument `--interact-from-file`  | `false` |


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
| blogger-post-likers       | List of usernames with whose post likers you want to interact. | `[username1, username2 ]` |
| blogger                   | List of usernames with whose you want to interact. | `[username1, username2]` |
| hashtag-likers-top        | List of hashtags in top results with whose likers you want to interact. | `[hashtag1, hashtag2]` |
| hashtag-likers-recent     | List of hashtags in recent results with whose likers you want to interact.  | `[hashtag1, hashtag2]` |
| hashtag-posts-top         | List of hashtags in top results with whose posts you want to interact. | `[hashtag1, hashtag2]` |
| hashtag-posts-recent      | List of hashtags in recent results with whose posts you want to interact. | `[hashtag1, hashtag2]` |
| place-likers-top          | List of places in top results with whose likers you want to interact. | `[place1, place2]` |
| place-likers-recent       | List of places in recent results with whose likers you want to interact.  | `[place1, place2]` |
| place-posts-top           | List of places in top results with whose posts you want to interact. | `[place1, place2]` |
| place-posts-recent        | List of places in recent results with whose posts you want to interact. | `[place1, place2]` |
| interact-from-file        | Path to a text file of usernames that will be interacted with. | `[usernames_list1.txt, usernames_list2.txt]` |
| posts-from-file           | Path to a text file of posts that will be liked. More actions will come in the future. Useful for engagement groups. | `[posts_list1.txt, posts_list2.txt`] |
| delete-interacted-users   | Not actually an action, but a option for `interact-from-file` and `posts-from-file` to remove users/urls from file after they are interacted with | ` ` |

<br />

### Unfollow

| Argument                    | Description | Example |
|---------------------------- |---          |---      |
| unfollow                    | Unfollow at most the given number of users. Only users followed by this script will be unfollowed. | `10-20` |
| unfollow-any                | Unfollow at most the given number of users. Any user is eligible to be unfollowed regardless of if this script followed them. | `10-20` |
| unfollow-non-followers      | Unfollow at most the given number of users, that don't follow you back. Only users followed by this script will be unfollowed. | `10-20` |
| unfollow-any-non-followers  | Unfollow at most the given number of users, that don't follow you back. Any user is eligible to be unfollowed regardless of if this script followed them. | `10-20` |
| unfollow-from-file          | Unfollow usernames from a list (.txt)  | `[usernames_list1.txt, usernames_list2.txt]` |
| sort-followers-newest-to-oldest   | Not actually an action, but a option for all unfollow type except the one from file to sort user from newest to oldest instead that oldest to newst which is the default choice | ` ` |

<br />

### Post Processing

| Argument      | Description                 | Example |
|-------        |------------------           |---------      |
| analytics | Generates a PDF analytics report for current username session data | `options` |

<br />

## Source Limits

| Argument            | Description | Default |
|-------------------- |---          |---      |
| interactions-count  | Number of interactions per source in each action. | `70` |
| likes-count         | Number of likes for each interacted user. | `2` |
| stories-count       | Number of stories for each interacted user. | `0` |
| stories-percentage  | Chance of watching stories on a particular profile. Supported by plugins: hashtag-likers, hashtag-posts, blogger-followers. | `30` |
| carousel-count      | Number of available carousel items to browse. | `0` |
| carousel-percentage | Chance of browsing a carousel. | `0` |
| max-comments-pro-user | Number of comments you can do for each user you interact. | `0` |
| comments-percentage | Chance of commenting an user post. | `0` |
| pm-percentage       | Chance of send a private message to an user you're interacting with. | `0` |
| interact-percentage | Chance to interact with user/hashtag when applicable. Supported by plugins: hashtag-posts". | `50` |
| follow-percentage   | Follow the given percentage of interacted users. | `0` |
| follow-limit        | Limit on amount of follows per source in each action. | `0` |
| skipped-list-limit  | Limit how many scrolls tried, with already interacted users, until we move to next source. Does not apply for unfollows. | `10-15` |
| fling-when-skipped  | Fling (instead of scroll) after "X" many scrolls tried, with already interacted users. (not recommended - disabled by default) | `0` |
| min-following       | Minimum amount of followings, after reaching this amount unfollowing stops | `0` |
| blogger-post-limits | Limit of blogger post which likers you are interacting (`--blogger-post-likers`) before ending job. | `2` |


<br />

## Total Limits

| Argument                            | Description | Default |
|---                                  |---          |---      |
| total-likes-limit                   | Limit on total amount of likes during the session across all sources. | `300` |
| total-follows-limit                 | Limit on total amount of follows during the session across all sources. | `50` |
| total-watches-limit                 | Limit on total amount of story watches during the session across all sources. | `50` |
| total-successful-interactions-limit | Limit on total amount of successful interactions during the session across all sources. | `100` |
| total-interactions-limit            | Limit on total amount of successful and non-sucessful interactions during the session across all sources. | `1000` |
| total-comments-limit                | Limit on total amount of comments during the session across all sources. | `300` |
| total-pm-limit                      | Limit on total amount of private-messages during the session across all sources. | `300` |
| total-scraped-limit                 | Limit on total amount of scraped users you will collect during the session across all sources. | `300` |
| total-crashes-limit                 | Limit on total amount of crashes during the session you are willing to accept. Reaching this limit will stop the bot. | `300` |

<br />

## Special modificators for jobs and sources

| Argument | Description | Example |
|---       |---          |---      |
| shuffle-jobs                  | Instead of follow the order of the jobs you write, that argument will allow the bot to shuffle the jobs | `300` |
| truncate-sources              | If you have a lot of sources, with this argument you're able to pick n random from the list and interact only with them, for that session | `2-3` |
| watch-video-time       | Instead of liking video without watching them, you can fake it and pause the bot for a given time (in seconds). Set to 0 to disable it. | `15-35` |

<br />

## Scheduling

| Argument | Description | Example |
|---       |---          |---      |
| repeat   | Repeat the same session again after N minutes after completion, disabled by default. | `120-180` |
| working-hours   | Scheduler for bot activity. You can specify the interval (one or more) of time in which you want the bot to run. You must use the time notation 0-24. You can use with the above argument `--repeat` for have a never stop bot.  | `[10.15-16.40, 18.15-22.46]` |
| time-delta   | This is intended to be used with `working-hours` and allows to change the start and the end point of each interval. A random value, positive or negative, will be generated. | `10-15` |

## Available Filters

We know that you want to make sure that you only interact with a specific set of users. When you leave it up to a bot, you never know what will happen. We try to make this easier for you by giving you a wide subset of filters to help weed out the undesirables. The full list is below, but if you need some inspiration - there is a filter.example file included with some sensible defaults. You can either rename this to `filter.json` and modify as desired or create a new file named `filter.json` and add only the disired filters in a json dictionary format.

```
  "skip_business"             
        If it is true, business acounts won't be interacted.
        (e.g. "skip_business": true)

  "skip_non_business"         
        If it is true, private accounts and public accounts 
        won't be interacted.
        (e.g. "skip_non_business": true)
  
  "skip_following"
        If it is true, accounts that you follow won't be interacted
        with. 
        (e.g. "skip_following": true)
        
  "skip_follower"
        If it is true, accounts that follow you won't be interacted
        with. Note, if you follow someone, the filter won't be able
        to tell if that person follows you.
        (e.g. "skip_following": true)

  "min_followers"             
        It is the lower follower bound for an account that can 
        be interacted. If an account has less followers than 
        this amount, it wont be interacted. 
        (e.g. "min_followers": 100)

  "max_followers"             
        It is the upper follower bound for an account that can 
        be interacted. If an account has more followers than 
        this amount, it wont be interacted. 
        (e.g "max_followers": 1000)

  "min_followings"            
        It is the lower following bound for an account that can 
        be interacted. If an account has less followings than 
        this amount, it wont be interacted. 
        (e.g. "min_followings": 300)
  
  "max_followings"            
        It is the upper following bound for an account that can 
        be interacted. If an account has more followings than 
        this amount, it wont be interacted. 
        (e.g. "max_followings": 800)

  "min_potency_ratio"         
        If an account's followers/following ratio is not above 
        this ratio, then they will not be interacted with. 
        Combine with "max_potency_ratio" to specify a range.
        Example: username has 500 followers and 1000 
        followings. That means its ratio is 0.5 If you set your 
        "min_potency_ratio": 0.2 it will be interacted with. 
        (e.g. "min_potency_ratio": 1)

  "max_potency_ratio"         
        If an account's followers/following ratio is not below 
        this ratio, then they will not be interacted with. 
        Combine with "min_potency_ratio" to specify a range.
        Example: username has 500 followers and 1000 
        followings. That means its ratio is 0.5 If you set your 
        "max_potency_ratio": 0.7 it will be interacted with.
        (e.g. "max_potency_ratio": 2)
                              
  "follow_private_or_empty"   
        If it is false, private accounts or public accounts 
        that have no posts will not be interacted with. 
        (e.g. "follow_private_or_empty": false)

  "interact_only_private"     
        If it is set to true, only private accounts will be    
        interacted with. No public accounts will be interacted 
        with.
        (e.g. "interact_only_private": true)
        
  "blacklist_words"     
        Checks a biography for specified words. If any one word 
        is found in the bio, the user will not be interacted with.
        Otherwise the user will be interacted with. 
        (e.g. "blacklist": ["sex", "furry", "biden"])
       
  "mandatory_words"     
        Checks a biography for specified words. If any one word 
        is found in the bio, the user will be interacted with.
        Otherwise the user will not be interacted with. 
        (e.g. "mandatory_words": ["cat", "kitten", "meow"])
        
  "specific_alphabet"     
        If a type is specified, the bio will be inspected and
        the primary character type will be matched against the
        one specified. If they do not match, you will not interact
        with them. This is commonly used to avoid people whose
        biographys don't match your language.
        From version 2.0 you can set more then one.
        (e.g. "specific_alphabet": ["LATIN", "ARABIAN"])

  "min_posts"                 
        You can specify the minumum post number that an account 
        should have. 
        (e.g. "min_posts": 7)
   
  "comment_hashtag_likers_top"
  "comment_hashtag_likers_top"
  "comment_hashtag_likers_recent"
  "comment_hashtag_posts_top"
  "comment_hashtag_posts_recent"
  "comment_place_likers_top"
  "comment_place_likers_recent"
  "comment_place_posts_top"
  "comment_place_posts_recent"
  "comment_blogger_followers"
  "comment_interact_usernames"
  "comment_blogger_post_likers"
  "comment_interact_from_file"
  "comment_feed"
        You can specify for which job you want to comment.
        Every interaction type has his own filter.
        For example if you set your comments_list.txt with 
        text that fits place posts, you don't want to say 
        something about Rome in other circumstances.
        
  "comment_photos":
  "comment_videos":
        You can also turn on/off commenting videos or photos.
```

## Comments
In order to comment post, you have also to set your comments_list.txt which is located inside the folder with your nickname. Every username has his own comments_list.txt file.
I've dived that file in 3 sections: %PHOTO, %VIDEO and %CAROUSEL. The reason of that is for allow you to have 3 different type of comment in relation of what you're effectively commenting. A lot of time other bots commented on my videos with "nice photo!". In this way you will be less detectable.
I also made possibile to use emoji [look here for emoji list supported](https://www.webfx.com/tools/emoji-cheat-sheet/).

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

## Private message
You can send private message to people you're interacting with. You just have to set your pm_list.txt file, always in the folder with your nickname. Every username has his own pm_list.txt file. Emoji are supported.

For example:
```
Hello there! I'm bla bla consider follow me! :smile:
Sorry for bothering you, can you pls take part of my survey? 
:fu:
```
A random one will be picked each time.

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

When honoring limits, the bot uses the following priority:

- **Total Interactions or Total Successful Interactions**:  If either of these are met, the current run will stop without interating through any additional sources. If no repeat is enabled, the script will stop.
- **Total *Type* Limit**: If a total *type* limit is met, no more of that *type* will be done. If possible, the bot will continue running.
- **Individual Limits (e.g. interaction-count, unfollow, follow)**: If the limit is met, but the total limits are not met, the bot will continue on another source (if possible) or possibly continue until the other individual limits are met.

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
