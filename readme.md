# Passport.js authentication for Apptrack

[Passport](http://passportjs.org/) strategy for authenticating with [Apptrack](https://apptrack.io/) using the OAuth 2.0 API.

This module lets you authenticate using Apptrack in your Node.js applications.

By plugging into Passport, Apptrack authentication can be easily and unobtrusively integrated into any application or framework that supports [Connect](http://www.senchalabs.org/connect/)-style middleware, including [Express](http://expressjs.com/).

## Install
```
npm install passport-apptrack
```

## Usage

#### Configure Strategy

The Apptrack authentication strategy authenticates users using a Apptrack account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which accepts these credentials and calls `done` providing a user, as well as `options` specifying a client ID, client secret, and callback URL.
```
passport.use(new ApptrackOAuth2Strategy({
	clientID: CLIENT_ID,
	clientSecret: CLIENT_SECRET,
	callbackURL: "https://www.example.net/auth/apptrack/callback"
	},
	function(accessToken, refreshToken, profile, done) {
	User.findOrCreate({ providerId: profile.id }, function (err, user) {
		return done(err, user);
	});
	}
));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'apptrack'` strategy, to authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/) application:

```
app.get('/auth/apptrack',
	passport.authenticate('apptrack'));

app.get('/auth/apptrack/callback',
	passport.authenticate('apptrack', { failureRedirect: '/login' }),
	function(req, res) {
	// Successful authentication, redirect home.
	res.redirect('/');
	});
```

## Credits

Initiated by [Makis Tracend](http://github.com/tracend)

Part of [Apptrack](http://apptrack.io/) by [K&D Interactive](http://kdi.co/)

Released under the [MIT license](http://makesites.org/licenses/MIT)

