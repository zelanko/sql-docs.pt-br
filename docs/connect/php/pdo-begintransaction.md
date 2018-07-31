---
title: 'PDO:: BeginTransaction | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4d5db438-9df7-4d22-9907-3ddc63bd2220
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48b5d1343a941904280c33f5a983be944c751f2f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38020884"
---
# <a name="pdobegintransaction"></a>PDO::beginTransaction
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Desativa o modo de confirmação automática e inicia uma transação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
bool PDO::beginTransaction();  
```  
  
## <a name="return-value"></a>Valor retornado  
true se a chamada do método for bem-sucedida; caso contrário, false.  
  
## <a name="remarks"></a>Remarks  
A transação começava com PDO::beginTransaction terminará quando [PDO::commit](../../connect/php/pdo-commit.md) ou [PDO::rollback](../../connect/php/pdo-rollback.md) era chamado.  
  
PDO::beginTransaction não é afetado pelo valor de PDO::ATTR_AUTOCOMMIT (e não o afeta).  
  
Você não tem permissão para chamar PDO::beginTransaction antes de o PDO::beginTransaction anterior ser finalizado com PDO::rollback ou PDO::commit.  
  
A conexão retornará para o modo de confirmação automática se esse método falhar.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir usa um banco de dados chamado Test e uma tabela chamada Table1. Ele inicia uma transação e, em seguida, emite comandos para adicionar duas linhas e depois excluir uma linha. Os comandos são enviados para o banco de dados e a transação é finalizada explicitamente com `PDO::commit`.  
  
```  
<?php  
   $conn = new PDO( "sqlsrv:server=(local); Database = Test", "", "");  
   $conn->beginTransaction();  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'b') ");  
   $ret = $conn->exec("insert into Table1(col1, col2) values('a', 'c') ");  
   $ret = $conn->exec("delete from Table1 where col1 = 'a' and col2 = 'b'");  
   $conn->commit();  
   // $conn->rollback();  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
