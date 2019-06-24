---
title: Interface ISQLServerStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7f83b514-6e76-4f37-baf3-a10db2010e7c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7a49ef95ac7e6ee122252577ccff9ec535c912fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796419"
---
# <a name="isqlserverstatement-interface"></a>Interface ISQLServerStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa a implementação básica da funcionalidade de instrução JDBC. Essa interface foi adicionada ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** java.sql.Statement  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public interface ISQLServerStatement  
```  
  
## <a name="remarks"></a>Remarks  
 Essa interface é implementada pelo [classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
 Essa interface expõe os seguintes métodos específicos do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]:  
  
|Método|Para obter mais informações, consulte|  
|------------|-------------------------------|  
|public String getResponseBuffering|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|  
|public void setResponseBuffering|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
