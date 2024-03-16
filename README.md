var retweetTweets = function() {
    var tweets = document.querySelectorAll('[data-testid="tweet"]');
    var retweetCount = 0; // Initialize retweet counter
    
    tweets.forEach(function(tweet) {
        // Check if the tweet has already been retweeted
        var retweetButton = tweet.querySelector('[data-testid="retweet"]');
        var retweeted = tweet.querySelector('[data-testid="retweet"] div[aria-label="Undo Retweet"]');

        // Check if the tweet contains images
        var media = tweet.querySelector('[data-testid="tweetPhoto"]');
        
        if (retweetButton && !retweeted && media) {
            // Click the retweet button
            retweetButton.click();
            setTimeout(function() {
                // Check if both retweet and quote buttons exist
                var quoteButton = document.querySelector('[data-testid="retweetConfirm"]');
                if (quoteButton) {
                    // Click the retweet button again to choose "Retweet" option
                    document.querySelector('[data-testid="retweetConfirm"]').click();
                    console.log("Retweeted.");
                    retweetCount++; // Increment retweet counter
                } else {
                    console.log("Could not retweet.");
                }

                // Check if retweet count reaches the limit (e.g., 300)
                if (retweetCount >= 300) {
                    console.log("Reached the retweet limit. Stopping script.");
                    return; // Stop the script
                }
            }, 1000); // Wait 1 second before checking for quote button
        }
    });

    console.log("Scrolling down to load more tweets.");
    window.scrollBy(0, window.innerHeight); // Scroll down to load more tweets
    setTimeout(retweetTweets, 5000); // Wait for 5 seconds before repeating
};

retweetTweets();
