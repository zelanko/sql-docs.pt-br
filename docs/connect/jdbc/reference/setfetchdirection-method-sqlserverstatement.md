---
title: Método setFetchDirection (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 18176517-2fb3-4266-924d-0f01253083d2
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd846f103df1428b88a540ac20dd071d419d12d3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setfetchdirection-method-sqlserverstatement"></a>Método setFetchDirection (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Fornece [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] uma dica sobre a direção na qual resultado conjunto de linhas devem ser processadas.  
  
> [!NOTE]  
>  Atualmente, o driver JDBC ignora a dica fornecida por este método.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setFetchDirection(int nDir)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *nDir*  
  
 Um **int** que indica a direção, que pode ser um dos seguintes valores de processamento da linha:  
  
 FETCH_FORWARD  
  
 FETCH_REVERSE  
  
 FETCH_UNKNOWN  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setFetchDirection é especificado pelo método setFetchDirection na interface Java.SQL. Statement.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
