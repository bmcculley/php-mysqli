.. _initialization:

Initialization
--------------

Simple initialization with utf8 charset set by default:

  $db = new MysqliDb ('host', 'username', 'password', 'databaseName');

### Advanced initialization:

  $db = new MysqliDb (Array (
                'host' => 'host',
                'username' => 'username', 
                'password' => 'password',
                'db'=> 'databaseName',
                'port' => 3306,
                'prefix' => 'my_',
                'charset' => 'utf8'));

table prefix, port and database charset params are optional. If no charset should be set charset, set it to null

Also it is possible to reuse already connected mysqli object:

  $mysqli = new mysqli ('host', 'username', 'password', 'databaseName');
  $db = new MysqliDb ($mysqli);

If no table prefix were set during object creation its possible to set it later with a separate call:

$db->setPrefix ('my_');

If you need to get already created mysqliDb object from another class or function use

    function init () {
        // db staying private here
        $db = new MysqliDb ('host', 'username', 'password', 'databaseName');
    }
    ...
    function myfunc () {
        // obtain db object created in init  ()
        $db = MysqliDb::getInstance();
        ...
    }