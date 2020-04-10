---
title: PDO::errorCode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5864b1d8-6814-41cd-a88d-415124484c13
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df9bce6acf829e39e5082d63f6a910731b709ef8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919374"
---
# <a name="pdoerrorcode"></a>PDO::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO::errorCode recupera o SQLSTATE da operação mais recente no identificador do banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
mixed PDO::errorCode();  
```  
  
## <a name="return-value"></a>Valor retornado  
PDO::errorCode retorna um SQLSTATE de cinco caracteres como uma cadeia de caracteres ou NULL se não houve nenhuma operação no identificador do banco de dados.  
  
## <a name="remarks"></a>Comentários  
PDO::errorCode no driver PDO_SQLSRV retorna avisos sobre algumas operações bem-sucedidas. Por exemplo, em uma conexão bem-sucedida, PDO::errorCode retornará "01000", indicando SQL_SUCCESS_WITH_INFO.  
  
PDO::errorCode recupera somente códigos de erro de operações executadas diretamente na conexão de banco de dados. Se você criar uma instância de PDOStatement por meio de PDO::prepare ou PDO::query e for gerado um erro no objeto de instrução, PDO::errorCode não recuperará esse erro. Você deve chamar PDOStatement::errorCode para retornar o código de erro de uma operação executada em um objeto de instrução específico.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
Neste exemplo, o nome da coluna está incorreto, `Cityx` em vez de `City`, causando um erro, que é, então, relatado.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[PDO Class](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
