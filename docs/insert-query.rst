.. _insert-query:

Insert Query
------------

Simple Example
~~~~~~~~~~~~~~

  $data = Array ("login" => "admin",
                 "firstName" => "John",
                 "lastName" => 'Doe'
  );
  $id = $db->insert ('users', $data);
  if($id)
      echo 'user was created. Id=' . $id;

Insert with functions use

  $data = Array (
      'login' => 'admin',
      'active' => true,
      'firstName' => 'John',
      'lastName' => 'Doe',
      'password' => $db->func('SHA1(?)',Array ("secretpassword+salt")),
      // password = SHA1('secretpassword+salt')
      'createdAt' => $db->now(),
      // createdAt = NOW()
      'expires' => $db->now('+1Y')
      // expires = NOW() + interval 1 year
      // Supported intervals [s]econd, [m]inute, [h]hour, [d]day, [M]onth, [  Y]ear
  );

  $id = $db->insert ('users', $data);
  if ($id)
      echo 'user was created. Id=' . $id;
  else
      echo 'insert failed: ' . $db->getLastError();

Insert with on duplicate key update
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

  $data = Array ("login" => "admin",
                 "firstName" => "John",
                 "lastName" => 'Doe',
                 "createdAt" => $db->now(),
                 "updatedAt" => $db->now(),
  );
  $updateColumns = Array ("updatedAt");
  $lastInsertId = "id";
  $db->onDuplicate($updateColumns, $lastInsertId);
  $id = $db->insert ('users', $data);

Replace Query
~~~~~~~~~~~~~

Replace() method implements same API as insert();