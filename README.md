# Story Engine

## TODOS:
* Clean up php code style
* Create smart modular bits and store them in smart locations
* Fix typography design here and there

A build-your-own-adventure making app built with php 5.5.38

### Install Locally
Detailed explanations for these steps follow:
1. Clone the repo
2. Start servers running php 5.5.* (preferably 5.5.38)
3. Create a new mysql database and add the required tables and rows.
4. Open browser, go to the new localsite, and register as a new user.
5. If you'd like, give the user admin privileges.

**Clone the repo**
```
git clone https://github.com/akiryk/storyengine.git
```

**Start servers**
If using MAMP, select php version 5.5.* and start servers.

**Create a new mySql database**
Call it "story_engine" (or whatever you'd like). If using phpMyAdmin, leave default setting as `collation` .

**Create tables and rows for the database**
*Start mysql from command line if using MAMP on a Mac:*
```
/Applications/MAMP/Library/bin/mysql --host=localhost -u root -p
```
*Start mysql from command line on Mac not using MAMP:*
```
/usr/local/mysql/bin/mysql -u root -p
USE story_engine
```
*If you'd like to clear out existing tables and rows beforehand:*
```
USE story_engine
DROP TABLE users, stories, stories_users, chapters, story_chapter, options, chapter_option;
```
*Add tables and rows to the DB:*
```
CREATE TABLE users (
  id MEDIUMINT NOT NULL AUTO_INCREMENT,
  firstname CHAR (30) NOT NULL,
  lastname CHAR (30) NOT NULL,
  username CHAR (30) NOT NULL,
  hashed_password CHAR (40) NOT NULL,
  admin TINYINT DEFAULT NULL,
  PRIMARY KEY (id)
);

CREATE TABLE stories (
  id INT NOT NULL AUTO_INCREMENT,
  title VARCHAR (40) NOT NULL,
  first_chapter INT DEFAULT NULL,
  PRIMARY KEY (id)
);

CREATE TABLE stories_users (
  id INT NOT NULL AUTO_INCREMENT,
  story_id INT NOT NULL,
  user_id INT NOT NULL,
  PRIMARY KEY (id)
);

CREATE TABLE chapters (
  id INT NOT NULL AUTO_INCREMENT,
  content TEXT,
  beginning INT,
  endpoint INT,
  level INT,
  PRIMARY KEY (id)
);

CREATE TABLE story_chapter (
  id INT NOT NULL AUTO_INCREMENT,
  story_id INT,
  chapter_id INT,
  PRIMARY KEY (id)
);

CREATE TABLE options (
  id INT NOT NULL AUTO_INCREMENT,
  child_chapter INT DEFAULT 0,
  content VARCHAR (60),
  PRIMARY KEY (id)
);

CREATE TABLE chapter_option (
  id INT NOT NULL AUTO_INCREMENT,
  chapter_id INT,
  option_id INT,
  PRIMARY KEY (id)
);
```
*Register a new user on the site*
* Using phpMyAdmin: Change `admin` row to 1.
* In terminal: `UPDATE users SET admin = NULL WHERE id = 1;`

### Copy to remote server
1. Make sure that c/constants.php data are correct, e.g, check on server to ensure each of the constants works.
2. Copy to server.