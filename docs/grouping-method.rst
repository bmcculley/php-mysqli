.. _grouping-method:

Grouping method
---------------

  $db->groupBy ("name");
  $results = $db->get ('users');
  // Gives: SELECT * FROM users GROUP BY name;

Join table products with table users with LEFT JOIN by tenantID