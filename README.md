**Open Speech Recording** is a small web application to collect short snippets
of speech, and upload them to cloud storage. It's designed to help gather open
speech data sets to train machine learning systems.

It's based around a small Flask app that will run on Google App Engine. This
serves up a client-side Javascript app that prompts for a series of words,
records the audio, and then POSTs the results back to the server.

## Running

1. Install pip dependencies with `pip install -t lib -r requirements.txt`.
2. Edit `app.yaml` with updated environment variables.

If you have the Google Cloud SDK set up, you should be able to run a local copy
with this command:

```
dev_appserver.py app.yaml
```

I've often had trouble getting local copies of the app to work with cloud
storage, so you may see errors on the final upload stage with this setup. To
deploy it to an appspot instance, run this:

```
gcloud app deploy
```

## Input and output formats

Phrases that we want to collect are stored in `static/phrases.json`. Recordings
will be stored in the bucket specified in the app.yaml environment variable, in
the path: /$phraseKey_$sessionId_$UUID.ogg.


## Notes and TODOs (for Stella/Dan)

- I gave the gs://the-phrasebook bucket the canned public-read-write ACL. This
  is no good, and it should be set to something that only this AppEngine can
  write to, and nobody can delete from at all (like a dropbox).



## Credits

Thanks to the Mozilla team for the [Web Dictaphone sample application](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream_Recording_API/Using_the_MediaStream_Recording_API#A_sample_application_Web_Dictaphone)
that I used as a starting point, [Sole](https://soledadpenades.com/) for the
oscilloscope, and the Flask team for a lovely Python microframework!

Written by Pete Warden, pete@petewarden.com.
