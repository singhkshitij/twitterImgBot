# MyTrashCode Twitter bot 

Twitter handle : [@mytrashcode](https://twitter.com/mytrashcode)

## What it does ?

It automatically posts random images with some hashtags on twitter to build social media presence for my blog [Mytrashcode](https://mytrashcode.com)

You can find the setup instruction on the [original repo here](https://github.com/joaquinlpereyra/twitterImgBot) if you also want to build one.

## From where do i get image ? 
I scrap them in one shot from popular programming meme subreddits and uploaded to an static folder on a linux instance running all time. 

## Do i pay for linux instance ?
No. I run a lifetime free linux instance on GCP. It does the job for me.

## Does the bot automatically post ?
No. I have scheduled a cron job to trigger randomly 3 times a day.
```
0 0,8,16 * * * sleep $(( RANDOM \% 14400 )); /usr/bin/python3 /home/kshitij.singh/twitterImgBot/twitterbot.py --tweet
```
It runs the python script and does the job.

### Where do i store these images ? 

In folder `twitterImgBot/images/reddit_sub_ProgrammerHumor/`

### How do i scrap reddit images ?
This is a one time job, which i achieved with tool called [ripme](https://github.com/ripmeapp/ripme/wiki/How-To-Run-RipMe).

SSH to box and run
```
java -jar ripme.jar --url https://www.reddit.com/r/ProgrammerHumor/top/?t=year --ripsdirectory ./twitterImgBot/images/

```

### Cleanup steps :
Remove videos or other non image files that could have been scraped also by running these commands :

```
ls | wc -l
find . -type f ! \( -name '*.jpg' -o -name "*.png" \) -delete
ls | wc -l
```