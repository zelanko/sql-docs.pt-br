---
title: PDO::commit | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a0db4a00-9700-4f49-ab16-6522dd1101d3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cf60044e9a1d448df64b41f95bce1ae3cdd3b0c7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="pdocommit"></a>PDO::commit
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Envia comandos para o banco de dados que foram emitidos depois de chamar [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) e retorna a conexão para o modo de confirmação automática.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
bool PDO::commit();  
```  
  
## <a name="return-value"></a>Valor de retorno  
true se a chamada do método for bem-sucedida; caso contrário, false.  
  
## <a name="remarks"></a>Remarks  
PDO::commit não é afetado pelo valor de PDO::ATTR_AUTOCOMMIT (e não o afeta).  
  
Consulte [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) para obter um exemplo que utilize PDO::commit.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="see-also"></a>Consulte também  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
