---
title: Método setNull (int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setNull (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7e7f08e9-278a-495a-8ce3-ca173d055021
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f250113f83ea51c2705d81780c2207f63149a292
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920460"
---
# <a name="setnull-method-int-int"></a>Método setNull (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como um valor nulo, considerando o tipo de parâmetro a ser definido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setNull(int index,  
                          int jdbcType)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *index*  
  
 Um **int** que indica o número do parâmetro.  
  
 *jdbcType*  
  
 Um código do tipo de JDBC que é definido pelo java.sql.Types.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setNull é especificado pelo método setNull na interface java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setNull &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
