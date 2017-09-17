---
title: 'PDO:: Commit | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a0db4a00-9700-4f49-ab16-6522dd1101d3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d6da71238372c91123380d119c87e120b3eee2b8
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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
  
## <a name="remarks"></a>Comentários  
PDO::commit não é afetado pelo valor de PDO::ATTR_AUTOCOMMIT (e não o afeta).  
  
Consulte [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) para obter um exemplo que utilize PDO::commit.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="see-also"></a>Consulte também  
[Classe PDO](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

