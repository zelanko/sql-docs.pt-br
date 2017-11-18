---
title: 'PDO:: ErrorCode | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5864b1d8-6814-41cd-a88d-415124484c13
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a0104db7e46a377fa78b7f323de6ad237431a032
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="pdoerrorcode"></a>PDO::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO::errorCode recupera o SQLSTATE da operação mais recente no identificador do banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
mixed PDO::errorCode();  
```  
  
## <a name="return-value"></a>Valor de retorno  
PDO::errorCode retorna um SQLSTATE de cinco caracteres como uma cadeia de caracteres ou NULL se não houve nenhuma operação no identificador do banco de dados.  
  
## <a name="remarks"></a>Comentários  
PDO::errorCode no driver PDO_SQLSRV retornará avisos sobre algumas operações bem-sucedidas. Por exemplo, em uma conexão bem-sucedida, PDO::errorCode retornará "01000", indicando SQL_SUCCESS_WITH_INFO.  
  
PDO::errorCode recupera somente códigos de erro de operações executadas diretamente na conexão de banco de dados. Se você criar uma instância de PDOStatement por meio de PDO::prepare ou PDO::query e gerar um erro no objeto de instrução, PDO::errorCode não recuperará esse erro. Você deve chamar PDOStatement::errorCode para retornar o código de erro de uma operação executada em um objeto de instrução específico.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
Neste exemplo, o nome da coluna está incorreto (`Cityx` em vez de `City`), causando um erro, que é relatado em seguida.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Classe PDO](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

