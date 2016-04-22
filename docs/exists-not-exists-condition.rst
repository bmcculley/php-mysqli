.. _exists-not-exists-condition:

EXISTS / NOT EXISTS condition
-----------------------------

  $sub = $db->subQuery();
      $sub->where("company", 'testCompany');
      $sub->get ("users", null, 'userId');
  $db->where (null, $sub, 'exists');
  $products = $db->get ("products");
  // Gives SELECT * FROM products WHERE EXISTS (select userId from users where company='testCompany')