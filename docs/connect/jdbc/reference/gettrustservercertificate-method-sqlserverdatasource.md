---
title: "Método getTrustServerCertificate (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: getTrustServerCertificate Method (SQLServerDataSource)
apilocation: getTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: e4f443cc-b5d7-4859-81df-836a8642ed07
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fbc992d3ae27a2c519e653d77ec8acbb160d2fe5
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>Método getTrustServerCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um **booliano** valor que indica se a propriedade trustServerCertificate está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se trustServerCertificate estiver habilitada. Caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 Se a propriedade trustServerCertificate estiver definida como **true**, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] certificado Secure Sockets Layer (SSL) será automaticamente confiável quando a camada de comunicação for criptografada com SSL. Em outras palavras, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] não validará o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] certificado SSL. O valor padrão é **false**.  
  
 Se a propriedade trustServerCertificate estiver definida como **false**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] validará o certificado SSL do servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
