---
title: setAuthenticationScheme (SQLServerDataSource) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
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
ms.assetid: b942f78e-7ce1-44ef-923d-a7c3d7c76b83
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 59560311e9da0bd60a5b2f124deae933672e2d0c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setauthenticationscheme-sqlserverdatasource"></a>setAuthenticationScheme (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica o tipo de segurança integrada que o aplicativo deve usar.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
public void setAuthenticationScheme(String authenticationScheme);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *authenticationScheme*  
  
 Os valores são **"JavaKerberos"** e o padrão **"NativeAuthentication"**. Para obter mais informações, consulte [usando a autenticação integrada Kerberos para se conectar ao SQL Server](../../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

