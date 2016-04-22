.. _helper-methods:

Helper methods
--------------

Reconnect in case mysql connection died:

 if (!$db->ping())
     $db->connect()

Get last executed SQL query: Please note that function returns SQL query only for debugging purposes as its execution most likely will fail due missing quotes around char variables.

    $db->get('users');
    echo "Last executed query was ". $db->getLastQuery();

Check if table exists:

    if ($db->tableExists ('users'))
        echo "hooray";

mysqli_real_escape_string() wrapper:

    $escaped = $db->escape ("' and 1=1");