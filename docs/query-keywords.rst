.. _query-keywords:

Query Keywords
--------------

To add LOW PRIORITY | DELAYED | HIGH PRIORITY | IGNORE and the rest of the mysql keywords to INSERT (), REPLACE (), GET (), UPDATE (), DELETE() method or FOR UPDATE | LOCK IN SHARE MODE into SELECT ():

  $db->setQueryOption ('LOW_PRIORITY')->insert ($table, $param);
  // GIVES: INSERT LOW_PRIORITY INTO table ...

  $db->setQueryOption ('FOR UPDATE')->get ('users');
  // GIVES: SELECT * FROM USERS FOR UPDATE;

Also you can use an array of keywords:

  $db->setQueryOption (Array('LOW_PRIORITY', 'IGNORE'))->insert ($table,$param);
  // GIVES: INSERT LOW_PRIORITY IGNORE INTO table ...

Same way keywords could be used in SELECT queries as well:

  $db->setQueryOption ('SQL_NO_CACHE');
  $db->get("users");
  // GIVES: SELECT SQL_NO_CACHE * FROM USERS;

Optionally you can use method chaining to call where multiple times without referencing your object over an over:

  $results = $db
      ->where('id', 1)
      ->where('login', 'admin')
      ->get('users');