---
title: "Conectar-se ao SQL Server com um servidor proxy (SQL Server Configuration Manager) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WinSock remoto"
  - "RWS"
  - "LATs"
  - "servidores proxy [SQL Server]"
  - "conexões [SQL Server], servidor proxy"
  - "Microsoft Proxy Server [SQL Server]"
  - "tabelas de endereço locais [SQL Server]"
ms.assetid: 39714de0-2a1f-4179-9091-5c3fa4612545
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Conectar-se ao SQL Server com um servidor proxy (SQL Server Configuration Manager)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como conectar-se ao SQL Server por meio de um servidor proxy no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. Para escutar Remote WinSock (RWS) remotamente, defina a tabela de endereço local (LAT) para o servidor proxy, para que o endereço do nó de escuta fique fora do intervalo de entradas de LAT.  
  
##  <a name="a-namessmsprocedurea-using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-enable-connections-to-sql-server-through-microsoft-proxy-server"></a>Habilitar conexões com o SQL Server usando o Microsoft Proxy Server  
  
1.  Siga as etapas em [Configurar um servidor para escutar em uma porta TCP específica &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/configure a server to listen on a specific tcp port.md) para determinar quais portas TCP/IP são usadas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou para configurar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usar uma porta desejada.  
  
2.  No servidor proxy, defina a tabela de endereço local (LAT) para o servidor proxy, para que o endereço do nó de escuta fique fora do intervalo de entradas de LAT. Para obter mais informações, consulte a documentação do servidor proxy.  
  
>  [!NOTE]
>  Este tópico se aplica ao [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] local. Para problemas de conexão relacionados ao [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], consulte [Solucionar problemas de conexão no Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-common-connection-issues).  

