---
title: Tipos de cursor (SQLSRV Driver) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8472d839-8124-4a62-a83c-7e771b0d4962
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 763795618eb90fe24db313b801bc01af3cd6737b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928036"
---
# <a name="cursor-types-sqlsrv-driver"></a>Tipos de cursor (driver SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

O driver SQLSRV permite que você crie um conjunto de resultados com linhas que pode acessar em qualquer ordem, dependendo do tipo de cursor.  Este tópico discutirá os cursores do lado do cliente (em buffer) e do lado do servidor (sem buffer).  
  
## <a name="cursor-types"></a>Tipos de cursor  
Ao criar um conjunto de resultados com [sqlsrv_query](../../connect/php/sqlsrv-query.md) ou com [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md), você pode especificar o tipo de cursor. Por padrão, um cursor de somente avanço é usado, o que permite que você mova uma linha por vez, começando na primeira linha do conjunto de resultados até chegar ao final do conjunto de resultados.  
  
Você pode criar um conjunto de resultados com um cursor rolável, que permite acessar qualquer linha no conjunto de resultados, em qualquer ordem. A tabela a seguir lista os valores que podem ser passados para a opção **Scrollable** em sqlsrv_query ou sqlsrv_prepare.  
  
|Opção|DESCRIÇÃO|  
|----------|---------------|  
|SQLSRV_CURSOR_FORWARD|Permite que você mova uma linha por vez, começando na primeira linha do conjunto de resultados até chegar ao final do conjunto de resultados.<br /><br />Esse é o tipo de cursor padrão.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) retorna um erro para conjuntos de resultados criados com esse tipo de cursor.<br /><br />**forward** é a forma abreviada de SQLSRV_CURSOR_FORWARD.|  
|SQLSRV_CURSOR_STATIC|Permite acessar linhas em qualquer ordem, mas não refletirá alterações no banco de dados.<br /><br />**static** é a forma abreviada de SQLSRV_CURSOR_STATIC.|  
|SQLSRV_CURSOR_DYNAMIC|Permite acessar linhas em qualquer ordem e refletirá alterações no banco de dados.<br /><br />[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md) retorna um erro para conjuntos de resultados criados com esse tipo de cursor.<br /><br />**dynamic** é a forma abreviada de SQLSRV_CURSOR_DYNAMIC.|  
|SQLSRV_CURSOR_KEYSET|Permite que você acesse linhas em qualquer ordem. Porém, um cursor de conjunto de chaves não atualizará a contagem de linhas se uma linha for excluída da tabela (uma linha excluída será retornada sem valores).<br /><br />**keyset** é a forma abreviada de SQLSRV_CURSOR_KEYSET.|  
|SQLSRV_CURSOR_CLIENT_BUFFERED|Permite que você acesse linhas em qualquer ordem. Cria uma consulta de cursor do lado do cliente.<br /><br />**buffered** é a forma abreviada de SQLSRV_CURSOR_CLIENT_BUFFERED.|  
  
Se uma consulta gerar vários conjuntos de resultados, a opção **Scrollable** se aplicará a todos eles.  
  
## <a name="selecting-rows-in-a-result-set"></a>Selecionar todas as linhas em um conjunto de resultados  
Depois de criar um conjunto de resultados, você pode usar [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md), [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md) ou [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) para especificar uma linha.  
  
A tabela a seguir lista e descreve os valores que podem ser especificados no parâmetro *row*.  
  
|Parâmetro|DESCRIÇÃO|  
|-------------|---------------|  
|SQLSRV_SCROLL_NEXT|Especifica a próxima linha. Esse será o valor padrão se você não especificar o parâmetro *row* para um conjunto de resultados rolável.|  
|SQLSRV_SCROLL_PRIOR|Especifica a linha imediatamente anterior à linha atual.|  
|SQLSRV_SCROLL_FIRST|Especifica a primeira linha no conjunto de resultados.|  
|SQLSRV_SCROLL_LAST|Especifica a última linha no conjunto de resultados.|  
|SQLSRV_SCROLL_ABSOLUTE|Especifica a linha especificada com o parâmetro *offset*.|  
|SQLSRV_SCROLL_RELATIVE|Especifica a linha especificada com o parâmetro *offset* da linha atual.|  
  
## <a name="server-side-cursors-and-the-sqlsrv-driver"></a>Cursores do lado do servidor e o driver SQLSRV  
O exemplo a seguir mostra o efeito dos diversos cursores. Na linha 33 do exemplo, vê-se a primeira de três instruções de consulta que especificam cursores diferentes.  Duas das instruções de consulta estão comentadas. Cada vez que você executar o programa, use um tipo de cursor diferente para ver o efeito da atualização de banco de dados na linha 47.  
  
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
  
## <a name="client-side-cursors-and-the-sqlsrv-driver"></a>Cursores do lado do cliente e o driver SQLSRV  
Os cursores do lado do cliente são um recurso adicionado na versão 3.0 do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] que permite armazenar em cache na memória todo um conjunto de resultados. A contagem de linhas está disponível após a consulta ser executada ao usar um cursor do lado do cliente.  
  
Os cursores do lado do cliente devem ser usados para conjuntos de resultados pequeno a médio porte. Use cursores do lado do servidor para conjuntos de resultados de grande porte.  
  
Uma consulta retornará false se o buffer não for grande o suficiente para conter todo o conjunto de resultados. Você pode aumentar o tamanho do buffer até o limite de memória do PHP.  
  
Usando o driver SQLSRV, você pode configurar o tamanho do buffer que contém o conjunto de resultados com a configuração ClientBufferMaxKBSize para [sqlsrv_configure](../../connect/php/sqlsrv-configure.md). [sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md) retorna o valor de ClientBufferMaxKBSize. Você também pode definir o tamanho máximo do buffer no arquivo php.ini com sqlsrv.ClientBufferMaxKBSize (por exemplo, sqlsrv.ClientBufferMaxKBSize = 1024).  
  
O exemplo a seguir mostra:  
  
-   A contagem de linhas está sempre disponível com um cursor do lado do cliente.  
  
-   O uso de cursores do lado do cliente e instruções em lote.  
  
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
  
O exemplo a seguir mostra um cursor do lado do cliente usando [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) e tamanho do buffer de cliente diferente.
  
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
$stmt = sqlsrv_prepare( $conn, $tsql, array(), array("Scrollable" => SQLSRV_CURSOR_CLIENT_BUFFERED, "ClientBufferMaxKBSize" => 51200));
  
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
  
## <a name="see-also"></a>Consulte Também  
[Especificando um tipo de cursor e selecionando linhas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md)  
  
