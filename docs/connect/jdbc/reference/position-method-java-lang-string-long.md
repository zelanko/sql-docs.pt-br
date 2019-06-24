---
title: Método (lang, longo) Position | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.position (java.lang.String, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 86fad8ed-375a-42e1-b40e-1fa085957a2c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 40c7dadf83861d889acd7932dbe1dad17fda4b35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802453"
---
# <a name="position-method-javalangstring-long"></a>Método position (java.lang.String, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna a posição de caractere da subcadeia de caracteres especificada no CLOB com base na posição inicial fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public long position(java.lang.String searchstr,  
                     long start)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *searchstr*  
  
 A subcadeia de caracteres pela qual pesquisar.  
  
 *start*  
  
 A posição em que a pesquisa deve ser iniciada; a primeira posição é 1.  
  
## <a name="return-value"></a>Valor retornado  
 A posição em que a subcadeia de caracteres aparece ou -1 se ela não estiver presente; a primeira posição é 1.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método de posição é especificado pelo método posição na interface do CLOB.  
  
## <a name="see-also"></a>Consulte Também  
 [Método Position &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/position-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
