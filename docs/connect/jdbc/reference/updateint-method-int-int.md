---
title: Método updateInt (int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateInt (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f4f651b0-a822-4bd4-b391-cc2355154a2a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae2b49f04f36b43d63eeb287e10ac52556f8fe44
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927833"
---
# <a name="updateint-method-int-int"></a>Método updateInt (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor **int**, considerando o índice da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateInt(int index,  
                      int x)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *index*  
  
 Um **int** que indica o índice de coluna.  
  
 *x*  
  
 Um valor **int**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateInt é especificado pelo método updateInt na interface java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateInt &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
