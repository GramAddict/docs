## Multiple Action Support

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
        sources, 300 by default

  --total-follows-limit 50
        limit on total amount of follows during the session across all
        sources, 50 by default

  --total-watches-limit 50
        limit on total amount of story watches during the session across 
        all sources, 50 by default

  --total-successful-interactions-limit 100
        limit on total amount of successful interactions during the
        session across all sources, 100 by default

  --total-interactions-limit 1000
        limit on total amount of successful and non-successful interactions
        during the session across all sources, 1000 by default
```

So if you wanted to interact with multiple bloggers, multiple hashtags, unfollow followers, and generate a report after - you can do a command similar to below:

```
python3 run.py --blogger-followers justinbieber selenagomez --hashtag-likers-top popmusic bestartists --interactions-count 20 --follow-percentage 20 --total-successful-interactions-limit 80 --total-interactions-limit 700 --total-likes-limit 160 --total-follows-limit 20 --unfollow 16 --analytics myusername --repeat 200-260
```

This command would:
- Interact with 20 each of @justinbieber's and @selenagomez's followers, following 20% of them (~4 follows each, ~8 total). The order of @justinbieber and @selenagomez will be randomized each time. 
- Interact with 20 each of likers of posts in top results of #popmusic and #bestartists, following 20% of them (~4 follows each, ~8 total). The order of #popmusic and #bestartists will be randomized each time. 
- Unfollow 16 people in order of oldest to newest. 
- Generate a PDF report for @myusername using the session data from previous runs
- The above will repeat the above steps every 200-260 minutes.



## Command Line Arguments

GramAddict can do many things and the list is constantly growing. This is a full list of the command line arguments that can be provided in order for you to get started using it. We know this is a crazy long list, so if you need help getting started - check out our [sensible examples](/examples).

### Argument Glossary

- **Source**: The *thing* being interacted with, primarily usernames or hashtags 
- **Interaction**: Any profile that is interacted with for a particular **source** (successful or unsuccessful)
- **Successful Interaction**: Any profile that was actioned (e.g. like or follow) for a particular **source**
- **Unsuccessful Interaction**: Any profile that was opened, but not actioned (e.g. like or follow) for a particular **source**

- **Total Interactions**: Number of profiles with **successful interactions** or **unsuccessful interactions** across all **sources**
- **Total Successful Interactions**: Number of profiles with **successful interactions** with across all **sources**
- **Other "Total" Limits**: Number of *item* done, across all **sources**

### Limit Logic

When honoring limits, the bot uses the following priority:

- **Total Interactions or Total Successful Interactions**:  If either of these are met, the current run will stop without interating through any additional sources. If no repeat is enabled, the script will stop.
- **Total *Type* Limit**: If a total *type* limit is met, no more of that *type* will be done. If possible, the bot will continue running.
- **Individual Limits (e.g. interaction-count, unfollow, follow)**: If the limit is met, but the total limits are not met, the bot will continue on another source (if possible) or possibly continue until the other individual limits are met.

### Arguments

Full list of command line arguments:
```
  --blogger-followers username1 [username2 ...]
        list of usernames with whose followers you want to interact
  
  --hashtag-likers-top hashtag1 [hashtag2 ...]
        list of hashtags in top results with whose likers you want to interact
  
  --hashtag-likers-recent hashtag1 [hashtag2 ...]
        list of hashtags in recent results with whose likers you want to interact

  --posts-from-file posts.txt
        provide the path to a text file of posts that should be interacted with.
        Presently, this will only like posts. More actions coming in the future.
        Useful for engagement groups.

  --likes-count 2-4
        number of likes for each interacted user, 2 by default. It 
        can be a number (e.g. 2) or a range (e.g. 2-4)

  --stories-count 2-4   
        number of stories for each interacted user, 0 by default. It 
        can be a number (e.g. 2) or a range (e.g. 2-4). Supported 
        by plugins: hashtag-likers, blogger-followers

  --stories-percentage 30-40
        chance of watching stories on a particular profile, 30-40 by 
        default. It can be a number (e.g. 30) or a range (e.g. 30-40) 
        Supported by plugins: hashtag-likers, blogger-followers

  --interactions-count 60-80
        number of interactions per each blogger, 70 by default. It 
        can be a number (e.g. 70) or a range (e.g. 60-80). Only 
        successful interactions count.

  --total-likes-limit 300
        limit on total amount of likes during the session across all
        sources, 300 by default

  --total-follows-limit 50
        limit on total amount of follows during the session across all
        sources, 50 by default

  --total-watches-limit 50
        limit on total amount of story watches during the session across 
        all sources, 50 by default

  --total-successful-interactions-limit 100
        limit on total amount of successful interactions during the
        session across all sources, 100 by default

  --total-interactions-limit 1000
        limit on total amount of successful and non-successful interactions
        during the session across all sources, 1000 by default

  --repeat 120-180
        repeat the same session again after N minutes after 
        completion, disabled by default. It can be a number of 
        minutes (e.g. 180) or a range (e.g. 120-180)

  --follow-percentage 50
        follow given percentage of interacted users, 0 by default

  --follow-limit 50
        limit on amount of follows during interaction with each one 
        user's followers, disabled by default

  --unfollow 100-200    
        unfollow at most given number of users. Only users followed 
        by this script will be unfollowed. The order is from oldest 
        to newest followings. It can be a number (e.g. 100) or a 
        range (e.g. 100-200)

  --unfollow-non-followers 100-200
        unfollow at most given number of users, that don't follow you
        back. Only users followed by this script will be unfollowed.
        The order is from oldest to newest followings. It can be a 
        number (e.g. 100) or a range (e.g. 100-200)

  --unfollow-any 100-200
        unfollow at most given number of users. The order is from 
        oldest to newest followings. It can be a number (e.g. 100) 
        or a range (e.g. 100-200)

  --min-following 100   
        minimum amount of followings, after reaching this amount 
        unfollowing stops

  --device 2443de990e017ece
        device identifier. Should be used only when multiple
        devices are connected at once

  --screen-sleep        
        turns on the phone screen when the script is running and 
        off when when it's ended or sleeping (e.g. when using with
        --repeat) - disable the passcode for unlocking the phone
        if you want to use this function!

  --analytics username1
        Generates a PDF analytics report of specified usernames
        session data


```

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

  "min_posts"                 
        You can specify the minumum post number that an account 
        should have. 
        (e.g. "min_posts": 7)
```
