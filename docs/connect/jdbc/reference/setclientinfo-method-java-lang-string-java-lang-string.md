---
title: "Método (Java, Java) setClientInfo | Microsoft Docs"
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
ms.assetid: 8d050831-8305-48a8-bd22-207932111040
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e136cd3eb2330bfd82c531acaa37838ed30e7713
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="setclientinfo-method-javalangstring-javalangstring"></a>Método setClientInfo (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o valor da propriedade de informações de cliente especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setClientInfo (java.lang.String name,  
                           java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *name*  
  
 Uma cadeia de caracteres que contém o nome da propriedade de informações do cliente para definir.  
  
 *value*  
  
 Uma cadeia de caracteres que contém o valor para definir a propriedade de informações do cliente.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setClientInfo é especificado pelo método setClientInfo na interface Java.SQL.  
  
 O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] não oferece suporte a nenhuma propriedade de informações do cliente. No JDBC Driver 2.0, esse método gera um aviso para uma propriedade. Os aplicativos devem usar [getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md) método o [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) classe para recuperar um aviso.  
  
## <a name="see-also"></a>Consulte também  
 [Método setClientInfo &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
