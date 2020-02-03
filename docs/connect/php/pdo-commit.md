---
title: PDO::commit | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a0db4a00-9700-4f49-ab16-6522dd1101d3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41a87a6444ce61af5b2b8a00aa61306dd90d0d8c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67993292"
---
# <a name="pdocommit"></a>PDO::commit
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Envia comandos para o banco de dados que foram emitidos depois de chamar [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) e retorna a conexão para o modo de confirmação automática.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
bool PDO::commit();  
```  
  
## <a name="return-value"></a>Valor retornado  
true se a chamada do método for bem-sucedida; caso contrário, false.  
  
## <a name="remarks"></a>Comentários  
PDO::commit não é afetado pelo valor de PDO::ATTR_AUTOCOMMIT (e não o afeta).  
  
Consulte [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) para obter um exemplo que utilize PDO::commit.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="see-also"></a>Consulte Também  
[PDO Class](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
