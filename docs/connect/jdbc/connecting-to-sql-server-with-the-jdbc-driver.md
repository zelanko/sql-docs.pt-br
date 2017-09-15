---
title: Conectando ao SQL Server com o Driver JDBC | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 94bcfbe3-f00e-4774-bda8-bb7577518fec
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1ebc9542e5683eb58c198745892916893f284822
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-to-sql-server-with-the-jdbc-driver"></a>Conectando ao SQL Server com o JDBC Driver
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Uma das coisas mais importantes que você vai fazer com o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] é fazer uma conexão para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados. Toda a interação com o banco de dados ocorre por meio de [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) objeto, e como o driver JDBC tem uma arquitetura simples, quase todo tipo de comportamento interessante envolve o objeto SQLServerConnection.  
  
 Se um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está escutando apenas em uma porta IPv6, definir o sistema Java.NET preferipv6addresses para certificar-se de que o IPv6 é usado em vez de IPv4 para conectar-se para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
```  
System.setProperty("java.net.preferIPv6Addresses", "true");  
```  
  
 Os tópicos nesta seção descrevem como criar e trabalhar com uma conexão para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Construindo a URL de conexão](../../connect/jdbc/building-the-connection-url.md)|Descreve como formar uma URL de conexão para se conectar a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados. Também descreve como conectar a instâncias nomeadas de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados.|  
|[Configurando as propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md)|Descreve as várias propriedades de conexão e como eles podem ser usados quando você se conectar a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados.|  
|[Configurando as propriedades da fonte de dados](../../connect/jdbc/setting-the-data-source-properties.md)|Descreve como usar fontes de dados em uma Plataforma Java, ambiente do Enterprise Edition (Java EE).|  
|[Trabalhando com uma conexão](../../connect/jdbc/working-with-a-connection.md)|Descreve os vários modos nos qual criar uma instância de uma conexão para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados.|  
|[Usando pool de conexões](../../connect/jdbc/using-connection-pooling.md)|Descreve como o driver JDBC oferece suporte ao uso de pool de conexão.|  
|[Usando o espelhamento de banco de dados &#40; JDBC &#41;](../../connect/jdbc/using-database-mirroring-jdbc.md)|Descreve como o driver JDBC oferece suporte ao uso de espelhamento de banco de dados.|  
|[Suporte a JDBC driver para alta disponibilidade e recuperação de desastre](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)|Descreve como desenvolver um aplicativo que se conectará a um grupo de disponibilidade AlwaysOn.|  
|[Usando a autenticação integrada do Kerberos para se conectar ao SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)|Discute uma implementação Java para aplicativos que se conectam a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados usando a autenticação integrada Kerberos.|  
|[Conectando-se a um banco de dados SQL do Azure](../../connect/jdbc/connecting-to-an-azure-sql-database.md)|Discute problemas de conectividade para bancos de dados no SQL Azure.|  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
