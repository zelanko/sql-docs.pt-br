---
title: Construtor SQLServerException (java.lang.Object, Java, Java, StreamError, boolean) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2018
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
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5cbee14fda8cca8f38806cc0540d51f0e38dd161
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/02/2018
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-streamerror-boolean"></a>Construtor SQLServerException (java.lang.Object, Java, Java, StreamError, booleano)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa uma nova instância do [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) classe quando é fornecido um **objeto**, um **cadeia de caracteres** objeto, um **cadeia de caracteres** objeto, um  **StreamError** objeto e um **booliano**.

## <a name="syntax"></a>Sintaxe  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            StreamError streamError,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>Parâmetros  
 *obj*  
  
 O buffer de e/s que gerou a exceção.

 *errText*  
  
 Uma cadeia de caracteres que contém o texto de erro.
  
 *sqlState*  
  
 Um objeto de enumeração que contém o estado SQL.
 
 *streamError*  
  
 Um objeto StreamError que contém detalhes sobre o erro.
 
 *bStack*  
  
 Um booliano que indica se o rastreamento de pilha deve ser gerado.
  
## <a name="see-also"></a>Consulte também  
 [Construtores de SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Membros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Classe SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
