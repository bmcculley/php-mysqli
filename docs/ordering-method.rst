.. _ordering-method:

Ordering method
---------------

  $db->orderBy("id","asc");
  $db->orderBy("login","Desc");
  $db->orderBy("RAND ()");
  $results = $db->get('users');
  // Gives: SELECT * FROM users ORDER BY id ASC,login DESC, RAND ();

Order by values example:

  $db->orderBy('userGroup', 'ASC', array('superuser', 'admin', 'users'));
  $db->get('users');
  // Gives: SELECT * FROM users ORDER BY FIELD (userGroup, 'superuser', 'admin', 'users') ASC;

If you are using setPrefix () functionality and need to use table names in orderBy() method make sure that table names are escaped with ``.

  $db->setPrefix ("t_");
  $db->orderBy ("users.id","asc");
  $results = $db->get ('users');
  // WRONG: That will give: SELECT * FROM t_users ORDER BY users.id ASC;

  $db->setPrefix ("t_");
  $db->orderBy ("`users`.id", "asc");
  $results = $db->get ('users');
  // CORRECT: That will give: SELECT * FROM t_users ORDER BY t_users.id ASC;