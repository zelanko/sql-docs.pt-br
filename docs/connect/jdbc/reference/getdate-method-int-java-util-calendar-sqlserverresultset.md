---
title: Método getDate (int, java.util.Calendar) (SQLServerResultSet) | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLServerResultSet.getDate (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 150411f7-2a73-4380-b921-9698acd5d1f9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3703a3ef5947ba92ec6fc4b24415ce2e914e665
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getdate-method-int-javautilcalendar-sqlserverresultset"></a>Método getDate (int, java.util.Calendar) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do índice de coluna designada na linha atual deste [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como um objeto Java.SQL em Java linguagem de programação, usando o objeto de calendário fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Date getDate(int columnIndex,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice da coluna.  
  
 *CAL*  
  
 Um objeto de calendário.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de data.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getDate é especificado pelo método na interface Java.SQL. ResultSet getDate.  
  
 Esse método retorna uma parte de data válida de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de dados datetime ou smalldatetime, com a parte de hora definida como a linha de base de tempo de Java de 00:00 (meia-noite) no fuso horário do calendário fornecido.  
  
## <a name="see-also"></a>Consulte também  
 [Método getDate &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
