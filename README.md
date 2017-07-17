# Personalized Shopping Suggestions

## What
- Suggest designs for purchase based on authenticated users' social media activity.

## Why
- This can lead to a more personalized shopping experience.
- It can strengthen customers' brand-association.
- It would be a fun task to implement this feature.

## How

### General Overview
- Spoonflower's designs have 'tag' data, as can be seen on results from its new API.
- Twitter posts have 'hashtag' data.
- There will likely be overlaps between these two sets of tags.
- Comparing the users' most-used hastags with tags associated with designs would enable the suggestion of new designs.

### Backend Implementation
Assuming a user has authorized Spoonflower to access Twitter data, and the needed
Twitter account information is stored on the user's db record:
- Implement an API endpoint for retrieving suggested designs for a user.
  - Controller's action will:
    - Query Twitter for the user's Tweets, let's say 50 most recent for now.
    - Reduce Twitter API results to a flat array of hashtags featured in those tweets.
    - Query the designs tags table for records with a tag that is included in the array of hashtags, limit to say, 20 for now.
    - Query and respond with the designs associated with these tags, using the same response format as the 'search' API endpoint for consistency.
- Of course, acceptance, integration, and/or unit tests will be needed!


### Frontend Implementation
- On 'Home' view, include a section of page that is a row for suggestions.
  - This row would be empty for users who have not yet authorized Spoonflower to integrate with Twitter. There could be a button for Twitter and a suggestion for users to integrate.
- On initial loading of view, the React container for the suggestions would dispatch an asynchronous action to fetch the suggestions from an API endpoint.
- On receiving the API response, another action would dispatch
- Test the container's ability to receive and render these results, possibly via Jest.


### Technology to Use
- Twitter API
- isomorphic fetch

### Personnel

### Potential Challenges
- Feature efficacy
  - One likely scenario on initial implementation is that users will have suggestions for designs that they may have already purchased.
    - This could be smoothed out in planning another feature for the filtering of suggestions.
    - This would not be entirely inconsistent with other E-Commerce platforms that have similar "rough edges" and such challenges.
  - There may be the possibility of having empty results (user does not use hashtags, or hashtags have no corresponding tags on Spoonflower).
- Scalability
  - Querying Twitter for potentially large amounts of data on a user's posts.
  - Querying through large quantities of designs to match tag data with a user's hashtag-related data from Twitter.
- Guiding users to integrate with Twitter and give permissions to Spoonflower to access data.
  - Users will likely not mind sharing data, but they may need to be convinced that they want to make a few extra clicks and possibly log-in to Twitter, as well.
