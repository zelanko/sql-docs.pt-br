---
title: Configurar um servidor para escutar em uma porta TCP específica (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- fixed port
- static ports
- ports [SQL Server], assigning numbers
- assigning port numbers
- dynamic ports [SQL Server]
- TCP/IP [SQL Server], port numbers
ms.assetid: 2276a5ed-ae3f-4855-96d8-f5bf01890640
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cfe8a35e9ba0a23edb3fc08833ab015ddbd2f119
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935820"
---
# <a name="configure-a-server-to-listen-on-a-specific-tcp-port-sql-server-configuration-manager"></a>Configurar um servidor para escuta em uma porta TCP específica (SQL Server Configuration Manager)
  Este tópico descreve como configurar uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para escutar em uma porta fixa específica usando o SQL Server Configuration Manager. Se habilitada, a instância padrão do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] escutará na porta TCP 1433. As instâncias nomeadas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e do [!INCLUDE[ssEW](../../includes/ssew-md.md)] são configuradas para portas dinâmicas. Isso significa que elas selecionam uma porta disponível quando o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado. Ao conectar-se a uma instância nomeada através de um firewall, configure o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para escutar em uma porta específica, para que a porta adequada possa ser aberta no firewall.  
  
 Para obter mais informações sobre as configurações padrão do Firewall do Windows e uma descrição das portas TCP que afetam o Mecanismo de Banco de Dados, o Analysis Services, o Reporting Services e o Integration Services, veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
> [!TIP]  
>  Ao selecionar um número de porta, consulte [http://www.iana.org/assignments/port-numbers](http://www.iana.org/assignments/port-numbers) para obter uma lista de números de porta que são atribuídos a aplicativos específicos. Selecione um número de porta não atribuído. Para obter mais informações, consulte [O intervalo de porta dinâmica para TCP/IP mudou no Windows Vista e no Windows Server 2008](https://support.microsoft.com/kb/929851).  
  
> [!WARNING]  
>  O mecanismo de banco de dados começa a escutar em uma nova porta quando é reiniciado. Entretanto, o serviço de Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] monitora o Registro e relata o novo número de porta, assim que a configuração é alterada, mesmo que o mecanismo de banco de dados não esteja usando essa porta. Reinicie o mecanismo de banco de dados para garantir a consistência e evitar falhas de conexão.  
  
 **Neste tópico**  
  
-   **Para configurar um servidor para escutar em uma porta TCP específica usando:**  
  
     [SQL Server Configuration Manager](#SSMSProcedure)  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-assign-a-tcpip-port-number-to-the-sql-server-database-engine"></a>Para atribuir um número de porta TCP/IP ao Mecanismo de Banco de Dados do SQL Server  
  
1.  No SQL Server Configuration Manager, no painel de console, expanda **SQL Server configuração de rede**, expanda **protocolos para \<instance name> **e clique duas vezes em **TCP/IP**.  
  
2.  Na caixa de diálogo **Propriedades de TCP/IP** , na guia **Endereços IP** , vários endereços IP aparecem no formato **IP1**, **IP2**, até **IPAll**. Um desses é para o endereço IP do adaptador de loopback, 127.0.0.1. Endereços IP adicionais aparecem para cada Endereço IP no computador. Clique com o botão direito do mouse em cada endereço e clique em **Propriedades** para identificar o endereço IP que você deseja configurar.  
  
3.  Se a caixa de diálogo **Portas TCP Dinâmicas** contiver **0**, indicando que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] está escutando em portas dinâmicas, exclua o 0.  
  
4.  Na caixa de **Propriedades** **IP**_n_ , na caixa **porta TCP** , digite o número da porta que você deseja que esse endereço IP escute e clique em **OK**.  
  
5.  No painel de console, clique em **Serviços do SQL Server**.  
  
6.  No painel de detalhes, clique com o botão direito do mouse em **SQL Server (** \<instance name> **)** e clique em **reiniciar**para parar e reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Após configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para escutar em uma porta específica, há três maneiras de se conectar a uma porta específica com um aplicativo cliente:  
  
-   Execute o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor para conectar-se à instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] pelo nome.  
  
-   Crie um alias no cliente, especificando o número da porta.  
  
-   Programe o cliente para se conectar usando uma cadeia de conexão personalizada.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar ou excluir um alias de servidor para ser usado por um cliente &#40;SQL Server Configuration Manager&#41;](create-or-delete-a-server-alias-for-use-by-a-client.md)  
  
  
