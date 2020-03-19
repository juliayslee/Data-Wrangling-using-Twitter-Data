# Data-Wrangling-using-Twitter-Data
Using Twitter's API, we will go through the data wrangling process for the Twitter account WeRateDogs. This Twitter account is a humorous account of pictures of dogs with a witty caption, for example ["This is Andi and Olli. They fell asleep arguing over who gets to cuddle the chicken toy. 13/10 for both"](https://twitter.com/dog_rates/status/1240080545306066945), and each tweet always includes a rating- usually a high rating out of 10 (10/10, 11/10, 12/10, etc.) These lovable tweets have gained immense popularity with the WeRateDogs account boasting 8.7 million followers to date. With these many followers, inevitably each tweet garners many "favourites" and "retweets". This Jupyter Notebook attached will take you through the entire data wrangling process, starting from gathering the data, cleaning the data, and analysis/visualization. 

For the Gathering Part:
- Imported all necessary libraries (pandas, numpy, matplotlib.pyplot and tweepy (Python's Twitter library)
- Read in tweet archive csv data, image predictions file (images of dogs in tweets predicted through a neural network), JSON file of tweets information like retweet count, favourite count, etc. 
  - this code below was provided and used to query Twitter's API to gather tweet information
```
import tweepy
from tweepy import OAuthHandler
import json
from timeit import default_timer as timer

consumer_key = 'HIDDEN'
consumer_secret = 'HIDDEN'
access_token = 'HIDDEN'
access_secret = 'HIDDEN'

auth = OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_secret)

api = tweepy.API(auth, wait_on_rate_limit=True)

tweet_ids = df_1.tweet_id.values
len(tweet_ids)

count = 0
fails_dict = {}
start = timer()

with open('tweet_json.txt', 'w') as outfile:
    # This loop will likely take 20-30 minutes to run because of Twitter's rate limit
    for tweet_id in tweet_ids:
        count += 1
        print(str(count) + ": " + str(tweet_id))
        try:
            tweet = api.get_status(tweet_id, tweet_mode='extended')
            print("Success")
            json.dump(tweet._json, outfile)
            outfile.write('\n')
        except tweepy.TweepError as e:
            print("Fail")
            fails_dict[tweet_id] = e
            pass
end = timer()
print(end - start)
print(fails_dict)
```

