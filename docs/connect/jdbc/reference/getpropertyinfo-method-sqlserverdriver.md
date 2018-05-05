---
title: Método getPropertyInfo (SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDriver.getPropertyInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b5eaad8a-31ef-44ac-af11-d5caa13ac3e2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2b08a3ffe01bda19b25e2164078d89f3e68a741
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getpropertyinfo-method-sqlserverdriver"></a>Método getPropertyInfo (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Usado para descobrir as propriedades necessárias para conectar a um banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.DriverPropertyInfo[] getPropertyInfo(java.lang.String Url,  
                                                     java.util.Properties Info)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *URL*  
  
 Um **cadeia de caracteres** valor que contém a URL que é usada para se conectar ao banco de dados.  
  
 *informações de*  
  
 Uma lista de pares de valor de propriedade; nulo no primeiro uso.  
  
## <a name="return-value"></a>Valor de retorno  
 Uma matriz de objetos DriverPropertyInfo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getPropertyInfo é especificado pelo método getPropertyInfo na interface Java.SQL. driver.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [Membros de SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [Classe SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
