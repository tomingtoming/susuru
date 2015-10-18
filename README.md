# susuru (啜る)
Management modules to use up RateLimit on Twitter4J.

# Quick usage
## Initialize
```scala
import susuru.twitter.TwitterPool
import twitter4j.Twitter
// Initialize pool with function to get Map[Long(id), Twitter] excepting specified ids.
TwitterPool singleton { idSet: Set[Long] =>
  TwitterRepository.getAll.filter { (twitter: Twitter) =>
    !idSet.contains(twitter.getId)
  }
}
```

## Use (User-specified)
```scala
// Get instance of Twitter for user id:123456.
val twitter: Twitter = TwitterPool.getInstance(123456)
val result = twitter.lookupUsers(123, 456, 789)
```

## Use (User-unspecified)
```scala
// Get instance of Twitter for any user. Usable resource will be selected.
val twitter: Twitter = TwitterPool.getInstance()
val result = twitter.lookupUsers(123, 456, 789)
```
