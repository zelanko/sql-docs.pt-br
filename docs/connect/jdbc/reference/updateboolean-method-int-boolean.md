---
title: Método updateBoolean (int, boolean) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBoolean (int, boolean)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7937f4bb-8537-4012-af81-837f9ac123a2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88dc682abfff75f5668888d2d4598e0619ed033e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924714"
---
# <a name="updateboolean-method-int-boolean"></a>Método updateBoolean (int, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor **boolean**, considerando o índice da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateBoolean(int index,  
                          boolean x)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *index*  
  
 Um **int** que indica o índice de coluna.  
  
 *x*  
  
 Um valor **booliano**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateBoolean é especificado pelo método updateBoolean na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateBoolean &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateboolean-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
