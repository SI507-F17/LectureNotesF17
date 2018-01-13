# SI 507 | Lecture 9 | November 1, 2017 | APIs & OAuth Protocols, useful Python libraries

# Admin

Any questions?


# APIs and Authentication
- You’ve seen APIs before, and caching of now a few different sorts
- You know that there are different tradeoffs to make when designing a program
- You’ve experienced or had access to code that gets data from the internet with authentication like an API key specific to your account on a service like FB or Twitter, and maybe you’ve experienced getting data from services that follow the **OAuth protocol** before
  - Today we’re going to dig into that a bit


## REST APIs: things you need to know
- Endpoints (and the base urls that go with them) — deciphering documentation
- Security, scopes, specific URLs for authentication — “”
- Required (and optional) query parameters — “”


# OAuth (1 and 2) Protocols
## Intention: Data exchanged between web services

And data security
Have you seen a web page that looks like this? (where you can sign into a given service with your Facebook account)?

![](https://camo.githubusercontent.com/e44f1cad38b343b3ff5fde6d21840aaac470a69e/68747470733a2f2f6c68342e676f6f676c6575736572636f6e74656e742e636f6d2f2d305555496563542d334e342f552d4c514a6b64373569492f4141414141414141455a592f594e334f652d65555047632f77313637362d68313135382d6e6f2f736174656c6c697a65722e706e67)


For example, Spotify allows you to log in with Facebook or to create an account:

![](https://www.dropbox.com/s/1vwfmubecrep4nq/Screenshot%202017-04-03%2011.54.37.png?dl=1)


This is done with **OAuth**. OAuth is an authorization protocol -- or in other words, **a set of rules** --  that allows a third-party website or application to access a user's data without the user needing to share login credentials. (from *Technopedia*)

Note: we definitely don’t expect anyone to memorize this. I just want to illustrate what happens when you authenticate with a third party.

 https://developer.yahoo.com/oauth/guide/oauth-auth-flow.html
 **OAuth 1 Flow**

![](https://d2mxuefqeaa7sj.cloudfront.net/s_FEED692B22B617ED34F96344493E5579D3310E9D83D52F04C89D8E476418404F_1484696501556_hackpad.com_noAVIeDWojZ_p.664750_1479136742006_oauth_graph.gif)


Any service that lets your program do things on behalf of users requires oauth. Some APIs require oauth for everything.

**The most common version of oauth expects your program to be running a web server.**
****

1. The user, in a browser, visits the external site (e.g., Twitter), and authorizes your program to act on behalf of the user.
  1. You pass a "redirect url" as one of the parameters in the original URL
2. The external site "redirects" the browser to *your* web server
3. Your program running at your webserver extracts a credential from the redirected URL
4. Your program uses the credential in further communications with the external site's API

**We will modify this slightly****. For example****:**
****
1. Same as above. User enters password in web browser
2. The external site redirects to https://www.programsinformationpeople.org/runestone/oauth
  1. User cuts and pastes that whole URL into your running program
3. Your program extracts a credential from the pasted URL
4. Same as above: Your program uses the credential in further communications with the external site's API.


## oAuth1 (e.g., Twitter requests on behalf of another user)

See code and comments in the textbook, and `oauth1_twitter_caching.py`.

**Note that Twitter offers a special service with its API, where,** instead of redirecting at step 2 above, it provides a page at Twitter.com that displays a code for the user to cut and paste into the running python program on your laptop/desktop. That makes it a little easier, because there's no effort to extract the code from a url.

## oAuth2 (many newer services)

Check out http://requests-oauthlib.readthedocs.io/en/latest/oauth2_workflow.html#web-application-flow
Documentation for Spotify at: https://developer.spotify.com/web-api/tutorial/
We’ll look at a couple of examples of managing oAuth2 authentication.

Regardless of which version of the protocol, proceeding through a process with OAuth generally happens between two web servers: the server belonging to the **consumer**, or **client**, which you as a programmer can think of as “the application you’re making” (which wants data from this other app using OAuth).

At this point in this course,
you want to *basically* circumvent the need for running your own web server, in order to get data from this external service for processing, analysis, etc.

There are a few ways of doing this that will make what you already know from 506 or equivalent (you can read about it in the textbook, as well) about getting data from a REST API even more malleable to new situations.

Being aware of how to use and configure various workarounds will help you be less constricted by — confusing documentation, or thorough authentication requirements, for example.


## A few ways we’ll/you’ll examine today
- using the `requests_oauthlib` library to complete the circumventing process explained above
  - for OAuth 1 (Twitter, Tumblr) — we’ve shown a Twitter example
  - for OAuth 2 (Spotify, Eventbrite) — we’ve shown a Spotify example (and a Facebook example)
- running a **local server** from your computer to play the role of “your web server” to get data and use it in your local program — relying on an external library
- using API wrapper libraries (sometimes in concert with these other methods, e.g. `spotipy` (https://github.com/plamere/spotipy ) and `tweepy` (the latter you may have used before. Docs are here: http://www.tweepy.org/ and there are some code examples on Canvas; see `tweepy_examples.py`) that help you avoid additional authentication complication
  - This is a bit more similar to code you’ve seen before than the other ways, so we’re going to focus on those first
  - A warning, though: sometimes it sounds really nice to try a special library built just for this!
    - First: pay attention to the documentation — is it good? Does it answer your questions?
    - Do a lot of people/projects seem to use it? Are there relatively easy examples to try? If so, might be nice.
    -  If not… might not be worth sinking time into.
- There are also other oAuth help libraries, like `rauth`, which you can also use/install: http://rauth.readthedocs.io/en/latest/  (similar to requests_oauthlib)
# Local servers (FYI)

You’ll see a little bit more of this in a couple weeks… mostly, something to be aware of now.

After you have `cd` -ed to a directory that contains at least one text (.txt) or .py file, try running the following at the command prompt:


    python -m http.server

*(You’ll need to be running Python 3 for this, so if you need to, type* `*python3*` *instead of* `*python*` *— you can do a similar thing in Python 2, but it is a different command.)*

Then in a browser, go to:


    http://localhost:8000

What do you see?
Why?

**What’s happening here?** You’re running a local server on a default port (in this case, 8000). *Basically*…

(You can exit this projection of a local server on port 8000 by pressing `Control` + `C` — Control even if you’re on a mac)

Before we get back to that, today we’ll take a look at some other example code (— one piece of which, later on, relies on this concept).

All files referred to can be found on Canvas, in **Files > Lecture 9**.


# An OAuth1 example (with complex caching)

`oauth1_twitter_caching.py`

Brief overview…

Before running/using it, you’ll need to download `secret_data_example.py`, follow the instructions in it (you’ll need a twitter account, even if you never use it again… and you’ll have to follow some instructions to create a Twitter application), and rename that file to `secret_data.py` in the same directory.

**Questions**

- What does that `if __name__ == "__main__"` line do? Why is it here?
- What is `import secret_data` doing?
- How would you describe the caching system included here in English? How is it different from the one you saw in section 6 for the New York Times API?
- What type is the variable `oauth1_inst`?
- Using the provided functionality, how could you make a request to the Twitter API for 5 tweets that include “@umsi” at the end of the file? And print out each of those tweets’ text?
  - Also check out: https://developer.twitter.com/en/docs/tweets/search/api-reference/get-search-tweets.html

**Note:** Consider — e.g. for Project 5 — You could use a lot of *very* similar functionality for the Tumblr API! What things would you definitely have to change to get access to the Tumblr API instead?

- About the code overall? (Also consider: what could stay the same? It’s a lot…)
- About the invocations at the end of the file?


# An OAuth2 example

Download:

- `spotify_oauth2_example.py`
- `spotify_data.py` (Follow instructions in this file and edit/save it in same directory)

You’ll need a Spotify account for this as well, but it doesn’t have to be real (it won’t be very interesting data if you haven’t used the account at first, but that’s OK), and you’ll have to follow some instructions to create an application in the Spotify account.

Let’s show an example of this working — what did I have to do to make this work?

**Questions**

- What does the `redirect_uri` mean? What is it doing? Why do we need it, even though we’re running code on a personal computer, not a web server?
- What type is the variable `oauth2inst`?
- Could you make requests to other URLs for spotify? (check out https://developer.spotify.com/web-api/endpoint-reference/ )
- What would need to change if you wanted to use this process for a different API?


# Another OAuth2 example

Relying on some external libraries
You’ll need to install `spotipy` and `tornado` with pip…

Download:

- `sam_oauth_util.py`
- `sam_spotify_example.py` (And read the comments and instructions in it)

Make sure you’ve updated your Application on Spotify properly.

Then try running it!

**What’s different between this example and the previous OAuth2 example? What’s similar?**


# A Facebook example [01/18: NOW OUTDATED]

You’ll need a FB account, and will need to create an application. Go to https://developers.facebook.com

(Of course, instead of the data shown in this example, you should put in your own equivalent data. In most cases, stuff like names of applications can be anything within certain rules, as long as it is unique, etc.)

![](https://www.dropbox.com/s/zw54dfw8zyvd3p7/Screenshot%202017-04-03%2013.28.17.png?dl=1)


On the top right, under “My Apps”, click “Add a new App”


![](https://www.dropbox.com/s/qtmm2c15dmd6uka/Screenshot%202017-04-03%2013.29.07.png?dl=1)


Create a new App ID


![](https://www.dropbox.com/s/fpl14j3d5gb8dbg/Screenshot%202017-04-03%2013.29.42.png?dl=1)


That will lead you to a page like this:


![](https://www.dropbox.com/s/mzuzubbbvzsum5b/Screenshot%202017-04-03%2013.30.12.png?dl=1)


On the left, click **Settings**

![](https://www.dropbox.com/s/ohfgjuatmqkp8or/Screenshot%202017-04-03%2013.32.52.png?dl=1)


Click “+ Add Platform” and select “Website”

![](https://www.dropbox.com/s/0stwjvd48756wpe/Screenshot%202017-04-03%2015.53.19.png?dl=1)




- Add “www.programsinformationpeople.org” to “App Domains”
- Set Site URL to: https://www.programsinformationpeople.org/runestone/oauth
  - Our special “OAuth2 redirect URL” again!
![](https://www.dropbox.com/s/6zcbvgctv2v6p5m/Screenshot%202017-04-03%2013.34.04.png?dl=1)



Copy your **app ID** and **app secret** into your python file, like so:


![](https://www.dropbox.com/s/w5sn057uzah0l2v/Screenshot%202017-04-03%2013.35.16.png?dl=1)


(note: this code uses OAuth 2, which is slightly more concise than OAuth 1, as you already saw with the Spotify examples)
On Canvas as `facebook_example.py`,,,

    __author__ = "Steve Oney"

    import json
    import webbrowser
    import unittest
    from requests_oauthlib import OAuth2Session
    from requests_oauthlib.compliance_fixes import facebook_compliance_fix # special for Facebook!

    APP_ID     = '<put your app id here>' # or use a secret data file
    APP_SECRET = '<put your app secret here>' # or use a secret data file
    facebook_session = False

    def makeFacebookRequest(baseURL, params = {}):
        global facebook_session # makes this a global variable, not just in the function scope
        if not facebook_session:
            # OAuth endpoints given in the Facebook API documentation
            authorization_base_url = 'https://www.facebook.com/dialog/oauth'
            token_url = 'https://graph.facebook.com/oauth/access_token'
            redirect_uri = 'https://www.programsinformationpeople.org/runestone/oauth'

            scope = ['user_posts','pages_messaging','user_managed_groups','user_status','user_likes'] # What do we want the app to be able to access?
            facebook = OAuth2Session(APP_ID, redirect_uri=redirect_uri, scope=scope)
            facebook_session = facebook_compliance_fix(facebook)

            authorization_url, state = facebook_session.authorization_url(authorization_base_url)
            print('Opening browser to {} for authorization'.format(authorization_url))
            webbrowser.open(authorization_url)

            redirect_response = input('Paste the full redirect URL here: ')
            facebook_session.fetch_token(token_url, client_secret=APP_SECRET, authorization_response=redirect_response.strip())

        return facebook_session.get(baseURL, params=params)

Try it out, in that file:


    makeFacebookRequest('https://graph.facebook.com/me') # If you have data in your FB profile at all


    print(makeFacebookRequest('https://graph.facebook.com/me').text)

Of course, again — this code does not employ caching.

But you could consider: how would you add it?


# Wrapper functions: the idea
- A useful tool for code organization
- Sometimes you want a function to return plain old data — but you want to “wrap it in something”
  - Clarity
  - Additional info
  - Maybe the values it returns could apply to many situations
  - Maybe you want to apply a conditional to them

For example, on your midterm…

- A function to display the player names — invoke the game and then display the scores!
- The game function you wrote does most of the work, returns a tuple of numbers
  - Wrapper function might — e.g. print “The winning score is…”
  - Or whatever you wanted it to do
- All about the program design!
- Always depends on a number of factors.
- Rarely ONE right answer. (People will argue)


# (if time) itertools & collections

Super useful tools for writing complex programs with containers and various types of iteration.

**Itertools:** https://docs.python.org/3/library/itertools.html
**Collections:** https://docs.python.org/3/library/collections.html

( Plus another fairly nice reading on iterators and generators, just for your edification: http://sahandsaba.com/python-iterators-generators.html )

## Exercises
- You want to create a dictionary that shows lists of letters that might come after another letter   — what from `collections` might be useful?
- You want to create reasonable groups in a class, knowing student names and preferred project types — what from `collections` or `itertools` might be useful?
- You want to  count off an enormous set in threes (dictionary paired with int 1 in a tuple, dictionary paired with int 2, dictionary paired with int 3, and so on for thousands of dictionaries) — what from `itertools` could help out with this?

Some cool examples here: https://www.blog.pythonlibrary.org/2016/04/20/python-201-an-intro-to-itertools/ and here: http://jmduke.com/posts/a-gentle-introduction-to-itertools/

Some programming challenges that these can often be useful for, if this is something you find fun: https://wiki.python.org/moin/ProblemSets
