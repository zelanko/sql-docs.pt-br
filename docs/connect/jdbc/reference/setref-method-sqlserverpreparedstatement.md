---
title: Método vsetRef (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setRef
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1a09bbf9-6f8f-4a21-85d2-2182111b5ce7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a002ec9f607804854e0bf390c455e6b492432a42
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67973122"
---
# <a name="setref-method-sqlserverpreparedstatement"></a>Método setRef (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto Ref fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setRef(int i,  
                         java.sql.Ref x)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *i*  
  
 Um **int** que indica o número do parâmetro.  
  
 *x*  
  
 Um objeto Ref.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setRef é especificado pelo método setRef na interface java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Classe SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
