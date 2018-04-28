---
title: Método updateNClob (int, Java.SQL. NCLOB) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6e9bca18-f64e-46a4-8541-2c9c39b393b5
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3897258b1f2d43b98aa38d6428c022a654a08e5a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="updatenclob-method-int-javasqlnclob"></a>Método updateNClob (int, java.sql.NClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um **NClob** valor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateNClob(int columnIndex,  
                        java.sql.NClob nClob)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice da coluna.  
  
 *nClob*  
  
 Um objeto NClob.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateNClob é especificado pelo método updateNClob na interface Java.SQL. resultset.  
  
 Esse método tem suporte somente em **nvarchar (max)**, **ntext**, e **xml** colunas. Seu uso em quaisquer outros tipos de dados fará com que uma exceção seja lançada.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateNClob &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
