---
title: Interface de ISQLServerResultSet | Microsoft Docs
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
ms.assetid: 002496f7-8ec0-4267-b4e6-ba095e2ef306
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a097625364eab954500f2c635fc27212c5c1380
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="isqlserverresultset-interface"></a>Interface ISQLServerResultSet
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa um conjunto de resultados JDBC. Essa interface foi adicionada ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** ResultSet  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public interface ISQLServerResultSet  
```  
  
## <a name="remarks"></a>Remarks  
 Essa interface é implementada por [classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
 Essa interface expõe o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-métodos específicos:  
  
|Método|Para obter mais informações, consulte|  
|------------|-------------------------------|  
|public microsoft.sql.DateTimeOffset getDateTimeOffset(int)|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-int-sqlserverresultset.md)|  
|public microsoft.sql.DateTimeOffset getDateTimeOffset(String)|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-java-lang-string-sqlserverresultset.md)|  
|public void updateDateTimeOffset(int, microsoft.sql.DateTimeOffset)|[updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-int-microsoft-sql-datetimeoffset-sqlserverresultset.md)|  
|public void updateDateTimeOffset(String, microsoft.sql.DateTimeOffset)|[updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-string-microsoft-sql-datetimeoffset-sqlserverresultset.md)|  
  
 Essa interface expõe os seguintes [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-campos específicos:  
  
|Campo|Para obter mais informações, consulte|  
|-----------|-------------------------------|  
|public static final int CONCUR_SS_OPTIMISTIC_CC|[CONCUR_SS_OPTIMISTIC_CC](../../../connect/jdbc/reference/concur-ss-optimistic-cc-field-sqlserverresultset.md)|  
|public static final int CONCUR_SS_OPTIMISTIC_CCVAL|[CONCUR_SS_OPTIMISTIC_CCVAL](../../../connect/jdbc/reference/concur-ss-optimistic-ccval-field-sqlserverresultset.md)|  
|public static final int CONCUR_SS_SCROLL_LOCKS|[CONCUR_SS_SCROLL_LOCKS](../../../connect/jdbc/reference/concur-ss-scroll-locks-field-sqlserverresultset.md)|  
|public static final int TYPE_SS_DIRECT_FORWARD_ONLY|[TYPE_SS_DIRECT_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-direct-forward-only-field-sqlserverresultset.md)|  
|public static final int TYPE_SS_SCROLL_DYNAMIC|[TYPE_SS_SCROLL_DYNAMIC](../../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md)|  
|public static final int TYPE_SS_SCROLL_KEYSET|[TYPE_SS_SCROLL_KEYSET](../../../connect/jdbc/reference/type-ss-scroll-keyset-field-sqlserverresultset.md)|  
|public static final int TYPE_SS_SCROLL_STATIC|[TYPE_SS_SCROLL_STATIC](../../../connect/jdbc/reference/type-ss-scroll-static-field-sqlserverresultset.md)|  
|public static final int TYPE_SS_SERVER_CURSOR_FORWARD_ONLY|[TYPE_SS_SERVER_CURSOR_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-server-cursor-forward-only-field-sqlserverresultset.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
