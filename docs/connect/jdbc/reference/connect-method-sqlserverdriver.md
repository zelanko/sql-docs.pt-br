---
title: Método Connect (SQLServerDriver) | Microsoft Docs
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
- SQLServerDriver.connect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 43813a4c-1cc7-4659-ba27-f1786f1371eb
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee87f7694e3612cd89ca3dfa21a691c2aaecb8e3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connect-method-sqlserverdriver"></a>Método connect (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Faz uma conexão ao banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Connection connect(java.lang.String Url,  
                                   java.util.Properties suppliedProperties)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *URL*  
  
 Um **cadeia de caracteres** valor que contém a URL que é usada para se conectar ao banco de dados.  
  
 *suppliedProperties*  
  
 Um conjunto de pares de valor de cadeia de caracteres usado como argumentos de conexão.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de Conexão.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método de conexão é especificado pelo método na interface Java.SQL. driver conectar.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [Membros de SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [Classe SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
