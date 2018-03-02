---
title: "getTrustManagerClass método (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getTrustManagerClass
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: baaf12b14655d4e3f3b05b12b85200b46956e6a9
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2018
---
# <a name="gettrustmanagerclass-method-sqlserverdatasource"></a>getTrustManagerClass método (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o valor de cadeia de caracteres da propriedade de conexão TrustManagerClass.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getTrustManagerClass()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** que contém o valor da propriedade de conexão TrustManagerClass, ou nulo se nenhum valor for definido.  
  
## <a name="remarks"></a>Remarks  
 Se a propriedade TrustManagerClass não está definida, o [getTrustManagerClass](../../../connect/jdbc/reference/gettrustmanagerclass-method-sqlserverdatasource.md) método retornará nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
