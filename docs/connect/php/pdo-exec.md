---
title: PDO::exec | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 359a87c6-c13a-4518-8f23-a922e7f3b171
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e3708ab788738ea523f2f879efbcac5eb584614e
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="pdoexec"></a>PDO::exec
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Prepara e executa uma instrução SQL em uma única chamada de função, retornando o número de linhas afetadas pela instrução.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int PDO::exec ($statement)  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$statement*: uma cadeia de caracteres contendo a instrução SQL a executar.  
  
## <a name="return-value"></a>Valor de retorno  
Um inteiro que informa o número de linhas afetadas.  
  
## <a name="remarks"></a>Remarks  
Se *$statement* contiver várias instruções SQL, a contagem de linhas afetadas será informada somente para a última instrução.  
  
PDO::exec não retorna resultados de uma instrução SELECT.  
  
Os atributos a seguir afetam o comportamento de PDO::exec:  
  
-   PDO::ATTR_DEFAULT_FETCH_MODE  
  
-   PDO::SQLSRV_ATTR_ENCODING  
  
-   PDO::SQLSRV_ATTR_QUERY_TIMEOUT  
  
Para obter mais informações, consulte [PDO::setAttribute](../../connect/php/pdo-setattribute.md). 
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
Este exemplo exclui linhas na tabela 1 com 'xxxyy' na col1. Em seguida, o exemplo informa quantas linhas foram excluídas.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec("use Test");  
   $ret = $c->exec("delete from Table1 where col1 = 'xxxyy'");  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
