---
title: Construtor SQLServerException (java.lang.String, java.lang.String, int, java.lang.Throwable) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18827d05bc5567b4566eaa006d88c249874132cf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971079"
---
# <a name="sqlserverexception-constructor-javalangstring-javalangstring-int-javalangthrowable"></a>Construtor SQLServerException (java.lang.String, java.lang.String, int, java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa uma nova instância da classe [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) quando é dado um objeto **String** , um objeto **String** , um **int**e um objeto **Throwable** .

## <a name="syntax"></a>Sintaxe  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState errState,
            int errNum,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>Parâmetros  
 *errText*  
  
 Uma cadeia de caracteres que contém o texto do erro.
  
 *errState*  
  
 Uma cadeia de caracteres que contém o estado do erro.
 
 *errNum*  
  
 Um int que contém o código de erro para a exceção.
 
 *causa*  
  
 Um objeto rethrowável que contém a causa da exceção.
  
## <a name="see-also"></a>Consulte Também  
 [Construtores SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Membros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Classe SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
