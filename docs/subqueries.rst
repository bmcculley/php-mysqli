.. _subqueries:

Subqueries
----------

Subquery init

Subquery init without an alias to use in inserts/updates/where Eg. (select * from users)

  $sq = $db->subQuery();
  $sq->get ("users");

A subquery with an alias specified to use in JOINs . Eg. (select * from users) sq

  $sq = $db->subQuery("sq");
  $sq->get ("users");

Subquery in selects:

  $ids = $db->subQuery ();
  $ids->where ("qty", 2, ">");
  $ids->get ("products", null, "userId");

  $db->where ("id", $ids, 'in');
  $res = $db->get ("users");
  // Gives SELECT * FROM users WHERE id IN (SELECT userId FROM products WHERE qty > 2)

Subquery in inserts:

  $userIdQ = $db->subQuery ();
  $userIdQ->where ("id", 6);
  $userIdQ->getOne ("users", "name"),

  $data = Array (
      "productName" => "test product",
      "userId" => $userIdQ,
      "lastUpdated" => $db->now()
  );
  $id = $db->insert ("products", $data);
  // Gives INSERT INTO PRODUCTS (productName, userId, lastUpdated) values ("test product", (SELECT name FROM users WHERE id = 6), NOW());

Subquery in joins:

  $usersQ = $db->subQuery ("u");
  $usersQ->where ("active", 1);
  $usersQ->get ("users");

  $db->join($usersQ, "p.userId=u.id", "LEFT");
  $products = $db->get ("products p", null, "u.login, p.productName");
  print_r ($products);
  // SELECT u.login, p.productName FROM products p LEFT JOIN (SELECT * FROM t_users WHERE active = 1) u on p.userId=u.id;

