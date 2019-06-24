---
title: Construtor SQLServerException (java.lang.Object, java.lang.String, java.lang.String, int, boolean) | Microsoft Docs
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
ms.openlocfilehash: 868e14c72fbb7c32d394df2fbbdf5cd3a7c36738
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66766992"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-int-boolean"></a>Construtor SQLServerException (java.lang.Object, java.lang.String, java.lang.String, int, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa uma nova instância dos [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) classe quando é fornecido um **objeto**, um **cadeia de caracteres** objeto, um **cadeia de caracteres** objeto, um **int**e um **booliano**.

## <a name="syntax"></a>Sintaxe  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            int errNum,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>Parâmetros  
 *obj*  
  
 O buffer de e/s que gerou a exceção.

 *errText*  
  
 Uma cadeia de caracteres que contém o texto de erro.
  
 *sqlState*  
  
 Um objeto de enumeração que contém o estado do SQL.
 
 *errNum*  
  
 Um int que contêm o código de erro da exceção.
 
 *bStack*  
  
 Um booliano que indica se o rastreamento de pilha deve ser gerado.
  
## <a name="see-also"></a>Consulte Também  
 [Construtores SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Membros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Classe SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
