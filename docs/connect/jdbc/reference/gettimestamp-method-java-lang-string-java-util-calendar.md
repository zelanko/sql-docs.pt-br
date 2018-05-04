---
title: Método getTimestamp (Java, java.util.Calendar) | Microsoft Docs
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
- SQLServerCallableStatement.getTimestamp (java.lang.String,java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 770668d9-2e52-4ff0-be2f-ebf78fd41644
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 310374294313d7eca6ea3aa8e821254e07b67d27
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="gettimestamp-method-javalangstring-javautilcalendar"></a>Método getTimestamp (java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto Java.SQL. timestamp na linguagem de programação Java, considerando o nome do parâmetro, usando um objeto de calendário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Timestamp getTimestamp(java.lang.String name,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *name*  
  
 Um **cadeia de caracteres** que contém o nome do parâmetro.  
  
 *CAL*  
  
 Um objeto de calendário.  
  
## <a name="return-value"></a>Valor de retorno  
 Um objeto de carimbo de hora.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getTimestamp é especificado pelo método getTimestamp na interface do CallableStatement.  
  
 Este método retorna valores apenas das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime** e **smalldatetime** colunas.  
  
## <a name="see-also"></a>Consulte também  
 [Método getTimestamp &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
