---
title: Método getTypeMap (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getTypeMap
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c81bcf9a-2e24-4dfc-8c04-d612e9b7baca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d42a24db0e1e0aad38adbdf1b2ca0ca686a76de
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80911032"
---
# <a name="gettypemap-method-sqlserverconnection"></a>Método getTypeMap (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o objeto Map associado ao objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
> [!NOTE]  
>  No momento, este método não é compatível com [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.util.Map getTypeMap()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Map.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getTypeMap é especificado pelo método getTypeMap na interface javax.sql.Connection.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
