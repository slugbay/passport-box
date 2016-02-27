# Passport-box

[![NPM](https://nodei.co/npm/passport-box-standard.png?downloads=true)](https://nodei.co/npm/passport-box-standard/) [![NPM](https://nodei.co/npm-dl/passport-box-standard.png?months=5&height=2)](https://nodei.co/npm/passport-box-standard/)

[Passport](https://github.com/jaredhanson/passport) strategy for authenticating
with [Box](http://box.com/) using the OAuth 2.0 API.

This module lets you authenticate using box, in your Node.js applications.  
By plugging into Passport, Box
authentication can be easily and unobtrusively integrated into any application or
framework that supports [Connect](http://www.senchalabs.org/connect/)-style
middleware, including [Express](http://expressjs.com/).

## Install

    $ npm install passport-box-standard

## Usage

#### Configure Strategy

The box authentication strategy authenticates users using a box
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

The consumer key and secret are obtained by [creating an application](https://app.box.com/developers/services/edit/) at
Box's [developer](https://developers.box.com/) site.

```js
    passport.use(new BoxStrategy({
        clientID: BOX_CLIENT_ID,
        clientSecret: BOX_CLIENT_SECRET,
        callbackURL: "http://127.0.0.1:3000/auth/box/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ boxId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'box'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

```js
    app.get('/auth/box',
      passport.authenticate('box'));

    app.get('/auth/box/callback', 
      passport.authenticate('box', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });
```

## Examples

For a complete, working example, refer to the [login example](https://github.com/slugbay/passport-box/tree/master/example/login).

## Credits

  - Made with ♥ by [SlugBay](https://www.slugbay.com) engineers
    
  [![Screenshot](http://challengepost-s3-challengepost.netdna-ssl.com/photos/production/software_photos/000/332/858/datas/gallery.jpg)](https://www.slugbay.com)

## Thanks

  - [Jared Hanson](http://github.com/jaredhanson)

## License

  - [The MIT License](http://opensource.org/licenses/MIT)
