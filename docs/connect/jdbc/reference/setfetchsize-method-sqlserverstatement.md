---
title: Método setFetchSize (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 760e555e-9667-4b40-b0ba-778026ff2923
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9fa7be5cc2f0e3f39e3d89881d38fb91a525b545
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922316"
---
# <a name="setfetchsize-method-sqlserverstatement"></a>Método setFetchSize (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Fornece ao [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] uma dica sobre o número de linhas que devem ser buscadas no banco de dados quando mais linhas são necessárias.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *rows*  
  
 Um **int** que indica o número de linhas a serem buscadas.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setFetchSize é especificado pelo método setFetchSize na interface java.sql.Statement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
