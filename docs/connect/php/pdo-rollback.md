---
title: 'PDO:: Rollback | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d918c1e3-1be0-4001-b3b0-000db6d9e8b8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f5f33f7d027a858bdd57aa69c65107ed15856e2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47609236"
---
# <a name="pdorollback"></a>PDO::rollback
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Descarta os comandos de banco de dados emitidos depois de chamar [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) e retorna a conexão para o modo de confirmação automática.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
bool PDO::rollBack ();  
```  
  
## <a name="return-value"></a>Valor retornado  
true se a chamada do método for bem-sucedida; caso contrário, false.  
  
## <a name="remarks"></a>Remarks  
PDO::rollback não é afetado pelo valor de PDO::ATTR_AUTOCOMMIT, nem o afeta.  
  
Consulte [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) para ver um exemplo que usa PDO::rollback.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="see-also"></a>Consulte Também  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
