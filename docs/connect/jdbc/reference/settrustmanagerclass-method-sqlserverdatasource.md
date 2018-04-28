---
title: setTrustManagerClass método (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerDataSource.setTrustManagerClass
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b41c26266125a20de78560eda5031227be1001a2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="settrustmanagerclass-method-sqlserverdatasource"></a>setTrustManagerClass método (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o valor de cadeia de caracteres da propriedade de conexão TrustManagerClass.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setTrustManagerClass(java.lang.String trustManagerClass)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *trustManagerClass*  
  
 Um **cadeia de caracteres** que contém o nome de classe totalmente qualificado de um javax.net.ssl.TrustManager personalizado.
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
