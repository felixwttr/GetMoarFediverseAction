# GetMoarFediverse

This is a small app that shows how you could use [FakeRelay](https://github.com/g3rv4/FakeRelay/) to import content into your instance that's tagged with hashtags you're interested in.

This doesn't paginate over the tags, that means it will import up to 20 statuses per instance. This also keeps a txt file with all the statuses it has imported.

## How can I run it?

The easiest way is with docker compose. This `docker-compose.yml` shows how it can be used:

```
version: '2'
services:
  importdata:
    image: 'ghcr.io/g3rv4/getmoarfediverse:latest'
    volumes:
      - '/path/to/data:/data'
```

On `/path/to/data`, you need to place a `config.json` that tells the system what you want. You could use something like this:

```
{
    "FakeRelayUrl": "https://fakerelay.gervas.io",
    "FakeRelayApiKey": "1TxL6m1Esx6tnv4EPxscvAmdQN7qSn0nKeyoM7LD8b9mz+GNfrKaHiWgiT3QcNMUA+dWLyWD8qyl1MuKJ+4uHA==",
    "Tags": [
        "dotnet",
        "csharp"
    ],
    "Sites": [
        {
            "Host": "hachyderm.io",
            "SiteSpecificTags": [
                "hachyderm"
            ]
        },
        {
            "Host": "mastodon.social"
        }
    ]
}
```

Once you have that set up, you can just execute it! and it will output what's going on. You can run this on a cron!

```
g3rv4@s1:~/docker/FakeRelay$ docker-compose run --rm import
Fetching tag #dotnet from mastodon.social
Fetching tag #hachyderm from hachyderm.io
Fetching tag #dotnet from hachyderm.io
Fetching tag #csharp from mastodon.social
Fetching tag #csharp from hachyderm.io
Bringing in https://dotnet.social/users/mzikmund/statuses/109458968117245196
```