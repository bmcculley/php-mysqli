.. _properties-sharing:

Properties sharing
------------------

Its is also possible to copy properties

  $db->where ("agentId", 10);
  $db->where ("active", true);

  $customers = $db->copy ();
  $res = $customers->get ("customers", Array (10, 10));
  // SELECT * FROM customers where agentId = 10 and active = 1 limit 10, 10

  $cnt = $db->getValue ("customers", "count(id)");
  echo "total records found: " . $cnt;
  // SELECT count(id) FROM users where agentId = 10 and active = 1