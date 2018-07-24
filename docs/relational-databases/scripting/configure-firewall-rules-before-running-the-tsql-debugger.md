---
title: Configurar regras de firewall antes de executar o Depurador TSQL | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.debug.error.sqlde_register_failed
- vs.debug.error.sqlde_accessdenied
- vs.debug.error.sqlde_firewall.remotemachines
helpviewer_keywords:
- Transact-SQL debugger, remote connections
- Windows Firewall [Database Engine], Transact-SQL debugger
- Transact-SQL debugger, Windows Firewall
- Transact-SQL debugger, configuring
- ports [SQL Server], Transact-SQL debugger
- TCP/IP [SQL Server], port numbers
ms.assetid: f50e0b0d-eaf0-4f4a-be83-96f5be63e7ea
caps.latest.revision: 43
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: db859f697a40e6ee8135335ee7c16efb29e6584a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37989428"
---
# <a name="configure-firewall-rules-before-running-the-tsql-debugger"></a>Configurar regras de firewall antes de executar o Depurador TSQL
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  As regras do Firewall do Windows devem ser configuradas para habilitar a depuração do [!INCLUDE[tsql](../../includes/tsql-md.md)] quando conectado a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que esteja em execução em outro computador que não o do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="configuring-the-transact-sql-debugger"></a>Configurando o Depurador Transact-SQL  
 O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] inclui componentes do lado do servidor e do lado do cliente. Os componentes do depurador do servidor são instalados com cada instância do Mecanismo de Banco de Dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2 (Service Pack 2) ou posterior. Os componentes do depurador do lado do cliente são incluídos:  
  
-   Ao instalar as ferramentas do lado do cliente do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior.  
  
-   Ao instalar o Microsoft Visual Studio 2010 ou posterior.  
  
-   Ao instalar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] via download da Web.  
  
 Não há requisitos de configuração para executar o depurador do [!INCLUDE[tsql](../../includes/tsql-md.md)] quando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] está sendo executado no mesmo computador da instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. No entanto, para executar o depurador do [!INCLUDE[tsql](../../includes/tsql-md.md)] quando ele estiver conectado a uma instância remota do [!INCLUDE[ssDE](../../includes/ssde-md.md)], as regras de programas e portas no Firewall do Windows devem ser habilitadas nos dois computadores. Essas regras podem ser criadas na instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você obtiver erros ao tentar abrir uma sessão remota de depuração, verifique se as regras de firewall a seguir estão definidas em seu computador.  
  
 Use o aplicativo **Firewall do Windows com Segurança Avançada** para gerenciar as regras de firewall. No [!INCLUDE[win7](../../includes/win7-md.md)] e no [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)], abra **Painel de Controle**, abra **Firewall do Windows**e selecione **Configurações avançadas**. No [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] , você também pode abrir **Service Manager**, expandir **Configuração** no painel esquerdo e expandir **Firewall do Windows com Segurança Avançada**.  
  
> [!CAUTION]  
>  A habilitação de regras no Firewall do Windows pode expor o computador a ameaças de segurança contra as quais o firewall foi projetado para bloquear. A habilitação de regras para depuração remota desbloqueia as portas e os programas listados neste tópico.  
  
## <a name="firewall-rules-on-the-server"></a>Regras de firewall no servidor  
 No computador que executa a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], use **Firewall do Windows com Segurança Avançada** para especificar as seguintes informações:  
  
