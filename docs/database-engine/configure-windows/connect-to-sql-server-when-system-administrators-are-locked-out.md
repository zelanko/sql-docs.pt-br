---
title: Conectar-se ao SQL Server quando os administradores do sistema estão bloqueados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- connecting when locked out [SQL Server]
- locked out [SQL Server]
ms.assetid: c0c0082e-b867-480f-a54b-79f2a94ceb67
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 573ddefa33c1e021c16359f0164f0eda49d329fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012107"
---
# <a name="connect-to-sql-server-when-system-administrators-are-locked-out"></a>Conectar-se ao SQL Server quando os administradores do sistema estão bloqueados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como você pode recuperar o acesso ao [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] como administrador do sistema. Um administrador do sistema pode perder o acesso a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devido a um dos seguintes motivos:  
  
-   Todos os logons que são membros da função de servidor fixa sysadmin foram removidos por engano.  
  
-   Todos os Grupos do Windows que são membros da função de servidor fixa sysadmin foram removidos por engano.  
  
-   Os logons que são membros da função de servidor fixa sysadmin são para indivíduos que deixaram a empresa ou que não estão disponíveis.  
  
-   A conta sa está desabilitada ou ninguém sabe a senha.  
  
 Um modo para recuperar o acesso é reinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e conectar todos os bancos de dados à nova instância. Essa solução é demorada; e recuperar os logons talvez exija a restauração do banco de dados mestre de um backup. Se o backup do banco de dados mestre for mais antigo, talvez ele não tenha todas a informações. Se o backup do banco de dados mestre for mais recente, ele poderá ter os mesmos logons da instância anterior, portanto, os administradores ainda serão bloqueados.  
  
## <a name="resolution"></a>Resolução  
 Inicie a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único usando as opções **-m** ou **-f** . Qualquer membro do grupo de Administradores locais do computador pode conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como membro da função de servidor fixa sysadmin.  
  
> [!NOTE]  
>  Ao iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único, primeiro interrompa o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Caso contrário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent poderá se conectar primeiro e impedir sua conexão como um segundo usuário.  
  
 Ao usar a opção **-m** com **sqlcmd** ou [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você pode limitar as conexões a um aplicativo cliente especificado. Por exemplo, **-m"sqlcmd"** limita as conexões a uma única conexão e essa conexão deve se identificar como o programa cliente **sqlcmd** . Use essa opção quando estiver iniciando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único e se um aplicativo cliente desconhecido estiver usando a única conexão disponível. Para se conectar por meio do Editor de Consultas no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], use **-m"Microsoft SQL Server Management Studio - Query"** .  
  
> [!IMPORTANT]  
>  Não use essa opção como um recurso de segurança. O aplicativo cliente fornece o nome do aplicativo cliente e pode fornecer um nome falso como parte da cadeia de conexão.  
  
 Para obter instruções passo a passo sobre como iniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único, veja [Configurar opções de inicialização do servidor &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
## <a name="step-by-step-instructions"></a>Instruções passo a passo  
 As instruções a seguir descrevem o processo de conexão com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em execução no Windows 8 ou superior. São fornecidos pequenas ajustes para as versões anteriores do SQL Server ou do Windows. Essas instruções deverão ser executadas enquanto você estiver conectado ao Windows como membro do grupo de administradores locais, e assumem que o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] está instalado no computador.  
  
1.  Na página inicial, inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No menu **Exibir** , selecione **Servidores Registrados**. (Se o servidor ainda não estiver registrado, clique com o botão direito do mouse em **Grupos de Servidores Locais**, aponte para **Tarefas**e clique em **Registrar Servidores Locais**.)  
  
2.  Na área Servidores Registrados, clique com o botão direito do mouse no servidor e clique em **SQL Server Configuration Manager**. Será solicitada permissão para realizar a execução como administrador e, em seguida, o programa Configuration Manager será aberto.  
  
3.  Feche o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
4.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no painel esquerdo, selecione **Serviços do SQL Server**. No painel direito, localize a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. (A instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui **(MSSQLSERVER)** após o nome do computador. As instâncias nomeadas aparecem em maiúsculas com o mesmo nome apresentado na área Servidores Registrados.) Clique com o botão direito do mouse na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e clique em **Propriedades**.  
  
