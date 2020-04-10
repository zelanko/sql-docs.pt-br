---
title: Método updateShort (int, short) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateShort (int, short)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 155b9189-cb97-4264-b42c-bbda1c7d624f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94c51ee818a7e598e774aed9c37f08f028ccd027
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919672"
---
# <a name="updateshort-method-int-short"></a>Método updateShort (int, short)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor **short**, considerando o índice da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateShort(int index,  
                        short x)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *index*  
  
 Um **int** que indica o índice de coluna.  
  
 *x*  
  
 Um valor **short**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateShort é especificado pelo método updateShort na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateShort &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
