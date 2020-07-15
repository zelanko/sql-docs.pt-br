---
title: Configurar um servidor para escutar em um pipe alternativo | Microsoft Docs
description: Descubra como configurar o pipe nomeado no qual o Mecanismo de Banco de Dados do SQL Server escuta. Saiba como conectar um aplicativo cliente a um pipe nomeado específico.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- listening [SQL Server], pipes
- pipes [SQL Server], alternate
- alternate pipes [SQL Server]
ms.assetid: 914f7491-e2be-4b0d-b3aa-fe5409cdbafa
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fb0d7b15cf17ac1af60dbb55382dc1886fcca9a2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789777"
---
# <a name="configure-a-server-to-listen-on-an-alternate-pipe"></a>Configurar um servidor para escutar em um pipe alternativo
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como configurar um servidor para escutar em um pipe alternativo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. Por padrão, a instância padrão do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] escuta em um pipe chamado \\\\.\pipe\sql\query. As instâncias nomeadas do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e do [!INCLUDE[ssEW](../../includes/ssew-md.md)] escutam em outros pipes.  
  
 Há três modos de se conectar a um pipe nomeado específico com um aplicativo cliente:  
  
-   Execute o serviço de navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor.  
  
-   Crie um alias no cliente, especificando o pipe nomeado.  
  
-   Programe o cliente para se conectar usando uma cadeia de conexão personalizada.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-configure-the-named-pipe-used-by-the-sql-server-database-engine"></a>Configurar o pipe nomeado usado pelo Mecanismo de Banco de Dados do SQL Server  
  
1.  No SQL Server Configuration Manager, no painel de console, expanda **Configuração de Rede do SQL Server** e clique para expandir **Protocolos para** *\<instance name>* .  
  
2.  No painel de detalhes, clique com o botão direito do mouse em **Pipes Nomeados**e clique em **Propriedades**.  
  
3.  Na guia **Protocolo** , na caixa **Nome do Pipe** , digite o pipe no qual você deseja que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] escute e clique em **OK**.  
  
4.  No painel do console, clique em **Serviços do SQL Server**.  
  
5.  No painel de detalhes, clique com o botão direito do mouse em **SQL Server (** \<instance name> **)** e depois clique em **Reiniciar** para interromper e reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está escutando em um pipe alternativo, há três modos de se conectar a um pipe nomeado específico com um aplicativo cliente:  
  
-   Execute o serviço de navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor.  
  
-   Crie um alias no cliente, especificando o pipe nomeado.  
  
-   Programe o cliente para se conectar usando uma cadeia de conexão personalizada.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar ou excluir um alias de servidor para ser usado por um cliente &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)   
 [Configuração de rede do servidor](../../database-engine/configure-windows/server-network-configuration.md)  
  
  
