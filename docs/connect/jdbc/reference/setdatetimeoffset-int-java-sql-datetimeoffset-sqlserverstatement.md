---
title: setDateTimeOffset (int, java.sql.DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e8b6e380-6b53-489b-be73-73fcb5258269
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 722250967bca8484f359d1e33a7541d34eb3ac79
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
 *DateTimeOffset*  
  
 Um objeto DateTimeOffset.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 O formato de DateTimeOffset é "AAAA-MM-DD HH-MM-SS[.nnnnnnn] [+][-] HH:MM". Use a tabela a seguir para referência.  
  
|Tipo de SQL|Insert (inserir)|  
|--------------|------------|  
|datetime|Pode inserir apenas: "AAAA-MM-DD hh:mm:ss[.nnn]"|  
|smalldatetime|Pode inserir apenas: "AAAA-MM-DD hh:mm:ss"|  
|Hora|Pode inserir apenas: "hh:mm:ss[.nnnnnnn]"|  
|Data|Pode inserir apenas: "YYYY-MM-DD"|  
|datetime2|Pode inserir apenas: "YYYY-MM-DD hh:mm:ss[.nnnnnnn]"|  
  
## <a name="see-also"></a>Consulte também  
 [getDateTimeOffset &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
