## cool new stuff

shithead-ng has been superseded by [shithead-X](https://github.com/albino/shithead-X), which uses very fancy GPT-2 instead of old and boring Markov chains. but if you submit an issue to shithead-ng I will still answer it.

## important

recent config changes:

 - target_words option
 - irc_channel changed to irc_channels
 - respond_on_highlight option

If you do not update your config.yml file to reflect these changes, shithead-ng will not work!

# shithead-ng

next generation markov chain irc shitposting bot

### The problem
The original shithead uses far too much ram and is badly implemented.

### The solution
Let's reimplement it and get redis to do all the heavy lifting.

## Getting Started
First, set up dependencies. You need a redis server and the necessary perl modules:

```bash
# install cpanminus with your package manager of choice (preferred), or install it through cpan:
cpan App::cpanminus
# clone the git repo if you haven't already, then install the perl modules
git clone https://neetco.de/albino/shithead-ng
cd shithead-ng
cpanm --installdeps .
# or, to avoid setting up local::lib:
cpanm --sudo --installdeps .
```

Next, you need a brainfile. A brainfile is simply an irc log with all joins, parts, timestamps and nicknames stripped. In other words, it contains only what was said.

```bash
# if you have an old brainfile, import it into redis
perl import-brain.pl /home/you/brainfile
# this can take a long time (about ten minutes for me), so be patient
```

```bash
# now, you need a config file
cp config.default.yml config.yml
# edit the values in config.yml to your choosing
```

Now, just run `perl MarkovBot.pl`.

## Commands

* .shitposting - controls the % of messages the bot will reply to
```
< user> .shitposting 1.5
< shithead-ng> OK
```

* .ignore - make the bot totally ignore a user (useful for bots)
```
< user> .ignore bot
< shithead-ng> Now ignoring bot.
```

* .unignore - removes a user from the ignore list
```
< user> .unignore bot
< shithead-ng> No longer ignoring bot.
```

* .ping - check that shithead-ng is still alive
```
< user> .ping
< shithead-ng> Pong!
```

## Command line options
```text
-f: specify a YAML config file for shithead-ng to use. Defaults to /path/to/shithead-ng/config.yml.
```

## Exporting the brainfile

```bash
perl export-brain.pl > brain
```

This produces a shithead-ng brainfile which cannot (currently) be read by other programs. This is because the redis database does not contain enough information to reconstruct the brainfile it was created from. This file can, however, be read by shithead-ng's import-brain.pl.