-   Adicione uma regra de entrada de programa a sqlservr.exe. Você deve ter uma regra para cada instância que precisa dar suportar a sessões remotas de depuração.  
  
    1.  Em **Firewall do Windows com Segurança Avançada**, no painel esquerdo, clique com o botão direito do mouse em **Regras de Entrada**e selecione **Nova Regra** no painel de ações.  
  
    2.  Na caixa de diálogo **Tipo de Regra** , selecione **Programa**e clique em **Avançar**.  
  
    3.  Na caixa de diálogo **Programa** , selecione **Este caminho de programa:** e insira o caminho completo para sqlservr.exe dessa instância. Por padrão, sqlservr.exe é instalado em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.*InstanceName*\MSSQL\Binn, em que *InstanceName* é MSSQLSERVER para a instância padrão ou o nome de qualquer instância nomeada.  
  
    4.  Na caixa de diálogo **Ação** , selecione **Permitir a conexão**e clique em **Avançar**.  
  
    5.  Na caixa de diálogo **Perfil** , selecione qualquer perfil que descreva o ambiente de conexão do computador quando você quiser abrir a sessão de depuração com a instância e clique em **Avançar**.  
  
    6.  Na caixa de diálogo **Nome** , digite um nome e uma descrição para essa regra e clique em **Concluir**.  
  
    7.  Na lista **Regras de Entrada** , clique com o botão direito do mouse na regra que você criou e selecione **Propriedades** no painel de ações.  
  
    8.  Selecione a guia **Protocolos e Portas** .  
  
    9. Selecione **TCP** na caixa **Tipo de protocolo:** , selecione **Portas Dinâmicas RPC** na caixa **Porta local:** , clique em **Aplicar**e clique em **OK**.  
  
-   Adicione uma regra de entrada de programa a svchost.exe para habilitar comunicações DCOM de sessões remotas do depurador.  
  
    1.  Em **Firewall do Windows com Segurança Avançada**, no painel esquerdo, clique com o botão direito do mouse em **Regras de Entrada**e selecione **Nova Regra** no painel de ações.  
  
    2.  Na caixa de diálogo **Tipo de Regra** , selecione **Programa**e clique em **Avançar**.  
  
    3.  Na caixa de diálogo **Programa** , selecione **Este caminho de programa:** e insira o caminho completo para sqlservr.exe. Por padrão, svchost.exe é instalado em %systemroot%\ System32\svchost.exe.  
  
    4.  Na caixa de diálogo **Ação** , selecione **Permitir a conexão**e clique em **Avançar**.  
  
    5.  Na caixa de diálogo **Perfil** , selecione qualquer perfil que descreva o ambiente de conexão do computador quando você quiser abrir a sessão de depuração com a instância e clique em **Avançar**.  
  
    6.  Na caixa de diálogo **Nome** , digite um nome e uma descrição para essa regra e clique em **Concluir**.  
  
    7.  Na lista **Regras de Entrada** , clique com o botão direito do mouse na regra que você criou e selecione **Propriedades** no painel de ações.  
  
    8.  Selecione a guia **Protocolos e Portas** .  
  
    9. Selecione **TCP** na caixa **Tipo de protocolo:** , selecione **Mapeador de Pontos de Extremidade RPC** na caixa **Porta local:** , clique em **Aplicar**e clique em **OK**.  
  
-   Se a política do domínio exigir que as comunicações de rede sejam feitas via IPsec, você também deverá adicionar regras de entrada para abrir as portas UDP 4500 e 500.  
  
## <a name="firewall-rules-on-the-client"></a>Regras de firewall no cliente  
 No computador que executa o Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , a instalação do SQL Server ou a instalação do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] pode ter configurado o Firewall do Windows para permitir a depuração remota.  
  
 Se você obtiver erros ao tentar abrir uma sessão de depuração remota, poderá configurar as exceções de programas e portas usando o **Firewall do Windows com Segurança Avançada** para configurar regras de firewall:  
  
-   Adicione uma entrada de programa a svchost:  
  
    1.  Em **Firewall do Windows com Segurança Avançada**, no painel esquerdo, clique com o botão direito do mouse em **Regras de Entrada**e selecione **Nova Regra** no painel de ações.  
  
    2.  Na caixa de diálogo **Tipo de Regra** , selecione **Programa**e clique em **Avançar**.  
  
    3.  Na caixa de diálogo **Programa** , selecione **Este caminho de programa:** e insira o caminho completo para sqlservr.exe. Por padrão, svchost.exe é instalado em %systemroot%\ System32\svchost.exe.  
  
    4.  Na caixa de diálogo **Ação** , selecione **Permitir a conexão**e clique em **Avançar**.  
  
    5.  Na caixa de diálogo **Perfil** , selecione qualquer perfil que descreva o ambiente de conexão do computador quando você quiser abrir a sessão de depuração com a instância e clique em **Avançar**.  
  
    6.  Na caixa de diálogo **Nome** , digite um nome e uma descrição para essa regra e clique em **Concluir**.  
  
    7.  Na lista **Regras de Entrada** , clique com o botão direito do mouse na regra que você criou e selecione **Propriedades** no painel de ações.  
  
    8.  Selecione a guia **Protocolos e Portas** .  
  
    9. Selecione **TCP** na caixa **Tipo de protocolo:** , selecione **Mapeador de Pontos de Extremidade RPC** na caixa **Porta local:** , clique em **Aplicar**e clique em **OK**.  
  
