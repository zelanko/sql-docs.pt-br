---
title: Método setDate ao valor de data - int | Microsoft Docs
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
- SQLServerPreparedStatement.setDate (int, java.sql.Date)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 12e5a4cc-45a2-4779-bbfc-e4da66829588
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f591bac9fffd73b0de80126c6d3c4f0f01c0a174
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setdate-method-int-javasqldate"></a>Método setDate (int, java.sql.Date)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o valor de data fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setDate(int n,  
                          java.sql.Date x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *n*  
  
 Um **int** que indica o número do parâmetro.  
  
 *x*  
  
 Um objeto de data.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setDate é especificado pelo método setDate na interface PreparedStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Método setDate &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setdate-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
