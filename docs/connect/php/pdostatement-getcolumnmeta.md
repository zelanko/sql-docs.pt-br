---
title: 'Pdostatement:: Getcolumnmeta | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c92a21cc-8e53-43d0-a4bf-542c77c100c9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 98925f324725be6c061c0baed6a3df320d1b39e2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="pdostatementgetcolumnmeta"></a>PDOStatement::getColumnMeta
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera metadados para uma coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
array PDOStatement::getColumnMeta ( $column );  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$conn*: (inteiro) o número com base em zero da coluna cujos metadados você deseja recuperar.  
  
## <a name="return-value"></a>Valor de retorno  
Uma matriz associativa (chave e valor) que contém os metadados da coluna. Consulte a seção de comentários para obter uma descrição dos campos na matriz.  
  
## <a name="remarks"></a>Comentários  
A tabela a seguir descreve os campos na matriz retornada por getColumnMeta.  
  
|NAME|VALUES|  
|--------|----------|  
|native_type|Especifica o tipo do PHP para a coluna. Sempre cadeia de caracteres.|  
|driver:decl_type|Especifica o tipo do SQL usado para representar o valor da coluna no banco de dados. Se a coluna no conjunto de resultados é o resultado de uma função, esse valor não é retornado por PDOStatement::getColumnMeta.|  
|sinalizadores|Especifica os sinalizadores definidos para essa coluna. Sempre 0.|  
|NAME|Especifica o nome da coluna no banco de dados.|  
|table|Especifica o nome da tabela que contém a coluna no banco de dados. Sempre em branco.|  
|len|Especifica o comprimento da coluna.|  
|precisão|Especifica a precisão numérica dessa coluna.|  
|pdo_type|Especifica o tipo desta coluna, conforme representado pelas constantes PDO::PARAM_ *. Sempre PDO::PARAM_STR (2).|  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$stmt = $conn->query("select * from Person.ContactType");  
$metadata = $stmt->getColumnMeta(2);  
var_dump($metadata);  
  
print $metadata['sqlsrv:decl_type'] . "\n";  
print $metadata['native_type'] . "\n";  
print $metadata['name'];  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Classe PDOStatement](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

