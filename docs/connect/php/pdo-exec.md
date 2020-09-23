---
title: PDO::exec
description: Referência de API para a função PDO::exec no Driver do Microsoft PDO_SQLSRV para PHP para SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 359a87c6-c13a-4518-8f23-a922e7f3b171
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 989d1f6346f26292326c5b49e1675492cd4ee8de
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646156"
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
  
## <a name="remarks"></a>Comentários  
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
  
## <a name="see-also"></a>Consulte Também  
[PDO Class](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
