---
description: Construtor SQLServerException (java.lang.Object, java.lang.String, java.lang.String, int, boolean)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f66bd8759733c2574438ba12ce9f12b00cf88842
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450471"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-int-boolean"></a>Construtor SQLServerException (java.lang.Object, java.lang.String, java.lang.String, int, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa uma nova instância da classe [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) quando são fornecidos um **object**, um objeto **string**, um objeto **string**, um **int** e um **boolean**.

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
  
 O buffer de E/S que gerou a exceção.

 *errText*  
  
 Uma cadeia de caracteres que contém o texto de erro.
  
 *sqlState*  
  
 Um objeto enum que contém o estado do SQL.
 
 *errNum*  
  
 Um int que contém o código de erro da exceção.
 
 *bStack*  
  
 Um booliano que indica se o rastreamento de pilha deve ser gerado.
  
## <a name="see-also"></a>Consulte Também  
 [Construtores SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Membros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Classe SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
