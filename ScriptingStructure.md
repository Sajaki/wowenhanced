#Shows how MangosWeb Enhanced is scripted.

## Mangosweb Scripting structure Documentation ##


## Style of code ##
On the CodingStyle page, you can find all about our code style requirements (be sure to read them before you commit your changes).


## Database connections ##

''Mangosweb uses the same database structure as the newest MaNGOS source. In MaNGOS source there are 3 databases, known as
World database, character and Realm database. Mangosweb uses them both to retrieve/update/add data.''

Mangosweb uses a database Class to retrieve and update data in databases. Classes to all of the databases that mangosweb is using are defined as
$WSDB, $CHDB and $DB. $WSDB is obiously the World database, $CHDB is the character database, and $DB is the realm database..

'''World database'''
Php variable: $WSDB->YOUR\_CLASS\_CALL
Desc: Connects and does what you want with the world database.

'''Characters Database'''
Php variable: $CHDB->YOUR\_CLASS\_CALL
Desc: connects and does what you want with the CHARACTER database.

'''Realm Database'''
Php variable: $DB->YOUR\_CLASS\_CALL
Desc: connects and does what you want with the REALM database.


'''Database Class information'''

''As known, MangosWeb uses a database class to do querys from the PHP scripts. Here are some basic explaination. ''[[BR](BR.md)]
Our example is, how to use $DB variable to get /update / delete things.[[BR](BR.md)]
From the table below you can see a table with the class function, here is an example of how to use it: "$DB->select("SELECT **FROM accounts");"[[BR](BR.md)]**

|ClassCall | Return Type | Return Detail | Further information|
|:---------|:------------|:--------------|:-------------------|
|select    |Array        | Returns the array generated from the database query | Use select if its more than one row that you want to get|
|selectRow | Array       |Returns the array generated from database query | Use selectRow if its only ONE (1) Row that you want out.|
|selectCell | String      | Returns the spesific Cell of database you want || Use selectCell if its only a Cell you want printed exm: SELECT id FROM account WHERE id=1|
|query     | Bool        | Returns TRUE or FALSE | Returns TRUE if query was OK , returns FALSE if querys was not OK, you can do all querys in here ( UPDATE / DELETE )|

'''Example 1: If you want to count how many accounts are on your server:'''[[BR](BR.md)]

```
$counting = $DB->select("SELECT id FROM accounts");
$total = count($counting);
echo $total;
```

'''Example 2: if you want to find how many characters the the user has and print it:'''[[BR](BR.md)]

```
$users_chars = $DB->selectCell("SELECT numchars FROM `realmcharacters` WHERE acctid=?d",$user['id']);
echo $users_chars;
```
<br />
OR
<br />
```
users_characters = $CHDB->select("SELECT guid FROM characters WHERE acctid='$user[id]'");
$total = count($users_chars);
echo $users_chars;
```

'''Example 3: Connecting to characters database; find all characters to the loggedin, make it an array and print name of all characters:'''[[BR](BR.md)]

```
$rows = $CHDB->select("SELECT `name` FROM `characters` WHERE online=1");
foreach($rows as $row){
echo $row['name'];
}
```



## Global Variables ##
''Global variables are variables who does not change, NEVER create a variable simular to these. Also please keep this list up to date.''
|Variable name|Variable type|What it does?|
|:------------|:------------|:------------|
|$user        |Array        |The variable user is defined as the logged in user, the user variable got all information that is stored in realm - >`account` table. Example: $user!['id'] holds what ID the user has, $user!['email'] holds the email to the user. If $user!['id'] = 0, this means that the user is not logged in.|
|`$_COOKIE['cur_selected_realmd']`|INT          |Holds information on what REALM to view. If user is logged on it depend on the "realm.account\_extend.viewing\_server" else its defined in config![realminfo](realminfo.md)[default\_realm\_id](default_realm_id.md).|
|`$_REQUEST['n']`|string       |This is used to request and show main categorys on screen|?            |
|`$_REQUEST['sub']`|string       |This is used to request and show Sub categorys on screen|?            |



To be continued.