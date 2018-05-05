---
title: Método getHoldability (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4508d90f-c3c4-4eac-8001-fb0b93b66734
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 422fdd2f8a7a695b8d1ee591bf7dc93c10ca78db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getholdability-method-sqlserverresultset"></a>Método getHoldability (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera a colocação em espera desse [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** valor que contenha um dos seguintes níveis de suspensão:  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getHoldability é especificado pelo método getHoldability na interface Java.SQL. resultset.  
  
 Para definir a suspensão do conjunto de resultados, os aplicativos podem usar o [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) método o [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) classe. Após o [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) método é chamado e o objeto de instrução e seu objeto de conjunto de resultados são criados e a instrução é executada, o aplicativo pode precisar alterar a suspensão novamente.  
  
 Para cursores de servidor, quando conectado ao SQL Server 2005 ou posterior, definir colocação em espera afetará apenas a suspensão dos novos conjuntos de resultados que ainda devem ser criados nessa conexão. Porém, com o SQL Server 2000, a definição da colocação em espera afetará a colocação em espera dos conjuntos de resultados existentes e dos novos conjuntos de resultados que ainda serão criados nessa conexão.  
  
 Quando a colocação em espera é redefinida e o método getHoldability é chamado no objeto do conjunto de resultados previamente criado, o valor retornado por esse método pode ser diferente do valor de colocação em espera retornado pelos métodos a seguir: Statement.getResultSetHoldability , Connection.getHoldability ou DatabaseMetaData.getResultSetHoldability.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
