---
title: PDOStatement::bindColumn | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bbdcea53-d23d-4769-89a0-95c7cf4d5390
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4b159e57f6f2335e894490f7e34d159bd95b2b6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993138"
---
# <a name="pdostatementbindcolumn"></a>PDOStatement::bindColumn
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Associa uma variável a uma coluna em um conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
bool PDOStatement::bindColumn($column, &$param[, $type[, $maxLen[, $driverdata ]]] );  
```  
  
#### <a name="parameters"></a>parâmetros  
$*column*: o número da coluna (misto, índice baseado em 1) ou o nome da coluna no conjunto de resultados.  
  
&$*param*: o nome (misto) da variável PHP à qual a coluna será associada.  
  
$*type*: o tipo de dados opcional do parâmetro, representando por uma constante PDO::PARAM_*.  
  
$*maxLen*: inteiro opcional, não usado pelos Drivers da Microsoft para PHP para SQL Server.  
  
$*driverdata*: um ou mais parâmetros mistos opcionais para o driver. Por exemplo, você poderia especificar PDO::SQLSRV_ENCODING_UTF8 para associar a coluna a uma variável como uma cadeia de caracteres codificada em UTF-8.  
  
## <a name="return-value"></a>Valor retornado  
TRUE se bem-sucedido; caso contrário, FALSE.  
  
## <a name="remarks"></a>Comentários  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
Este exemplo mostra como uma variável pode ser associada a uma coluna em um conjunto de resultados.  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$query = "SELECT Title, FirstName, EmailAddress FROM Person.Contact where LastName = 'Estes'";  
$stmt = $conn->prepare($query);  
$stmt->execute();  
  
$stmt->bindColumn('EmailAddress', $email);  
while ( $row = $stmt->fetch( PDO::FETCH_BOUND ) ){  
   echo "$email\n";  
}  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
