---
title: "Método setNull (int, int) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerPreparedStatement.setNull (int, int)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 7e7f08e9-278a-495a-8ce3-ca173d055021
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b0c220199ea686774fa320fda5d0a7af977620e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="setnull-method-int-int"></a>Método setNull (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como um valor nulo, considerando o tipo de parâmetro a ser definido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setNull(int index,  
                          int jdbcType)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *índice*  
  
 Um **int** que indica o número do parâmetro.  
  
 *jdbcType*  
  
 Um código do tipo de JDBC que é definido pelo java.sql.Types.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setNull é especificado pelo método na interface PreparedStatement setNull.  
  
## <a name="see-also"></a>Consulte também  
 [Método setNull &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
