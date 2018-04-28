---
title: Tipos de cursor (Driver SQLSRV) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c95beace96484b53d6786f8df24b55878a1ab8e2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="cursor-types-sqlsrv-driver"></a>Tipos de cursor (Driver SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

O driver SQLSRV permite que você crie um conjunto de resultados com linhas que você pode acessar em qualquer ordem, dependendo do tipo de cursor.  Este tópico descreverá (em buffer) do cliente e do servidor (sem buffer) cursores.  
  
## <a name="cursor-types"></a>Tipos de cursor  
Quando você cria um conjunto de resultados com [sqlsrv_query](../../connect/php/sqlsrv-query.md) ou com [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md), você pode especificar o tipo de cursor. Por padrão, um cursor somente de avanço é usado, o que permite mover uma linha por vez, começando na primeira linha do resultado definido até chegar ao final do conjunto de resultados.  
  
Você pode criar um conjunto de resultados com um cursor rolável, o que permite que você acesse qualquer linha no conjunto de resultados, em qualquer ordem. A tabela a seguir lista os valores que podem ser passados para o **rolável** opção sqlsrv_query ou sqlsrv_prepare.  
  
|Opção|Description|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|Permite mover uma linha por vez, começando na primeira linha do resultado definido até chegar ao final do conjunto de resultados.<br /><br />Este é o tipo de cursor padrão.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) retorna um erro para conjuntos de resultados criados com esse tipo de cursor.<br /><br />**Encaminhar** é a forma abreviada de SQLSRV_CURSOR_FORWARD.|  
|SQLSRV_CURSOR_STATIC|Permite acessar linhas em qualquer ordem, mas não refletirá as alterações no banco de dados.<br /><br />**estático** é a forma abreviada de SQLSRV_CURSOR_STATIC.|  
|SQLSRV_CURSOR_DYNAMIC|Permite que você acessar linhas em qualquer ordem e que refletirá as alterações no banco de dados.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) retorna um erro para conjuntos de resultados criados com esse tipo de cursor.<br /><br />**dinâmico** é a forma abreviada de SQLSRV_CURSOR_DYNAMIC.|  
|SQLSRV_CURSOR_KEYSET|Permite acessar linhas em qualquer ordem. No entanto, um cursor de conjunto de chaves não atualiza a contagem de linhas se uma linha for excluída da tabela (uma linha excluída será retornada sem valores).<br /><br />**conjunto de chaves** é a forma abreviada de SQLSRV_CURSOR_KEYSET.|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|Permite acessar linhas em qualquer ordem. Cria uma consulta de cursor do lado do cliente.<br /><br />**com buffer** é a forma abreviada de SQLSRV_CURSOR_CLIENT_BUFFERED.|  
  
Se uma consulta gera vários conjuntos de resultados, o **rolável** opção se aplica a todos os conjuntos de resultados.  
  
## <a name="selecting-rows-in-a-result-set"></a>Selecionar linhas em um conjunto de resultados  
Depois de criar um conjunto de resultados, você pode usar [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md), [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md), ou [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) para especificar uma linha.  
  
A tabela a seguir descreve os valores que você pode especificar o *linha* parâmetro.  
  
|Parâmetro|Description|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|Especifica a próxima linha. Este é o valor padrão, se você não especificar o *linha* parâmetro para um conjunto de resultados roláveis.|  
|SQLSRV_SCROLL_PRIOR|Especifica a linha antes da linha atual.|  
|SQLSRV_SCROLL_FIRST|Especifica a primeira linha no conjunto de resultados.|  
|SQLSRV_SCROLL_LAST|Especifica a última linha no conjunto de resultados.|  
|SQLSRV_SCROLL_ABSOLUTE|Especifica a linha especificada com o *deslocamento* parâmetro.|  
|SQLSRV_SCROLL_RELATIVE|Especifica a linha especificada com o *deslocamento* parâmetro da linha atual.|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>Cursores do lado do servidor e o Driver SQLSRV  
O exemplo a seguir mostra o efeito dos cursores de vários. Linha 33 do exemplo, você vê a primeira das três instruções de consulta que especificam cursores diferentes.  Duas das instruções de consulta são comentadas. Cada vez que você executar o programa, use um tipo de cursor diferente para ver o efeito da atualização do banco de dados na linha 47.  
  
