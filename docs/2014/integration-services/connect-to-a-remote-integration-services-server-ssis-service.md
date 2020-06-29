---
title: Conectar-se a um servidor de Integration Services remoto (serviço SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- service [Integration Services], remote instance
- Integration Services service, connecting
- Integration Services service, remote instance
- service [Integration Services], connecting
ms.assetid: 9487aff1-44d8-42c1-8176-bb9891d4632d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 48369c2691386bc41675571c892302e3e4b7ece1
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85434653"
---
# <a name="connect-to-a-remote-integration-services-server-ssis-service"></a>Conectar-se a um servidor remoto do Integration Services (serviço SSIS)
    
> [!IMPORTANT] 
> Esse tópico discute o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , um serviço do Windows para o gerenciamento de pacotes do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] dá suporte ao serviço para compatibilidade de versões anteriores com versões anteriores do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. A partir do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], você pode gerenciar objetos como pacotes no servidor do Integration Services.  
  
 Para se conectar a uma instância do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em um servidor remoto, a partir do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou de outro aplicativo de gerenciamento, é necessário um conjunto específico de direitos no servidor para os usuários do aplicativo.  
  
> [!IMPORTANT] 
> Para gerenciar pacotes armazenados em um servidor remoto, você não precisa conectar-se à instância do serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] naquele servidor remoto. Em vez disso, edite o arquivo de configuração do serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] de forma que o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] exiba os pacotes armazenados no servidor remoto. Para obter mais informações, consulte [Configurando o Serviço Integration Services &#40;Serviço SSIS#41;](service/integration-services-service-ssis-service.md).  
  
## <a name="connecting-to-integration-services-on-a-remote-server"></a>Conectando-se ao Integration Services em um servidor remoto  
  
#### <a name="to-connect-to-integration-services-on-a-remote-server"></a>Para se conectar ao Integration Services em um servidor remoto  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  Selecione **Arquivo**, **Conectar Pesquisador de Objetos** para exibir a caixa de diálogo **Conectar ao Servidor** .  
  
3.  Selecione **Integration Services** na lista **Tipo de servidor** .  
  
4.  Digite o nome de um servidor [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] na caixa de texto **Nome do servidor**.  
  
    > [!NOTE]  
    >  O serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] não é específico da instância. Você se conecta ao serviço usando o nome do computador no qual o serviço Integration Services está sendo executado.  
  
5.  Clique em **Conectar**.  
  
