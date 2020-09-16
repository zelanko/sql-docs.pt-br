---
description: Método position (java.lang.String, long)
title: Método position (java.lang.String, long) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6529acba826fb4e76c3c6f6612eacccc63ee7a30
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433038"
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
  
## <a name="return-value"></a>Valor de retorno  
 A posição em que a subcadeia de caracteres aparece ou -1 se ela não estiver presente; a primeira posição é 1.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método position é especificado pelo método position na interface java.sql.Clob.  
  
## <a name="see-also"></a>Consulte Também  
 [Método position &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/position-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
