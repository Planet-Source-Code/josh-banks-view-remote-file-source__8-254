<div align="center">

## view remote file source


</div>

### Description

it will return the data of a specified file, could be used to view the source of a webpage or the output of a php file..
 
### More Info
 
$server

$file

returns $data.. which is the content of the file after being called using fsockopen


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Josh Banks](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/josh-banks.md)
**Level**          |Beginner
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |PHP 3\.0, PHP 4\.0
**Category**       |[Internet/ Browsers/ HTML](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/internet-browsers-html__8-9.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/josh-banks-view-remote-file-source__8-254/archive/master.zip)





### Source Code

```
<?php
  function get_source($server, $file = "")
  {
  $data = "";
  $query = "GET /$file HTTP/1.0";
  $fp = fsockopen($server, 80);
  if($fp)
  {
  fputs($fp, $query."\n\n");
  while(!feof($fp))
  {
  $data .= fread($fp, 1000);
  }
  fclose($fp);
  }
  return $data;
  }
  ?>
  <FORM>
  <INPUT TYPE=HIDDEN NAME=action VALUE="query">
  <font face="verdana,arial" size="1"><b>
  Server:<br><INPUT TYPE="text" NAME=server SIZE="40" VALUE="<?echo $server?>">(no http://)<br>
  Specific file:<br><INPUT TYPE="text" NAME="file" SIZE="40">(ie. index.html) <br>
  <INPUT TYPE=SUBMIT VALUE=" View Source! ">
  </FORM>
  <?php
  if($action=="query")
  {
  $data = get_source($server, $file);
  echo "<font face=\"tahoma\" size=\"2\"></b>Connected To <b>$server</b> on port 80.<br>";
  echo "Source of <b>$file</b>: <p><pre><textarea cols=75 rows=25 wrap=\"virtual\">$data</textarea></p></pre>";
  }
  ?>
```

