---
title: "Configurar protocolos de cliente | Microsoft Docs"
ms.custom: ""
ms.date: "07/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "protocolos padrão"
  - "protocolos de rede [SQL Server], configuração do cliente"
  - "TCP/IP [SQL Server], protocolos de cliente"
  - "desabilitando protocolos de cliente"
  - "ordenando protocolos [SQL Server Agent]"
  - "protocolos [SQL Server], a ordem de computadores cliente"
  - "configurar protocolos de cliente"
  - "protocolos de cliente [SQL Server]"
  - "protocolos [SQL Server], configuração do cliente"
  - "protocolos padrão, cliente"
ms.assetid: 3dfa2702-ba65-43b4-a777-6727846e133a
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Configurar protocolos de cliente
  Este tópico descreve como configurar protocolos de cliente usados por aplicativos cliente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. O Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte à comunicação cliente com o protocolo de rede TCP/IP e o protocolo de pipes nomeados. O protocolo de memória compartilhada também estará disponível se o cliente estiver se conectando a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no mesmo computador. Há três métodos comuns de selecionar o protocolo.  
  
-   Configure todos os aplicativos cliente para usar o mesmo protocolo de rede definindo a ordem de protocolo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
-   Configure um único aplicativo cliente para usar um protocolo de rede diferente criando um alias. Para obter mais informações, consulte [Criar ou excluir um alias de servidor para ser usado por um cliente &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/create or delete a server alias for use by a client.md).  
  
-   Alguns aplicativos cliente, como sqlcmd.exe, podem especificar o protocolo como parte da cadeia de conexão. Para obter mais informações, veja [Conectar-se ao Mecanismo de Banco de Dados com sqlcmd](../../relational-databases/scripting/connect-to-the-database-engine-with-sqlcmd.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
###  <a name="EnableDisable"></a> Habilitar ou desabilitar um protocolo de cliente  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, expanda **Configuração do SQL Server Native Client**, clique com o botão direito do mouse em **Protocolos de Cliente** e clique em **Propriedades**.  
  
2.  Clique em um protocolo na caixa **Protocolos Desabilitados** e clique em **Habilitar** para habilitar um protocolo.  
  
3.  Clique em um protocolo na caixa **Protocolos Habilitados** e clique em **Desabilitar** para desabilitar um protocolo.  
  
###  <a name="ChangeDefault"></a> Alterar o protocolo padrão ou a ordem de protocolo para computadores cliente  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, expanda **Configuração do SQL Server Native Client**, clique com o botão direito do mouse em **Protocolos de Cliente** e clique em **Propriedades**.  
  
2.  Na caixa **Protocolos Habilitados**, clique em **Mover para Cima** ou **Mover para Baixo** para alterar a ordem na qual os protocolos são usados ao tentar uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O primeiro protocolo na caixa **Protocolos Habilitados** é o protocolo padrão.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Configuration Manager cria entradas de Registro para as configurações de alias de servidor e biblioteca de rede de cliente padrão. No entanto, o aplicativo não instala as bibliotecas nem os protocolos de rede do cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As bibliotecas de rede do cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são instaladas durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; os protocolos de rede são instalados como parte da Instalação do Microsoft Windows (ou em **Redes** no **Painel de Controle**). Um protocolo de rede específico pode não estar disponível como parte da Instalação do Windows. Para obter mais informações sobre como instalar esses protocolos de rede, consulte a documentação do fornecedor.  
  
###  <a name="Configure"></a> Configurar um cliente para usar TCP/IP  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, expanda **Configuração do SQL Server Native Client**, clique com o botão direito do mouse em **Protocolos de Cliente** e clique em **Propriedades**.  
  
2.  Na caixa **Protocolos Habilitados**, clique nas setas para cima e para baixo para alterar a ordem na qual os protocolos são tentados, quando tentar se conectar ao SQL Server. O primeiro protocolo na caixa **Protocolos Habilitados** é o protocolo padrão.  
  
 O protocolo de memória compartilhada é habilitado separadamente, marcando a caixa **Protocolo de Memória Compartilhada Habilitada**.  
  
## Consulte também  
 [Configurar a opção de configuração de servidor remote login timeout](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md)  
  
  