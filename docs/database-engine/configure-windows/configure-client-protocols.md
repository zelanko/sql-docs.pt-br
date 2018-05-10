---
title: Configurar protocolos de cliente | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- default protocols
- network protocols [SQL Server], client configuration
- TCP/IP [SQL Server], client protocols
- disabling client protocols
- ordering protocols [SQL Server]
- protocols [SQL Server], order for client computers
- configure client protocols
- client protocols [SQL Server]
- protocols [SQL Server], client configuration
- default protocols, client
ms.assetid: 3dfa2702-ba65-43b4-a777-6727846e133a
caps.latest.revision: 35
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0602c0605ac549184d7eee0fa752d28c0c591367
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-client-protocols"></a>configurar protocolos de cliente
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como configurar protocolos de cliente usados por aplicativos cliente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. O Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte à comunicação cliente com o protocolo de rede TCP/IP e o protocolo de pipes nomeados. O protocolo de memória compartilhada também estará disponível se o cliente estiver se conectando a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no mesmo computador. Há três métodos comuns de selecionar o protocolo.  
  
-   Configure todos os aplicativos cliente para usar o mesmo protocolo de rede definindo a ordem de protocolo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
-   Configure um único aplicativo cliente para usar um protocolo de rede diferente criando um alias. Para obter mais informações, consulte [Criar ou excluir um alias de servidor para ser usado por um cliente &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md).  
  
-   Alguns aplicativos cliente, como sqlcmd.exe, podem especificar o protocolo como parte da cadeia de conexão. Para obter mais informações, veja [Conectar-se ao Mecanismo de Banco de Dados com sqlcmd](../../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
###  <a name="EnableDisable"></a> Para habilitar ou desabilitar um protocolo de cliente  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, expanda **Configuração do SQL Server Native Client**, clique com o botão direito do mouse em **Protocolos de Cliente** e clique em **Propriedades**.  
  
2.  Clique em um protocolo na caixa **Protocolos Desabilitados** e clique em **Habilitar** para habilitar um protocolo.  
  
3.  Clique em um protocolo na caixa **Protocolos Habilitados** e clique em **Desabilitar** para desabilitar um protocolo.  
  
###  <a name="ChangeDefault"></a> Para alterar o protocolo padrão ou a ordem de protocolo para computadores cliente  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, expanda **Configuração do SQL Server Native Client**, clique com o botão direito do mouse em **Protocolos de Cliente** e clique em **Propriedades**.  
  
2.  Na caixa **Protocolos Habilitados**, clique em **Mover para Cima** ou **Mover para Baixo** para alterar a ordem na qual os protocolos são usados ao tentar uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O primeiro protocolo na caixa **Protocolos Habilitados** é o protocolo padrão.  
  
    > [!IMPORTANT]  
    >  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager cria entradas de registro para as configurações de alias de servidor e biblioteca de rede de cliente padrão. No entanto, o aplicativo não instala as bibliotecas nem os protocolos de rede do cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As bibliotecas de rede do cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são instaladas durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; os protocolos de rede são instalados como parte da Instalação do Microsoft Windows (ou em **Redes** no **Painel de Controle**). Um protocolo de rede específico pode não estar disponível como parte da Instalação do Windows. Para obter mais informações sobre como instalar esses protocolos de rede, consulte a documentação do fornecedor.  
  
###  <a name="Configure"></a> Para configurar um cliente para usar TCP/IP  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, expanda **Configuração do SQL Server Native Client**, clique com o botão direito do mouse em **Protocolos de Cliente** e clique em **Propriedades**.  
  
2.  Na caixa **Protocolos Habilitados**, clique nas setas para cima e para baixo para alterar a ordem na qual os protocolos são tentados, quando tentar se conectar ao SQL Server. O primeiro protocolo na caixa **Protocolos Habilitados** é o protocolo padrão.  
  
 O protocolo de memória compartilhada é habilitado separadamente, marcando a caixa **Protocolo de Memória Compartilhada Habilitada**.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar a opção de configuração do servidor remote login timeout](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md)  
  
  
