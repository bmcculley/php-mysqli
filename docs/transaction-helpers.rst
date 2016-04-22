.. _transaction-helpers:

Transaction helpers
-------------------

Please keep in mind that transactions are working on innoDB tables. Rollback transaction if insert fails:

  $db->startTransaction();
  ...
  if (!$db->insert ('myTable', $insertData)) {
      //Error while saving, cancel new record
      $db->rollback();
  } else {
      //OK
      $db->commit();
  }

Query exectution time benchmarking
----------------------------------

To track query execution time setTrace() function should be called.

  $db->setTrace (true);
  // As a second parameter it is possible to define prefix of the path which should be striped from filename
  // $db->setTrace (true, $_SERVER['SERVER_ROOT']);
  $db->get("users");
  $db->get("test");
  print_r ($db->trace);

    [0] => Array
        (
            [0] => SELECT  * FROM t_users ORDER BY `id` ASC
            [1] => 0.0010669231414795
            [2] => MysqliDb->get() >>  file "/avb/work/PHP-MySQLi-Database-Class/tests.php" line #151
        )

    [1] => Array
        (
            [0] => SELECT  * FROM t_test
            [1] => 0.00069189071655273
            [2] => MysqliDb->get() >>  file "/avb/work/PHP-MySQLi-Database-Class/tests.php" line #152
        )

