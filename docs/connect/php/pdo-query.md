---
title: PDO::query | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f6f5e6d4-8ca9-4f06-89ed-de65ad3952a2
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c945bb5ab0a14b1c93b0c7f4fb16a72cd258bb14
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35308265"
---
# <a name="pdoquery"></a>PDO::query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Executa uma consulta SQL e retorna um conjunto de resultados como um objeto PDOStatement.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PDOStatement PDO::query ($statement[, $fetch_style);  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$statement*: a instrução SQL que você quer executar.  
  
*$fetch_style*: instruções adicionais sobre como executar a consulta. Para obter mais detalhes, consulte a seção Comentários. $*fetch_style* em PDO:: Query pode ser substituído por $*fetch_style* em PDO:: Fetch.  
  
## <a name="return-value"></a>Valor retornado  
Se a chamada for bem-sucedida, o PDO::query retornará um objeto PDOStatement. Se a chamada falhar, PDO::query gerará um objeto PDOException ou retornará false, dependendo da configuração de PDO::ATTR_ERRMODE.  
  
## <a name="exceptions"></a>Exceções  
PDOException.  
  
## <a name="remarks"></a>Remarks  
Uma consulta executada com PDO:: Query pode executar uma instrução preparada ou diretamente, dependendo da configuração de PDO:: sqlsrv_attr_direct_query. Para obter mais informações, consulte [Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).  
  
PDO:: sqlsrv_attr_query_timeout também afeta o comportamento de PDO; Para obter mais informações, consulte [PDO:: setAttribute](../../connect/php/pdo-setattribute.md).  
  
Você pode especificar as seguintes opções para $*fetch_style*.  
  
|style|Description|  
|---------|---------------|  
|PDO::FETCH_COLUMN, *num*|Consultas de dados na coluna especificada. A primeira coluna na tabela é a coluna 0.|  
|Fetch_class, '*classname*', matriz ( *arglist* )|Cria uma instância de uma classe e atribui nomes de coluna a propriedades da classe. Se o construtor de classe aceitar um ou mais parâmetros, você poderá passar também uma *arglist*.|  
|Fetch_class, '*classname*'|Atribui nomes de coluna a propriedades de uma classe existente.|  
  
Chame PDOStatement::closeCursor para liberar os recursos de banco de dados associados ao objeto PDOStatement antes de chamar PDO::query novamente.  
  
Você pode fechar um objeto PDOStatement definindo-o como null.  
  
Se nem todos os dados de um conjunto de resultados forem buscados, a próxima chamada a PDO::query não falhará.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
Este exemplo mostra várias consultas.  
  
```  
<?php  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
$conn->setAttribute( PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 1 );  
  
$query = 'select * from Person.ContactType';  
  
// simple query  
$stmt = $conn->query( $query );  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print_r( $row['Name'] ."\n" );  
}  
  
echo "\n........ query for a column ............\n";  
  
// query for one column  
$stmt = $conn->query( $query, PDO::FETCH_COLUMN, 1 );  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query with a new class ............\n";  
$query = 'select * from HumanResources.Department order by GroupName';  
// query with a class  
class cc {  
   function __construct( $arg ) {  
      echo "$arg";  
   }  
  
   function __toString() {  
      return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
   }  
}  
  
$stmt = $conn->query( $query, PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query into an existing class ............\n";  
$c_obj = new cc( '' );  
$stmt = $conn->query( $query, PDO::FETCH_INTO, $c_obj );  
while ( $stmt->fetch() ){  
   echo "$c_obj\n";  
}  
  
$stmt = null;  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
