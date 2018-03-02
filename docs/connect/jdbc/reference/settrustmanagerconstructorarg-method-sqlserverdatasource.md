---
title: "setTrustManagerConstructorArg método (SQLServerDataSource) | Microsoft Docs"
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
- SQLServerDataSource.setTrustManagerConstructorArg
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d121f141ee47d42141b190283762ab636ccdbe24
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2018
---
# <a name="settrustmanagerconstructorarg-method-sqlserverdatasource"></a>setTrustManagerConstructorArg método (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o valor de cadeia de caracteres da propriedade de conexão TrustManagerConstructorArg.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setTrustManagerConstructorArg(java.lang.String trustManagerClass)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *trustManagerClass*  
  
 Um **cadeia de caracteres** que contém o nome de classe totalmente qualificado de um javax.net.ssl.TrustManager personalizado.
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