-   Adicione uma entrada de programa ao aplicativo que hospeda o Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Se você precisar abrir sessões remotas de depuração no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] no mesmo computador, adicione uma regra de programa a ambas:  
  
    1.  Em **Firewall do Windows com Segurança Avançada**, no painel esquerdo, clique com o botão direito do mouse em **Regras de Entrada**e selecione **Nova Regra** no painel de ações.  
  
    2.  Na caixa de diálogo **Tipo de Regra** , selecione **Programa**e clique em **Avançar**.  
  
    3.  Na caixa de diálogo **Programa** , selecione **Este caminho de programa:** e insira um destes três valores.  
  
        -   Para o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], insira o caminho completo para ssms.exe. Por padrão, ssms.exe é instalado em C:\Arquivos de Programas (x86)\Microsoft SQL Server\130\Tools\Management Studio.  
  
        -   Para o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] , insira o caminho completo para devenv.exe:  
  
            1.  Por padrão, o arquivo devenv.exe do Visual Studio 2010 está em C:\Arquivos de Programas (x86)\Microsoft Visual Studio 10.0\Common7\IDE.  
  
            2.  Por padrão, o arquivo devenv.exe do Visual Studio 2012 está em C:\Arquivos de Programas (x86)\Microsoft Visual Studio 11.0\Common7\IDE  
  
            3.  Você pode encontrar o caminho para ssms.exe a partir do atalho usado para iniciar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você pode encontrar o caminho para devenv.exe a partir do atalho usado para iniciar o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Clique com o botão direito do mouse no atalho e selecione **Propriedades**. O executável e o caminho são listados na caixa de **Destino** .  
  
    4.  Na caixa de diálogo **Ação** , selecione **Permitir a conexão**e clique em **Avançar**.  
  
    5.  Na caixa de diálogo **Perfil** , selecione qualquer perfil que descreva o ambiente de conexão do computador quando você quiser abrir a sessão de depuração com a instância e clique em **Avançar**.  
  
    6.  Na caixa de diálogo **Nome** , digite um nome e uma descrição para essa regra e clique em **Concluir**.  
  
    7.  Na lista **Regras de Entrada** , clique com o botão direito do mouse na regra que você criou e selecione **Propriedades** no painel de ações.  
  
    8.  Selecione a guia **Protocolos e Portas** .  
  
    9. Selecione **TCP** na caixa **Tipo de protocolo:** , selecione **Portas Dinâmicas RPC** na caixa **Porta local:** , clique em **Aplicar**e clique em **OK**.  
  
## <a name="requirements-for-starting-the-debugger"></a>Requisitos para iniciar o depurador  
 Todas as tentativas de iniciar o depurador do [!INCLUDE[tsql](../../includes/tsql-md.md)] também devem atender aos seguintes requisitos:  
  
* [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] deve estar sendo executado em uma conta do Windows que seja membro da função de servidor fixa sysadmin.  
  
* A janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve ser conectada usando um logon de Autenticação do Windows ou Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que seja um membro da função de servidor fixa sysadmin.  
  
* A janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve estar conectada a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 (SP2) ou posterior. Não é possível executar o depurador quando a janela do Editor de Consultas está conectada a uma instância que está no modo de usuário único.

* O servidor precisa se comunicar com o cliente via RPC. A conta sob a qual o serviço do SQL Server está em execução deve ter permissões de autenticação no cliente  
  
## <a name="see-also"></a>Consulte Também  
 [Depurador do Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Executar o depurador Transact-SQL](../../relational-databases/scripting/run-the-transact-sql-debugger.md)   
 [Percorrer código Transact-SQL](../../relational-databases/scripting/step-through-transact-sql-code.md)   
 [Informações do depurador Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [Editor de Consultas do Mecanismo de Banco de Dados &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)  
  
  
