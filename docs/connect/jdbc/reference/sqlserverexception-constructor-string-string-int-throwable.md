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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c8c90b5fcf9fd58bf4c6468603a91242fa1f935c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80902552"
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
  
#### <a name="parameters"></a>parâmetros  
 *errText*  
  
 Uma cadeia de caracteres que contém o texto de erro.
  
 *errState*  
  
 Uma cadeia de caracteres que contém o estado do erro.
 
 *errNum*  
  
 Um int que contém o código de erro da exceção.
 
 *causa*  
  
 Um objeto throwable que contém a causa da exceção.
  
## <a name="see-also"></a>Consulte Também  
 [Construtores SQLServerException](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [Membros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Classe SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