5.  Na guia **Parâmetros de Inicialização**, na caixa **Especificar um parâmetro de inicialização**, digite `-m` e clique em **Adicionar**. (É um traço seguido da letra m minúscula.)  
  
    > [!NOTE]  
    >  Em algumas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , não há nenhuma guia **Parâmetros de Inicialização** . Nesse caso, na guia **Avançado** , clique duas vezes em **Parâmetros de Inicialização**. Os parâmetros são abertos em uma janela muito pequena. Tenha cuidado para não alterar os parâmetros existentes. No final, adicione um novo parâmetro `;-m` e clique em **OK**. (É um ponto-e-vírgula seguido da letra m minúscula.)  
  
6.  Clique em **OK**e, após a mensagem de reinicialização, clique com o botão direito do mouse no nome do servidor e clique em **Reiniciar**.  
  
7.  Depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reiniciar, o servidor estará no modo de usuário único. Verifique se o Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está em execução. Se for iniciado, ele usará sua única conexão.  
  
8.  Na tela inicial do Windows 8, clique com o botão direito do mouse no ícone do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Na parte inferior da tela, selecione **Executar como administrador**. (As credenciais do administrador serão passadas para o SSMS.)  
  
    > [!NOTE]  
    >  Nas versões anteriores do Windows, a opção **Executar como administrador** aparece como um submenu.  
  
     Em algumas configurações, o SSMS tentará criar várias conexões. Várias conexões falharão porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está no modo de usuário único. Você pode selecionar uma das seguintes ações para executar. Execute uma delas.  
  
    1.  Conecte-se ao Pesquisador de Objetos usando a autenticação do Windows (que inclui as credenciais do administrador). Expanda **Segurança**, expanda **Logons**e clique duas vezes no seu próprio logon. Na página **Funções de Servidor** , selecione **sysadmin**e clique em **OK**.  
  
    2.  Em vez de conectar-se ao Pesquisador de Objetos, conecte-se à Janela de Consulta usando a autenticação do Windows (que inclui as credenciais do administrador). (Você só poderá se conectar dessa maneira se não tiver se conectado ao Pesquisador de Objetos.) Execute o código da seguinte maneira para adicionar um novo logon de autenticação do Windows que é membro da função de servidor fixa **sysadmin** . O exemplo a seguir adiciona um usuário de domínio chamado `CONTOSO\PatK`.  
  
        ```  
        CREATE LOGIN [CONTOSO\PatK] FROM WINDOWS;  
        ALTER SERVER ROLE sysadmin ADD MEMBER [CONTOSO\PatK];  
        ```  
  
    3.  Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver sendo executado no modo de autenticação mista, conecte-se a uma Janela de Consulta usando a autenticação do Windows (que inclui as credenciais do administrador). Execute o código da seguinte maneira para criar um novo logon de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é membro da função de servidor fixa **sysadmin** .  
  
        ```  
        CREATE LOGIN TempLogin WITH PASSWORD = '************';  
        ALTER SERVER ROLE sysadmin ADD MEMBER TempLogin;  
        ```  
  
        > [!WARNING]  
        >  Substitua ************ por uma senha forte.  
  
    4.  Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver sendo executado no modo de autenticação mista e você quiser redefinir a senha da conta **sa** , conecte-se a uma Janela de Consulta usando a Autenticação do Windows (que inclui as credenciais do Administrador). Alterar a senha da conta **sa** com a sintaxe a seguir.  
  
        ```  
        ALTER LOGIN sa WITH PASSWORD = '************';  
        ```  
  
        > [!WARNING]  
        >  Substitua ************ por uma senha forte.  
  
9. Agora, as etapas a seguir alteram o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] novamente para o modo de vários usuários. Feche o SSMS.  
  
10. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no painel esquerdo, selecione **Serviços do SQL Server**. No painel direito, clique com o botão direito do mouse na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e clique em **Propriedades**.  
  
11. Na guia **Parâmetros de Inicialização** , na caixa **Parâmetros existentes** , selecione `-m` e clique em **Remover**.  
  
    > [!NOTE]  
    >  Em algumas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , não há nenhuma guia **Parâmetros de Inicialização** . Nesse caso, na guia **Avançado** , clique duas vezes em **Parâmetros de Inicialização**. Os parâmetros são abertos em uma janela muito pequena. Remova o `;-m` que você adicionou anteriormente e clique em **OK**.  
  
12. Clique com o botão direito do mouse no nome do servidor e clique em **Reiniciar**.  
  
 Você poderá se conectar normalmente a uma das contas, que agora é membro da função de servidor fixa de **sysadmin** .  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o SQL Server no modo de usuário único](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)   
 [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
