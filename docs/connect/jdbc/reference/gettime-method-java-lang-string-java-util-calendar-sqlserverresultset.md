---
title: Método getTime (java.lang.String, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.getTime (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 13b51f77-cec9-45fc-862e-3d2bb2d718d7
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9c78428add1b57063f7bd6e55ff1902140316d0
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785228"
---
# <a name="gettime-method-javalangstring-javautilcalendar-sqlserverresultset"></a>Método getTime (java.lang.String, java.util.Calendar) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como um objeto java.sql.Time na linguagem de programação Java usando o objeto Calendar fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Time getTime(java.lang.String colName,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *colName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
 *CAL*  
  
 Um objeto de calendário.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto de tempo.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getTime é especificado pelo método getTime na interface do resultset.  
  
 Esse método retorna uma parte de hora válida de um tipo de dados datetime ou smalldatetime do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], com a parte de data definida como a data de linha de base do Java de 1970/01/01 no fuso horário do Calendário fornecido.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getTime &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
