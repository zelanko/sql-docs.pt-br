---
title: "Método getClientInfo () | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b06a5ced-b760-4c78-b17e-854ce95a1a5c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed81345b9cf45678fd4571fca747eebb7fc30f9b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="getclientinfo-method-"></a>Método getClientInfo ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera uma lista que contém o nome e o valor atual de cada propriedade de informações de cliente que tem o suporte do driver JDBC.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.util.Properties getClientInfo()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de propriedades que contém o nome e o valor atual de cada uma das propriedades de informações de cliente com suporte pelo driver.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getClientInfo é especificado pelo método getClientInfo na interface Java.SQL.  
  
 O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] não oferece suporte a nenhuma propriedade de informações do cliente. Como resultado, esse método retorna um objeto vazio de propriedades.  
  
 Da mesma forma, os aplicativos podem usar o [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) método o [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) classe para recuperar uma lista de propriedades de informações de cliente que o driver dá suporte. O [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) método retorna um conjunto de resultados vazio.  
  
## <a name="see-also"></a>Consulte também  
 [Método getClientInfo &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [Membros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
