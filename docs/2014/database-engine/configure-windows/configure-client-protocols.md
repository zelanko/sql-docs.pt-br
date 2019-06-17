---
title: Configurar protocolos de cliente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
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
ms.assetid: 3dfa2702-ba65-43b4-a777-6727846e133a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 331e062c86a65ce2be8fca4d07620156bab0a5e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813628"
---
# <a name="configure-client-protocols"></a>configurar protocolos de cliente
  Este tópico descreve como configurar protocolos de cliente usados por aplicativos cliente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. O Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte à comunicação cliente com o protocolo de rede TCP/IP e o protocolo de pipes nomeados. O protocolo de memória compartilhada também estará disponível se o cliente estiver se conectando a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no mesmo computador. Há três métodos comuns de selecionar o protocolo.  
  
-   Configure todos os aplicativos cliente para usar o mesmo protocolo de rede definindo a ordem de protocolo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
-   Configure um único aplicativo cliente para usar um protocolo de rede diferente criando um alias. Para obter mais informações, consulte [Criar ou excluir um alias de servidor para ser usado por um cliente &#40;SQL Server Configuration Manager&#41;](create-or-delete-a-server-alias-for-use-by-a-client.md).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Configurar a opção de configuração do servidor remote login timeout](configure-the-remote-login-timeout-server-configuration-option.md)  
  
  
