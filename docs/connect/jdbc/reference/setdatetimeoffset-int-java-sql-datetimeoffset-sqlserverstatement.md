---
title: setDateTimeOffset (int, java.sql.DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e8b6e380-6b53-489b-be73-73fcb5258269
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ecbdb1496ed0128d6f8e1c4ff37f26b7009171ca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810694"
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
  
## <a name="remarks"></a>Remarks  
 O formato de DateTimeOffset é "AAAA-MM-DD HH-MM-SS[.nnnnnnn] [+][-] HH:MM". Use a tabela a seguir para referência.  
  
|Tipo SQL|Insert|  
|--------------|------------|  
|DATETIME|Pode inserir apenas: "AAAA-MM-DD hh:mm:ss[.nnn]"|  
|smalldatetime|Pode inserir apenas: "AAAA-MM-DD hh:mm:ss"|  
|Hora|Pode inserir apenas: "hh:mm:ss[.nnnnnnn]"|  
|data|Pode inserir apenas: "YYYY-MM-DD"|  
|datetime2|Pode inserir apenas: "YYYY-MM-DD hh:mm:ss[.nnnnnnn]"|  
  
## <a name="see-also"></a>Consulte Também  
 [getDateTimeOffset &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
