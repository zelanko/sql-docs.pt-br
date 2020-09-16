---
description: Interface ISQLServerConnection
title: Interface ISQLServerConnection | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 031c01e2-2c65-4fe4-9700-fdbcc7a39f30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1cedc723bcaee3b8ca850d7671ea0c868f9e11fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433508"
---
# <a name="isqlserverconnection-interface"></a>Interface ISQLServerConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa uma conexão JDBC com um banco de dados do [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Essa interface foi adicionada ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** java.sql.Connection  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public interface ISQLServerConnection  
```  
  
## <a name="remarks"></a>Comentários  
 Essa interface é implementada pela [Classe SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
 Essa interface expõe o seguinte campo específico do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]:  
  
|Campo|Para obter mais informações, consulte|  
|-----------|-------------------------------|  
|public final static int TRANSACTION_SNAPSHOT|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|  
|public UUID getClientConnectionId()|[getClientConnectionID()](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
