---
title: Construtor SQLServerException (java.lang.Object, java.lang.String, java.lang.String, StreamError, boolean) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 95217b384788ea78bd389948930ba34f580036ec
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80902609"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-streamerror-boolean"></a>Construtor SQLServerException (java.lang.Object, java.lang.String, java.lang.String, StreamError, booliano)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa uma nova instância da classe [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) quando é dado um **object**, um objeto **string**, um objeto **string**, um objeto **StreamError** e um **boolean**.

## <a name="syntax"></a>Sintaxe  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            StreamError streamError,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>parâmetros  
 *obj*  
  
 O buffer de E/S que gerou a exceção.

 *errText*  
  
 Uma cadeia de caracteres que contém o texto de erro.
  
 *sqlState*  
  
 Um objeto enum que contém o estado do SQL.
 
 *streamError*  
  
 Um objeto StreamError que contém detalhes sobre o erro.
 
 *bStack*  
  
 Um booliano que indica se o rastreamento de pilha deve ser gerado.
  
## <a name="see-also"></a>Consulte Também  
 [Construtores SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Membros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Classe SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
