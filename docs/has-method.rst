.. _has-method:

Has method
----------

A convenient function that returns TRUE if exists at least an element that satisfy the where condition specified calling the "where" method before this one.

  $db->where("user", $user);
  $db->where("password", md5($password));
  if($db->has("users")) {
      return "You are logged";
  } else {
      return "Wrong user/password";
  }