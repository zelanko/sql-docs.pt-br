---
title: Método prepare (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.prepare
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f800c966-3fae-41b3-963a-464988f80da3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c926cafd2e0bb167d34484e864b7770cf894f3f9
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80914090"
---
# <a name="prepare-method-sqlserverxaresource"></a>Método prepare (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Solicita que o gerenciador de recursos prepare-se para uma confirmação da transação especificada pelo objeto Xid fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int prepare(javax.transaction.xa.Xid xid)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *xid*  
  
 Um objeto Xid.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **int**.  
  
## <a name="exceptions"></a>Exceções  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Comentários  
 Esse método prepare é especificado pelo método prepare na interface javax.transaction.xa.XAResource.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [Membros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Classe SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
