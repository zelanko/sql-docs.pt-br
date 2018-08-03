---
title: Conectando ao SQL Server com o JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 94bcfbe3-f00e-4774-bda8-bb7577518fec
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5dd38c3fa9be49e4781a23f82d8ef0a007e9f43a
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39279217"
---
# <a name="connecting-to-sql-server-with-the-jdbc-driver"></a>Conectando ao SQL Server com o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Uma das coisas mais importantes que você fará com o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] é estabelecer uma conexão com um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Toda a interação com o banco de dados ocorre por meio do objeto [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) e, como o driver JDBC tem uma arquitetura simples, praticamente todo tipo de comportamento interessante envolve o objeto SQLServerConnection.  
  
 Se um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] estiver escutando apenas em uma porta IPv6, defina o conjunto de propriedades do sistema java.net.preferIPv6Addresses para garantir que esse IPv6 seja usado no lugar de IPv4 para a conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
```java
System.setProperty("java.net.preferIPv6Addresses", "true");  
```  
  
 Os tópicos desta seção descrevem como fazer e trabalhar com uma conexão a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Construindo a URL de conexão](../../connect/jdbc/building-the-connection-url.md)|Descreve como formar uma URL de conexão para se conectar ao banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Também descreve a conexão a instâncias nomeadas de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Configurando as propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md)|Descreve as várias propriedades de conexão e como elas podem ser usadas quando você se conecta a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Configurando as propriedades da fonte de dados](../../connect/jdbc/setting-the-data-source-properties.md)|Descreve como usar fontes de dados em uma Plataforma Java, ambiente do Enterprise Edition (Java EE).|  
|[Trabalhando com uma conexão](../../connect/jdbc/working-with-a-connection.md)|Descreve os vários modos nos qual criar uma instância de uma conexão para um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Usando pool de conexões](../../connect/jdbc/using-connection-pooling.md)|Descreve como o driver JDBC oferece suporte ao uso de pool de conexão.|  
|[Usando o espelhamento de banco de dados&#40;JDBC&#41;](../../connect/jdbc/using-database-mirroring-jdbc.md)|Descreve como o driver JDBC oferece suporte ao uso de espelhamento de banco de dados.|  
|[Suporte a JDBC driver para alta disponibilidade e recuperação de desastre](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)|Descreve como desenvolver um aplicativo que se conectará a um grupo de disponibilidade AlwaysOn.|  
|[Usando a autenticação integrada do Kerberos para se conectar ao SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)|Discute uma implementação Java para aplicativos que se conectam a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], usando a autenticação integrada Kerberos.|  
|[Conectando-se a um banco de dados SQL do Azure](../../connect/jdbc/connecting-to-an-azure-sql-database.md)|Discute problemas de conectividade para bancos de dados no SQL Azure.|  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
