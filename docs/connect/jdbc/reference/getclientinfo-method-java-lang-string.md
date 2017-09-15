---
title: "Método (Java) getClientInfo | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e8e632c4-d6cc-4c5e-b6ad-873579343b19
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e0f92e5db61ef0b778e293ea61b25ad61956986a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getclientinfo-method-javalangstring"></a>Método getClientInfo (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor de uma propriedade de informações de cliente especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getClientInfo (java.lang.String name)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *name*  
  
 Uma cadeia de caracteres que contém o nome da propriedade de informações do cliente para recuperar.  
  
## <a name="return-value"></a>Valor de retorno  
 Uma cadeia de caracteres que contém o valor da propriedade de informações do cliente.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getClientInfo é especificado pelo método getClientInfo na interface Java.SQL.  
  
 O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] não oferece suporte a qualquer propriedade de informações do cliente. Como resultado, este método retorna **nulo**.  
  
 Da mesma forma, os aplicativos podem usar o [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) método o [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) classe para recuperar uma lista de propriedades de informações de cliente que o driver dá suporte. O [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) método retorna um conjunto de resultados vazio.  
  
## <a name="see-also"></a>Consulte também  
 [Método getClientInfo &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
