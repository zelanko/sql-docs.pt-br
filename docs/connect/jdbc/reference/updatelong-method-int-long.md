---
title: Método updateLong (int, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateLong (int, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6363288-1415-4b25-8bb3-c34d6211c6d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 27e572b5019a8c1a85e3c1bac5a8f4d5e5dd962c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80903207"
---
# <a name="updatelong-method-int-long"></a>Método updateLong (int, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor **long** considerando o índice da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateLong(int index,  
                       long x)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *index*  
  
 Um **int** que indica o índice de coluna.  
  
 *x*  
  
 Um valor **long**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateLong é especificado pelo método updateLong na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateLong &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
