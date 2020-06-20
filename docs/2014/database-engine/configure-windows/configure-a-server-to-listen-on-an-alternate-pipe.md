---
title: Configurar um servidor para escutar em um pipe alternativo (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- listening [SQL Server], pipes
- pipes [SQL Server], alternate
- alternate pipes [SQL Server]
ms.assetid: 914f7491-e2be-4b0d-b3aa-fe5409cdbafa
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2d610ec814097be44e189a663db5afaa1345d29c
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935787"
---
# <a name="configure-a-server-to-listen-on-an-alternate-pipe-sql-server-configuration-manager"></a>Configurar um servidor para escuta em um pipe alternativo (SQL Server Configuration Manager)
  Este tópico descreve como configurar um servidor para escutar em um pipe alternativo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. Por padrão, a instância padrão do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] escuta em um pipe chamado \\\\.\pipe\sql\query. As instâncias nomeadas do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e do [!INCLUDE[ssEW](../../includes/ssew-md.md)] escutam em outros pipes.  
  
 Há três modos de se conectar a um pipe nomeado específico com um aplicativo cliente:  
  
-   Execute o serviço de navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor.  
  
-   Crie um alias no cliente, especificando o pipe nomeado.  
  
-   Programe o cliente para se conectar usando uma cadeia de conexão personalizada.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-configure-the-named-pipe-used-by-the-sql-server-database-engine"></a>Configurar o pipe nomeado usado pelo Mecanismo de Banco de Dados do SQL Server  
  
1.  No SQL Server Configuration Manager, no painel de console, expanda **SQL Server configuração de rede**e clique em expandir **protocolos para** *\<instance name>* .  
  
2.  No painel de detalhes, clique com o botão direito do mouse em **Pipes Nomeados**e clique em **Propriedades**.  
  
3.  Na guia **Protocolo** , na caixa **Nome do Pipe** , digite o pipe no qual você deseja que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] escute e clique em **OK**.  
  
4.  No painel do console, clique em **Serviços do SQL Server**.  
  
5.  No painel de detalhes, clique com o botão direito do mouse em **SQL Server (** \<instance name> **)** e clique em **reiniciar**para parar e reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está escutando em um pipe alternativo, há três modos de se conectar a um pipe nomeado específico com um aplicativo cliente:  
  
-   Execute o serviço de navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor.  
  
-   Crie um alias no cliente, especificando o pipe nomeado.  
  
-   Programe o cliente para se conectar usando uma cadeia de conexão personalizada.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar ou excluir um alias de servidor para ser usado por um cliente &#40;SQL Server Configuration Manager&#41;](create-or-delete-a-server-alias-for-use-by-a-client.md)   
 [Configuração de rede do servidor](server-network-configuration.md)  
  
  
