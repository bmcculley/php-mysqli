.. _where-having-methods:

Where / Having Methods
----------------------

where(), orWhere(), having() and orHaving() methods allows you to specify where and having conditions of the query. All conditions supported by where() are supported by having() as well.

WARNING: In order to use column to column comparisons only raw where conditions should be used as column name or functions cant be passed as a bind variable.

Regular == operator with variables:

  $db->where ('id', 1);
  $db->where ('login', 'admin');
  $results = $db->get ('users');
  // Gives: SELECT * FROM users WHERE id=1 AND login='admin';

  $db->where ('id', 1);
  $db->having ('login', 'admin');
  $results = $db->get ('users');
  // Gives: SELECT * FROM users WHERE id=1 HAVING login='admin';

Regular == operator with column to column comparison:

  // WRONG
  $db->where ('lastLogin', 'createdAt');
  // CORRECT
  $db->where ('lastLogin = createdAt');
  $results = $db->get ('users');
  // Gives: SELECT * FROM users WHERE lastLogin = createdAt;

  $db->where ('id', 50, ">=");
  // or $db->where ('id', Array ('>=' => 50));
  $results = $db->get ('users');
  // Gives: SELECT * FROM users WHERE id >= 50;

BETWEEN / NOT BETWEEN:

  $db->where('id', Array (4, 20), 'BETWEEN');
  // or $db->where ('id', Array ('BETWEEN' => Array(4, 20)));

  $results = $db->get('users');
  // Gives: SELECT * FROM users WHERE id BETWEEN 4 AND 20

IN / NOT IN:

  $db->where('id', Array(1, 5, 27, -1, 'd'), 'IN');
  // or $db->where('id', Array( 'IN' => Array(1, 5, 27, -1, 'd') ) );

  $results = $db->get('users');
  // Gives: SELECT * FROM users WHERE id IN (1, 5, 27, -1, 'd');

OR CASE

  $db->where ('firstName', 'John');
  $db->orWhere ('firstName', 'Peter');
  $results = $db->get ('users');
  // Gives: SELECT * FROM users WHERE firstName='John' OR firstName='peter'

  $db->where ('firstName', 'John');
  $db->orWhere ('firstName', 'Peter');
  $results = $db->get ('users');
  // Gives: SELECT * FROM users WHERE firstName='John' OR firstName='peter'

NULL comparison:

  $db->where ("lastName", NULL, 'IS NOT');
  $results = $db->get("users");
  // Gives: SELECT * FROM users where lastName IS NOT NULL

Also you can use raw where conditions:

  $db->where ("id != companyId");
  $db->where ("DATE(createdAt) = DATE(lastLogin)");
  $results = $db->get("users");

Or raw condition with variables:

  $db->where ("(id = ? or id = ?)", Array(6,2));
  $db->where ("login","mike")
  $res = $db->get ("users");
  // Gives: SELECT * FROM users WHERE (id = 6 or id = 2) and login='mike';

Find the total number of rows matched. Simple pagination example:

  $offset = 10;
  $count = 15;
  $users = $db->withTotalCount()->get('users', Array ($offset, $count));
  echo "Showing {$count} from {$db->totalCount}";