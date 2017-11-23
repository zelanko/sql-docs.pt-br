---
title: setDateTimeOffset (int, java.sql.DateTimeOffset) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e8b6e380-6b53-489b-be73-73fcb5258269
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 176ae8749128565cca236817eb79bad94d839134
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setdatetimeoffsetint-javasqldatetimeoffset-sqlserverstatement"></a>setDateTimeOffset(int, java.sql.DateTimeOffset) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o valor DateTimeOffset especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setDateTimeOffset(int parameterIndex, DateTimeOffset dateTime)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *parameterIndex*  
  
 Índice da coluna a ser definido.  
  
 *dateTimeOffset*  
  
 Um objeto DateTimeOffset.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O formato de DateTimeOffset é "AAAA-MM-DD HH-MM-SS[.nnnnnnn] [+][-] HH:MM". Use a tabela a seguir para referência.  
  
|Tipo de SQL|Insert (inserir)|  
|--------------|------------|  
|datetime|Pode inserir apenas: "AAAA-MM-DD hh:mm:ss[.nnn]"|  
|smalldatetime|Pode inserir apenas: "AAAA-MM-DD hh:mm:ss"|  
|Hora|Pode inserir apenas: "hh:mm:ss[.nnnnnnn]"|  
|Data|Pode inserir apenas: "YYYY-MM-DD"|  
|datetime2|Pode inserir apenas: "YYYY-MM-DD hh:mm:ss[.nnnnnnn]"|  
  
## <a name="see-also"></a>Consulte também  
 [getDateTimeOffset &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

