## FaceBook Video Metrics
I've been messing around w/ some FB data at work, so I'm recording some notes as I go.  These come
from [Master Your Facebook Video Metrics](https://www.rivaliq.com/blog/mastering-facebook-video-metrics/).

* Post-Engagement Metrics (All Post Types)
  - Two Primary Metrics (available only to page owner):
    * Impressions: number of times your post has been seen
    * Reach: Number of unique FaceBook User impressions
  - Side Note: For video, these things are often just called "views" and "uniques"
  - The Impressions and Reach metrics are cut up in 3 ways
    * Organic
    * Viral 
    * Paid
* Engagement Metrics (All Post Types)
  - Like, Comments, and Shares (publicly available)
  - Can be used to benchmark against competing content since this data is public
  - Total Engagement: Clicks + Likes + Comments + Shares
  - Total Reach: 
    * they didn't seem to define this explicitly, so it can be
    * (a) Unique Clickers + Unique Likers + Unique Commenters + Unique Sharers
    * (b) UniqueFaceBookers(Clickers, Likers, Commenters, Sharers)
  - Engagement Rate:  Total Engagement / Total Reach
* Video Metrics
  - Total Video Views: Number of times video has been viewed for 3+ seconds
    * Can be broken down into Paid and Organic segments
  - 10-Second Views:  Number of times a video has been viewed for 10+ seconds (or completed if duration < 10s)
    * Can be broken down into Paid and Organic segments
  - 30-Second Views:  ...you get the point...
  - Complete Views:  Number of views starting from beginning of video and covering 95% or more
    * Bit about Paid and Organic segements again!
    * For videos < 30 seconds, Complete Views can be greater than 30-Second Views
      - e.g., for 20-second video, video must be completed for 20-second metric, but only 19 seconds (95%) to register as completed
  - Video Retention Vs Time:  graph showing %retained over videoTime
    * if there is a point w/ sharp drop off, figure out what is wrong and improve it
    * if retention has sharply dropped before main selling point, get to the point quicker!
  - Auto-Play vs Click-to-Play and Sound On/Off
    * Apparently this blog's owner can get you these numbers
    * How to get 'em myself?
  - Video View Rate ("Attractiveness"):  Total Views / Total Impressions
    * that is what is the % of impressions that viewed > 3 seconds 
  - 30-Second View Rate ("Stickiness"):  Total 30-Second Views / Total Views
    * that is, how many of those that actually viewed > 3 second stuck around for 30+ seconds?
  - Completer Rate ("Stickiness"):  To Complete Views / Total Views

============================================================================

https://developers.facebook.com/docs/graph-api/reference/video/video_insights/

https://developers.facebook.com/docs/graph-api/reference/v2.10/insights

https://developers.facebook.com/docs/marketing-api/insights/

https://developers.facebook.com/tools/explorer

Example of what to plug in to Explorer (v2.6):
* wwe/insights?fields=impressions,social_clicks,website_clicks,ctr&time_range={'since':'2017-01-01','until':'2017-01-30'}&time_increment=1

Using v2.10, I found out how to look at likes, comments, etc in the Graph Explorer:
* 10155166528086443/likes  
* 10155166528086443/comments
* 10155166528086443/sharedposts
* 10155166528086443/video_insights
  - this one we need to be signed in for
  - https://developers.facebook.com/docs/graph-api/reference/video/video_insights/


Live Video API: https://developers.facebook.com/docs/videos/live-video


Python FaceBook Package
* http://facebook-sdk.readthedocs.io/en/latest/install.html
```python
# This package only seems to support up to version 2.7 (currently on v2.10)
graph = facebook.GraphAPI(access_token="your_token", version="2.7")
# But! It does retrieve the data I need
graph.get_object("/10155166528086443/video_insights")
```


