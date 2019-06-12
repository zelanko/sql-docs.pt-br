---
title: Construtor SQLServerException (lang, lang, int, Throwable) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: fbd40c6edb2e4b623f0e2fbf7e00ad91dc683a04
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66766870"
---
# <a name="sqlserverexception-constructor-javalangstring-javalangstring-int-javalangthrowable"></a>Construtor SQLServerException (lang, lang, int, Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa uma nova instância dos [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) classe quando é fornecido um **cadeia de caracteres** objeto, uma **cadeia de caracteres** objeto, um **int**e um **throwable** objeto.

## <a name="syntax"></a>Sintaxe  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState errState,
            int errNum,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>Parâmetros  
 *errText*  
  
 Uma cadeia de caracteres que contém o texto de erro.
  
 *errState*  
  
 Uma cadeia de caracteres que contém o estado do erro.
 
 *errNum*  
  
 Um inteiro que contém o código de erro da exceção.
 
 *causa*  
  
 Um objeto throwable que contém a causa da exceção.
  
## <a name="see-also"></a>Consulte Também  
 [Construtores SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Membros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Classe SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
