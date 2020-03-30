---
title: Método getTimestamp (int, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTimestamp (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 161c559a-8651-44ba-a914-15eb6a612417
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 50aa202837bee9e091cbb2ad31f56da6ea15eef0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67978876"
---
# <a name="gettimestamp-method-int-javautilcalendar"></a>Método getTimestamp (int, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto java.sql.Timestamp na linguagem de programação Java, considerando o índice do parâmetro, usando um objeto Calendar.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Timestamp getTimestamp(int index,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *index*  
  
 Um **int** que indica o índice do parâmetro.  
  
 *cal*  
  
 Um objeto Calendar.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Timestamp.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getTimestamp é especificado pelo método getTimestamp na interface java.sql.CallableStatement.  
  
 Esse método só retorna valores das colunas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]datetime**e**smalldatetime**do**.  
  
## <a name="see-also"></a>Consulte Também  
 [getTimestamp Method &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
