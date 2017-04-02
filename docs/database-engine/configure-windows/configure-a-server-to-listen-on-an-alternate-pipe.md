---
title: "Configurar um servidor para escuta em um pipe alternativo (SQL Server Configuration Manager) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Pipes nomeados [SQL Server], configurando"
  - "escutando [SQL Server], tubos"
  - "tubos [SQL Server], alternar"
  - "pipes alternativos [SQL Server]"
ms.assetid: 914f7491-e2be-4b0d-b3aa-fe5409cdbafa
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Configurar um servidor para escuta em um pipe alternativo (SQL Server Configuration Manager)
  Este tópico descreve como configurar um servidor para escutar em um pipe alternativo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. Por padrão, a instância padrão do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] escuta em um pipe chamado \\\\.\pipe\sql\query. As instâncias nomeadas do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e do [!INCLUDE[ssEW](../../includes/ssew-md.md)] escutam em outros pipes.  
  
 Há três modos de se conectar a um pipe nomeado específico com um aplicativo cliente:  
  
-   Execute o serviço de navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor.  
  
-   Crie um alias no cliente, especificando o pipe nomeado.  
  
-   Programe o cliente para se conectar usando uma cadeia de conexão personalizada.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### Configurar o pipe nomeado usado pelo Mecanismo de Banco de Dados do SQL Server  
  
1.  No SQL Server Configuration Manager, no painel do console, expanda **Configuração de Rede do SQL Server** e clique para expandir **Protocolos para** *\<nome instância>*.  
  
2.  No painel de detalhes, clique com o botão direito do mouse em **Pipes Nomeados** e clique em **Propriedades**.  
  
3.  Na guia **Protocolo** , na caixa **Nome do Pipe** , digite o pipe no qual você deseja que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] escute e clique em **OK**.  
  
4.  No painel de console, clique em **Serviços do SQL Server**.  
  
5.  No painel de detalhes, clique com o botão direito do mouse em **SQL Server (**\<nome instância>**)** e clique em **Reiniciar** para parar e reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está escutando em um pipe alternativo, há três modos de se conectar a um pipe nomeado específico com um aplicativo cliente:  
  
-   Execute o serviço de navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor.  
  
-   Crie um alias no cliente, especificando o pipe nomeado.  
  
-   Programe o cliente para se conectar usando uma cadeia de conexão personalizada.  
  
## Consulte também  
 [Criar ou excluir um alias de servidor para ser usado por um cliente &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/create or delete a server alias for use by a client.md)   
 [Configuração de rede do servidor](../../database-engine/configure-windows/server-network-configuration.md)  
  
  