> [!NOTE]  
>  A caixa de diálogo **Procurar Servidores** não exibe instâncias remotas do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Além disso, as opções disponíveis na guia **Opções de conexão** da caixa de diálogo **Conectar ao Servidor** , exibida ao clicar no botão **Opções** , não é aplicável às conexões [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="eliminating-the-access-is-denied-error"></a>Eliminando o erro “Acesso negado”  
 Quando um usuário sem direitos suficientes tenta se conectar a uma instância do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em um servidor remoto, o servidor responde com uma mensagem de erro “Acesso negado”. Você pode evitar essa mensagem de erro verificando se os usuários têm as permissões DCOM exigidas.  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-server-2003-or-windows-xp"></a>Para configurar direitos para os usuários remotos no Windows Server 2003 ou no Windows XP  
  
1.  Se o usuário não for um membro do grupo local Administradores, adicione o usuário ao grupo Usuários de COM Distribuída. Você pode fazer isso no snap-in do MMC do Gerenciamento do Computador acessado pelo menu **Ferramentas Administrativas** .  
  
2.  Abra o Painel de Controle, clique duas vezes em **Ferramentas Administrativas** e clique duas vezes em **Serviços de Componentes** para iniciar o snap-in do MMC dos Serviços de Componentes.  
  
3.  Expanda o nó **Serviços de Componentes** no painel esquerdo do console. Expanda o nó **Computadores** , expanda **Meu Computador**e clique no nó **Configuração de DCOM** .  
  
4.  Selecione o nó **Configuração de DCOM** e selecione SQL Server Integration Services 11.0 na lista de aplicativos que podem ser configurados.  
  
5.  Clique com o botão direito do mouse em SQL Server Integration Services 11.0 e selecione **Propriedades**.  
  
6.  Na caixa de diálogo **Propriedades do SQL Server Integration Services 11.0** , selecione a guia **Segurança** .  
  
7.  Em **Permissões de Inicialização e Ativação**, selecione **Personalizar**e clique em **Editar** para abrir a caixa de diálogo **Permissão de Inicialização** .  
  
8.  Na caixa de diálogo **Permissão de Inicialização** , adicione ou exclua usuários e atribua as permissões adequadas aos usuários e grupos apropriados. As permissões disponíveis são Inicialização Local, Inicialização Remota, Ativação Local e Ativação Remota. Os direitos de Inicialização concedem ou negam permissão para iniciar e parar o serviço; os direitos de Ativação concedem ou negam permissão para conexão com o serviço.  
  
9. Clique em OK para fechar a caixa de diálogo.  
  
10. Em **Permissões de acesso**, repita as etapas 7 e 8 para atribuir as permissões adequadas aos usuários e grupos apropriados.  
  
11. Feche o snap-in do MMC.  
  
12. Reinicie o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-2000-with-the-latest-service-packs"></a>Para configurar direitos para usuários remotos no Windows 2000 com os service packs mais recentes  
  
1.  Executar **dcomcnfg.exe** no prompt de comando.  
  
2.  Na página **Aplicativos** da caixa de diálogo **Propriedades de Configuração de COM Distribuída** , selecione SQL Server Integration Services 11.0 e clique em **Propriedades**.  
  
3.  Escolha a página **Segurança** .  
  
4.  Use as duas caixas de diálogo separadas para configurar as **Permissões de acesso** e as **Permissões de Inicialização**. Você não pode distinguir entre acesso remoto e local – as permissões de Acesso incluem acesso local e remoto e as permissões de Inicialização incluem inicialização local e remota.  
  
5.  Feche as caixas de diálogo e **dcomcnfg.exe**.  
  
6.  Reinicie o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="connecting-by-using-a-local-account"></a>Conectando-se através de uma conta local  
 Se você estiver trabalhando em uma conta local do Windows em um computador cliente, só poderá se conectar ao serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em um computador remoto se houver uma conta local com o mesmo nome e senha e os direitos apropriados no computador remoto.  
  
## <a name="by-default-the-ssis-service-does-not-support-delegation"></a>Por padrão, o serviço SSIS não oferece suporte para delegação  
Por padrão [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , o serviço não oferece suporte à delegação de credenciais ou às vezes chamado de salto duplo. Nesse cenário, você está trabalhando em um computador cliente, o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] está em execução em um segundo computador e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está em execução em um terceiro computador. Primeiro, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] passa com sucesso as credenciais do computador cliente para o segundo computador no qual o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] está em execução. Em seguida, no entanto, o serviço [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] não pode delegar suas credenciais do segundo computador para o terceiro computador no qual [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está em execução.

Você pode habilitar a delegação de credenciais concedendo o direito **Confiar neste usuário para delegação a qualquer serviço (apenas Kerberos)** para a conta de serviço do SQL Server, que inicia o serviço do Integration Services (ISServerExec.exe) como um processo filho. Antes de conceder esse direito, considere se ele atende aos requisitos de segurança de sua organização.

Para obter mais informações, consulte [Getting Cross Domain Kerberos and Delegation working with SSIS Package (Obtendo entre Kerberos do domínio e delegação de trabalhar com o pacote do SSIS)](https://blogs.msdn.microsoft.com/psssql/2014/06/26/getting-cross-domain-kerberos-and-delegation-working-with-ssis-package/).
  
## <a name="see-also"></a>Consulte Também  
 [Configurar um Firewall do Windows para acesso ao serviço SSIS](../../2014/integration-services/configure-a-windows-firewall-for-access-to-the-ssis-service.md)  
  
  
