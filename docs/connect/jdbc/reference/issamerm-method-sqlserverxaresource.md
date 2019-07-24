---
title: Método isSameRM (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.isSameRM
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa24c46-b7cf-470a-afa1-52301847a448
author: MightyPen
ms.author: genemi
ms.openlocfilehash: acd1beaa07ab9d1867fe99e519d3969f4efec3ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977305"
---
# <a name="issamerm-method-sqlserverxaresource"></a>Método isSameRM (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Determina se a instância do gerenciador de recursos representada pelo objeto de destino é a mesma representada pelo objeto XAResource fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean isSameRM(javax.transaction.xa.XAResource xares)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *xares*  
  
 Um objeto XAResource.  
  
## <a name="return-value"></a>Valor retornado  
 **true** se as instâncias forem as mesmas. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 Esse método commit é especificado pelo método commit na interface javax.transaction.xa.XAResource.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Membros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
