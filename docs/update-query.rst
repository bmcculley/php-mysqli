.. _update-query:

Update Query
------------

  $data = Array (
      'firstName' => 'Bobby',
      'lastName' => 'Tables',
      'editCount' => $db->inc(2),
      // editCount = editCount + 2;
      'active' => $db->not()
      // active = !active;
  );
  $db->where ('id', 1);
  if ($db->update ('users', $data))
      echo $db->count . ' records were updated';
  else
      echo 'update failed: ' . $db->getLastError();

update() also support limit parameter:

  $db->update ('users', $data, 10);
  // Gives: UPDATE users SET ... LIMIT 10