# Spaced repetition WebApp

Welcome to the Spaced Repetition WebApp!

This webapp has serves to help with learning topics where spaced repetition has been shown to improve a user's ability to learn information by repeatedly being presented in 'flash card' style method. For example, many languages are learned using spaced repetition - hold up a card with a word, attempt to translate the word, and turn the card over to reveal the true translation on the other side!

This app works similarly by presenting the user with a word in a foreign language (in the deployed example, the fictional Klingon language is used, referencing the Klingon Pocket Dictionary), giving the user an input form to attempt to translate the word, and checking it against the true answer. It provides feedback for correct and incorrect answers, and will always reveal the correct answer after an attempt.

This Spaced Repetition WebApp allows a user to create a unique username and password, and will track correct and incorrect answers.

Though the deployed example is limited in scope, the list of words can be as long as the user likes. 

## API

While this API can run independently of the client and be used for a custom client, it is intended to be used with the accompanying Spaced Repetition Client.

### API Endpoints

`/api/user/` - `POST`
User creation endpoint. When supplied with the name, username, and password, a new user can be created.

`/api/auth/token/` - `POST`
Submitting a username and password will check against the database for authentication.

`/api/language/` - `GET`
This endpoint will return the name of the language, and the full list of nodes in the linked list.

`/api/language/head` - `GET`
This endpoint returns the next node in line in the linked list.

`/api/language/guess` - `POST`
This endpoint handles submissions of a user's attempt to translate the word.

## Client

The Spaced Repetition Client allows the user to interface with the app via a webpage.

The user can:

-Create a new account with a name, username, and password.
-Login to an existing account.
-View a list of words in the currently selected language.
-Begin spaced repetition practice.
-Attempt to answer prompts correctly.
-View the results of their attempted guess.
-Track the running total of correct guesses.
-Track correct and incorrect guesses for each word.
-Log out of the app.



## Local dev setup

If using user `dunder-mifflin`:

```bash
mv example.env .env
createdb -U dunder-mifflin spaced-repetition
createdb -U dunder-mifflin spaced-repetition-test
```

If your `dunder-mifflin` user has a password be sure to set it in `.env` for all appropriate fields. Or if using a different user, update appropriately.

```bash
npm install
npm run migrate
env MIGRATION_DB_NAME=spaced-repetition-test npm run migrate
```

And `npm test` should work at this point

## Configuring Postgres

For tests involving time to run properly, configure your Postgres database to run in the UTC timezone.

1. Locate the `postgresql.conf` file for your Postgres installation.
   1. E.g. for an OS X, Homebrew install: `/usr/local/var/postgres/postgresql.conf`
   2. E.g. on Windows, _maybe_: `C:\Program Files\PostgreSQL\11.2\data\postgresql.conf`
   3. E.g  on Ubuntu 18.04 probably: '/etc/postgresql/10/main/postgresql.conf'
2. Find the `timezone` line and set it to `UTC`:

```conf
# - Locale and Formatting -

datestyle = 'iso, mdy'
#intervalstyle = 'postgres'
timezone = 'UTC'
#timezone_abbreviations = 'Default'     # Select the set of available time zone
```

## Scripts

Start the application `npm start`

Start nodemon for the application `npm run dev`

Run the tests mode `npm test`

Run the migrations up `npm run migrate`

Run the migrations down `npm run migrate -- 0`
