---
title: Método setBoolean (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setBoolean
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 63397a19-03a2-44bb-b661-7d62c95b6e4e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9742112df6732618eeef07c477af98ff033368fc
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928807"
---
# <a name="setboolean-method-sqlserverpreparedstatement"></a>Método setBoolean (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o valor **boolean** fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setBoolean(int n,  
                             boolean x)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *n*  
  
 Um **int** que indica o número do parâmetro.  
  
 *x*  
  
 Um valor **booliano**, **true** ou **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setboolean é especificado pelo método setboolean na interface java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
