---
title: Classe SQLServerConnectionPoolDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b00e5a90-2af7-4d04-8ef8-256183777dcf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f80991eaf3449412db672dfcb73f71c596d1bb29
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800623"
---
# <a name="sqlserverconnectionpooldatasource-class"></a>SQLServerConnectionPoolDataSource Class
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa conexões de banco de dados físicas para gerentes de pool de conexões.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
 **Implementa:** javax.sql.ConnectionPoolDataSource  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerConnectionPoolDataSource  
```  
  
## <a name="remarks"></a>Remarks  
 O SQLServerConnectionPoolDataSource é usado normalmente em ambientes de Java Application Server que suportam pool de conexão interna e exigem um ConnectionPoolDataSource para fornecer conexões físicas, como servidores de aplicativos de Plataforma Java, Enterprise Edition (Java EE) que fornecem pool de conexão da especificação da API do JDBC 3.0.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
