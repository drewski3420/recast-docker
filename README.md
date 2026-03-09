# Recast

Recast is a django based podcast feed rebroadcaster.  There is a running version at https://recastthis.com if you want to try it out.

Recast is designed to make it convenient to listen to all the old episodes of a podcast from the beginning.

Most podcast clients will only automatically present the latest episode of a podcast and leave you to manually download previous episodes one by one, eliminating the convenience of automatic delivery.

Instead of subscribing directly to the podcast, you give Recast the address of the website or feed of the podcast and it will return you a unique, personalized feed. Simply subscribe to the Recast feed instead.

By default Recast will feed you a new episode of the podcast every five days - enough to slowly catch up with most weekly podcasts. At any time, you can change the frequency new episodes are released, or just release the next episode.

## Docker Installation

Clone the repo into your recast directory. Rename the folder to src (or adjust the build context in the docker-compose.yml file)

Copy docker-compose.yml and env_file example files into recast folder. Adjust values as necessary, especially in env_file. Be sure to mount a volume for db_data to persist your recast data.

Bring the container up using docker-compose up -d. Navigate to localhost:8000 (or whatever port you've mapped) to view the application.

### Recast Specific Settings

Recast will work with a Cloudflare account (a free one will do) to provide caching.  To take advantage of this, provide the following details

* `CLOUDFLARE_TOKEN` = Cloudflare API token if you are using it
* `CLOUDFLARE_ZONE` = Cloudflare Zone if you are using it

You can use a Cloudflare web worker to bust through Cloudlflare protected feeds.  Set up a new worker with the code in
[this file](https://raw.githubusercontent.com/xurble/django-feed-reader/master/support/cloudflare_worker.js) and then
put the url into the following setting.

* `FEEDS_CLOUDFLARE_WORKER` -  The url to your cloudflare worker if you are using them e.g. `https://foo.bar.workers.dev`


### Updating feeds

Once Recast is running, in order to keep it ticking over and reading feeds you need to periodically call `manage.py refreshfeeds`

I have a cron job that does this every 10 minutes.  

And that's it.

