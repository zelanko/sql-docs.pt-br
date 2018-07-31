---
title: 'PDO:: Prepare | Microsoft Docs'
ms.custom: ''
ms.date: 07/10/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 717657cabc469488565985e3e37d111bb9d592b8
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979761"
---
# <a name="pdoprepare"></a>PDO::prepare
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Prepara uma instrução para execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PDOStatement PDO::prepare ( $statement [, array(key_pair)] )  
```  
  
#### <a name="parameters"></a>Parâmetros  
$*statement*: uma cadeia de caracteres contendo a instrução SQL.  
  
*key_pair*: uma matriz contendo um nome e valor de atributo. Para obter mais informações, consulte a seção Comentários.  
  
## <a name="return-value"></a>Valor retornado  
Retorna um objeto PDOStatement em caso de êxito. Em caso de falha, retorna um objeto PDOException ou false, dependendo do valor de PDO::ATTR_ERRMODE.  
  
## <a name="remarks"></a>Remarks  
Os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] não avaliam instruções preparadas até a execução.  
  
A tabela a seguir mostra os valores possíveis de *key_pair*.  
  
|Chave|Descrição|  
|-------|---------------|  
|PDO::ATTR_CURSOR|Especifica o comportamento do cursor. O padrão é PDO::CURSOR_FWDONLY. PDO::CURSOR_SCROLL é um cursor estático.<br /><br />Por exemplo, `array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY )`.<br /><br />Se você usar PDO::CURSOR_SCROLL, pode usar PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE, descrito abaixo.<br /><br />Veja [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md) para obter mais informações sobre conjuntos de resultados e cursores no driver PDO_SQLSRV.|  
|PDO::ATTR_EMULATE_PREPARES|Quando PDO:: attr_emulate_prepares está habilitada, os espaços reservados em uma instrução preparada é substituído por parâmetros associados. Uma instrução SQL concluída com nenhum espaço reservado é enviada para o banco de dados em execução. <br /><br />PDO:: attr_emulate_prepares pode ser usado para ignorar algumas restrições no SQL Server. Por exemplo, SQL Server não dá suporte a parâmetros nomeados ou posicionais em algumas cláusulas de Transact-SQL. Além disso, o SQL Server tem um limite de 2100 parâmetros de associação.<br /><br />Você pode definir o atributo PDO:: attr_emulate_prepares como true. Por exemplo:<br /><br />`PDO::ATTR_EMULATE_PREPARES => true`<br /><br />Por padrão, esse atributo é definido como false.<br /><br />**Observação:** a segurança das consultas parametrizadas não é aplicada ao usar `PDO::ATTR_EMULATE_PREPARES => true`. Seu aplicativo deve garantir que os dados associados aos parâmetros não contenham código Transact-SQL mal-intencionado.<br /><br />**Limitações:**: porque os parâmetros não são associados usando o recurso de consulta parametrizada do banco de dados, não há suporte para parâmetros de saída e entrada_saída.|  
|PDO::SQLSRV_ATTR_ENCODING|PDO::SQLSRV_ENCODING_UTF8 (padrão)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|Se for True, especifica a execução direta da consulta. False significa uma execução preparada da instrução. Para obter mais informações sobre PDO::SQLSRV_ATTR_DIRECT_QUERY, veja [Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Para obter mais informações, consulte [PDO::setAttribute](../../connect/php/pdo-setattribute.md).|  
  
Quando você usa PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, pode usar PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE. Por exemplo,  
  
```  
array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_DYNAMIC));  
```  
  
A tabela a seguir mostra os valores possíveis para PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE.  
  
|Valor|Descrição|  
|---------|---------------|  
|PDO::SQLSRV_CURSOR_BUFFERED|Cria um cursor estático (em buffer) do lado do cliente. Para obter mais informações sobre os cursores do lado do cliente, veja [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_CURSOR_DYNAMIC|Cria um cursor dinâmico (sem buffer) do lado do servidor que permite acessar linhas em qualquer ordem e que refletirá as alterações no banco de dados.|  
|PDO::SQLSRV_CURSOR_KEYSET_DRIVEN|Cria um cursor de conjunto de chaves do lado do servidor. Um cursor de conjunto de chaves não atualiza a contagem de linhas se uma linha for excluída da tabela (uma linha excluída será retornada sem valores).|  
|PDO::SQLSRV_CURSOR_STATIC|Cria um cursor estático do lado do servidor, que permite acessar linhas em qualquer ordem, mas que não refletirá as alterações no banco de dados.<br /><br />PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL implica em PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_STATIC.|  
  
Você pode fechar um objeto PDOStatement definindo-o como null.  
  
## <a name="example"></a>Exemplo  
Este exemplo mostra como usar o método PDO::prepare com marcadores de parâmetro e um cursor somente de avanço.  
  
```  
<?php  
$database = "Test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$col1 = 'a';  
$col2 = 'b';  
  
$query = "insert into Table1(col1, col2) values(?, ?)";  
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );  
$stmt->execute( array( $col1, $col2 ) );  
print $stmt->rowCount();  
echo "\n";  
  
$query = "insert into Table1(col1, col2) values(:col1, :col2)";  
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );  
$stmt->execute( array( ':col1' => $col1, ':col2' => $col2 ) );  
print $stmt->rowCount();  
  
$stmt = null  
?>  
```  
  
## <a name="example"></a>Exemplo  
Este exemplo mostra como usar o método PDO::prepare com um cursor do lado do cliente. Para obter uma amostra exibindo um cursor do lado do servidor, veja [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "select * from Person.ContactType";  
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));  
$stmt->execute();  
  
echo "\n";  
  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print "$row[Name]\n";  
}  
echo "\n..\n";  
  
$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );  
print "$row[Name]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );  
print "$row[1]\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );  
print "$row[1]..\n";  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );  
print_r($row);  
  
$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );  
print_r($row);  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