```  
<?php  
$server = "server_name";  
$conn = sqlsrv_connect( $server, array( 'Database' => 'test' ));  
if ( $conn === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "DROP TABLE dbo.ScrollTest" );  
if ( $stmt !== false ) {   
   sqlsrv_free_stmt( $stmt );   
}  
  
$stmt = sqlsrv_query( $conn, "CREATE TABLE ScrollTest (id int, value char(10))" );  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 1, "Row 1" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 2, "Row 2" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "INSERT INTO ScrollTest (id, value) VALUES(?,?)", array( 3, "Row 3" ));  
if ( $stmt === false ) {  
   die( print_r( sqlsrv_errors(), true ));  
}  
  
$stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'keyset' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'dynamic' ));  
// $stmt = sqlsrv_query( $conn, "SELECT * FROM ScrollTest", array(), array( "Scrollable" => 'static' ));  
  
$rows = sqlsrv_has_rows( $stmt );  
if ( $rows != true ) {  
   die( "Should have rows" );  
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
$stmt2 = sqlsrv_query( $conn, "delete from ScrollTest where id = 3" );  
// or  
// $stmt2 = sqlsrv_query( $conn, "UPDATE ScrollTest SET id = 4 WHERE id = 3" );  
if ( $stmt2 !== false ) {   
   sqlsrv_free_stmt( $stmt2 );   
}  
  
$result = sqlsrv_fetch( $stmt, SQLSRV_SCROLL_LAST );  
$field1 = sqlsrv_get_field( $stmt, 0 );  
$field2 = sqlsrv_get_field( $stmt, 1 );  
echo "\n$field1 $field2\n";  
  
sqlsrv_free_stmt( $stmt );  
sqlsrv_close( $conn );  
?>  
```  
  
## <a name="client-side-cursors-and-the-sqlsrv-driver"></a>Cursores do lado do cliente e o Driver SQLSRV  
Cursores do lado do cliente são um recurso adicionado na versão 3.0 do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] que permite que você armazene um todo conjunto de resultados na memória. Contagem de linhas está disponível depois que a consulta é executada ao usar um cursor do lado do cliente.  
  
Cursores do lado do cliente devem ser usados para conjuntos de resultados de pequeno a médio porte. Use cursores do lado do servidor para grandes conjuntos de resultados.  
  
Uma consulta retornará false se o buffer não é grande o suficiente para conter o conjunto de resultados inteiro. Você pode aumentar o tamanho do buffer até o limite de memória do PHP.  
  
Usando o driver SQLSRV, você pode configurar o tamanho do buffer que contém o conjunto de resultados com a configuração ClientBufferMaxKBSize [sqlsrv_configure](../../connect/php/sqlsrv-configure.md). [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md) retorna o valor de ClientBufferMaxKBSize. Você também pode definir o tamanho máximo do buffer no arquivo php.ini com sqlsrv. ClientBufferMaxKBSize (por exemplo, sqlsrv. ClientBufferMaxKBSize = 1024).  
  
O exemplo a seguir mostra:  
  
-   Contagem de linhas sempre está disponível com um cursor do lado do cliente.  
  
-   Uso de cursores do lado do cliente e instruções em lote.  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Department";  
  
// Execute the query with client-side cursor.  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// row count is always available with a client-side cursor  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count = $row_count\n";  
  
// Move to a specific row in the result set.  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
// Client-side cursor and batch statements  
$tsql = "select top 2 * from HumanResources.Employee;Select top 3 * from HumanResources.EmployeeAddress";  
  
$stmt = sqlsrv_query($conn, $tsql, array(), array("Scrollable"=>"buffered"));  
if (! $stmt) {  
   echo "Error in statement execution.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for first result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
  
sqlsrv_next_result($stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
echo "\nRow count for second result set = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_LAST);  
$EmployeeID = sqlsrv_get_field( $stmt, 0);  
echo "Employee ID = $EmployeeID \n";  
?>  
```  
  
O exemplo a seguir mostra um cursor do lado do cliente usando [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
```  
<?php  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
$tsql = "select * from HumanResources.Employee";  
$stmt = sqlsrv_prepare( $conn, $tsql, array(), array("Scrollable"=>SQLSRV_CURSOR_CLIENT_BUFFERED));  
  
if (! $stmt ) {  
   echo "Statement could not be prepared.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_execute( $stmt);  
  
$row_count = sqlsrv_num_rows( $stmt );  
if ($row_count)  
   echo "\nRow count = $row_count\n";  
  
$row = sqlsrv_fetch($stmt, SQLSRV_SCROLL_FIRST);  
if ($row ) {  
   $EmployeeID = sqlsrv_get_field( $stmt, 0);  
   echo "Employee ID = $EmployeeID \n";  
}  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Especificando um tipo de cursor e selecionando linhas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
