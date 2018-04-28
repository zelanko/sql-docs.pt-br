---
title: getDateTimeOffset(int) (SQLServerResultSet) | Microsoft Docs
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
ms.assetid: 60abf83d-6f97-4e47-b9d3-5072bd09d869
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f12882a31f0c555edca070eca9c814edaa3ac7aa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="getdatetimeoffsetint-sqlserverresultset"></a>getDateTimeOffset(int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esse método foi adicionado no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0.  
  
 Recupera o valor da coluna designada como um [DateTimeOffset classe](../../../connect/jdbc/reference/datetimeoffset-class.md) objeto considerando o índice do parâmetro de linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 O ordinal da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 Um [DateTimeOffset classe](../../../connect/jdbc/reference/datetimeoffset-class.md) objeto.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Você pode atualizar um [DateTimeOffset classe](../../../connect/jdbc/reference/datetimeoffset-class.md) valor com [Updatedatetimeoffset](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
