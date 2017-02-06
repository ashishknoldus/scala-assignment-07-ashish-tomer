# scala-assignment-07-ashish-tomer

## Problem Statement : 

    Create a application in which:

    Retrieve tweet  on the basis of HASHTAG(#hashtag)
    Find number of tweets
    Find average tweets per day
    Find average likes and re-tweets per tweet
    
    
-------------------------------------------------------------------------

<ui>

<li>Futures are used for computation</li>

<li>Test coverage is 100%</li>

<li>There are 4 scalastyle warnings (reason discussed below)</li>

<li>Every method is well documented</li>

</ul>

------------------------------------------------------------------------

## Challenges

### 1. Java to scala conversion of Collections :
### 2. I've used a lot of vars (with thread safety) to read data from results of multiple pages.
###     <span style="color:brown">Note : One page can show a max of 100 tweets, if tweets for one hashtag are more than that we need to read next query</span>

<small>I want to discuss to Prabhat about 2nd point listed above.</small>

I had to use `null` in the code because of Java code. AND THAT'S THE SCALASTYLE WARNING - 4 TIMES!!

Below is the code I used as reference ( <a href="https://github.com/yusuke/twitter4j/blob/master/twitter4j-examples/src/main/java/twitter4j/examples/search/SearchTweets.java">link</a> ) : 

------------------------------------------------------------------------

<pre><code>
/*
 * Copyright 2007 Yusuke Yamamoto
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

package twitter4j.examples.search;

import twitter4j.*;

import java.util.List;

/**
 * @author Yusuke Yamamoto - yusuke at mac.com
 * @since Twitter4J 2.1.7
 */
public class SearchTweets {
    /**
     * Usage: java twitter4j.examples.search.SearchTweets [query]
     *
     * @param args search query
     */
    public static void main(String[] args) {
        if (args.length < 1) {
            System.out.println("java twitter4j.examples.search.SearchTweets [query]");
            System.exit(-1);
        }
        Twitter twitter = new TwitterFactory().getInstance();
        try {
            Query query = new Query(args[0]);
            QueryResult result;
            do {
                result = twitter.search(query);
                List<Status> tweets = result.getTweets();
                for (Status tweet : tweets) {
                    System.out.println("@" + tweet.getUser().getScreenName() + " - " + tweet.getText());
                }
            } while ((query = result.nextQuery()) != null);
            System.exit(0);
        } catch (TwitterException te) {
            te.printStackTrace();
            System.out.println("Failed to search tweets: " + te.getMessage());
            System.exit(-1);
        }
    }
}
</code>
</pre>


### My Rate Limit has exceeded
I can't even create a new app
![alt tag](https://raw.githubusercontent.com/ashishknoldus/scala-assignment-07-ashish-tomer/master/RateLimit.png)
