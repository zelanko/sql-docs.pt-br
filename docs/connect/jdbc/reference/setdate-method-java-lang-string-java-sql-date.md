---
title: cadeia de caracteres de método com valor de data - setDate método setDate | Microsoft Docs
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
- SQLServerCallableStatement.setDate (java.lang.String, java.sql.Date)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4762e2bd-5e94-4562-97d5-f023ecffc08c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e84290b6cfb3462e94e6a47b29e032e5cbf992aa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setdate-method-javalangstring-javasqldate"></a>Método setDate (java.lang.String, java.sql.Date)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o valor de data fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setDate(java.lang.String sCol,  
                    java.sql.Date d)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *sCol*  
  
 Um **cadeia de caracteres** que contém o nome do parâmetro.  
  
 *D*  
  
 Um objeto de data.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setDate é especificado pelo método setDate na interface do CallableStatement.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
