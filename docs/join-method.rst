.. _join-method:

JOIN method
-----------

  $db->join("users u", "p.tenantID=u.tenantID", "LEFT");
  $db->where("u.id", 6);
  $products = $db->get ("products p", null, "u.name, p.productName");
  print_r ($products);