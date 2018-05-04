---
title: Interface de ISQLServerCallableStatement | Microsoft Docs
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
ms.assetid: 030a1631-cfcd-41e0-beb5-47f93c01e8e0
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed88b8e077ba68ccd2a7dd5eabdcb93c2f1cc219
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="isqlservercallablestatement-interface"></a>Interface de ISQLServerCallableStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa instruções JDBC que podem ser chamadas. Essa interface foi adicionada ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** CallableStatement, [ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public interface ISQLServerCallableStatement  
```  
  
## <a name="remarks"></a>Remarks  
 Essa interface é implementada por [classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md).  
  
 Essa interface expõe os seguintes [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-métodos específicos:  
  
|Método|Para obter mais informações, consulte|  
|------------|-------------------------------|  
|microsoft.sql.DateTimeOffset getDateTimeOffset(int)|[getDateTimeOffset(int)](../../../connect/jdbc/reference/getdatetimeoffset-method-int.md)|  
|microsoft.sql.DateTimeOffset getDateTimeOffset(String)|[getDateTimeOffset(String)](../../../connect/jdbc/reference/getdatetimeoffset-method-string.md)|  
|void setDateTimeOffset(String, microsoft.sql.DateTimeOffset)|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
