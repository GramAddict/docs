## Command Line Arguments

GramAddict can do many things and the list is constantly growing. This is a full list of the command line arguments that can be provided in order for you to get started using it. We know this is a crazy long list, so if you need help getting started - check out our [sensible examples](/?id=sensible-examples).

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
        default. It can be a number (e.g. 2) or a range (e.g. 2-4) 
        Supported by plugins: hashtag-likers, blogger-followers

  --interactions-count 60-80
        number of interactions per each blogger, 70 by default. It 
        can be a number (e.g. 70) or a range (e.g. 60-80). Only 
        successful interactions count.

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