---
title: Método updateNull (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateNull (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b22336a1-fe53-4e00-a5ff-ede8d3f2b9f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7de1531b16578cacf70c6493029edcd2d853f7fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67998659"
---
# <a name="updatenull-method-int"></a>Método updateNull (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor nulo, considerando o índice da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateNull(int index)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *index*  
  
 Um **int** que indica o índice de coluna.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateNull é especificado pelo método updateNull na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método &#40;updateNull SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenull-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
