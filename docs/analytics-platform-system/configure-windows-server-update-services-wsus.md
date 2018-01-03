---
title: Configurar o Windows Server Update Services (WSUS) (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a10b2884-468e-41ef-bd59-8df894381254
caps.latest.revision: "41"
ms.openlocfilehash: 234c1ee3b13f3440e3f8a0377f3423ccf937acbc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="configure-windows-server-update-services-wsus"></a>Configurar o Windows Server Update Services (WSUS)
Essas instruções orientam você durante as etapas para usar o Assistente de configuração do Windows Server Update Services (WSUS) para configurar o WSUS para Analytics Platform System. Você precisa configurar o WSUS antes de aplicar as atualizações de software para o dispositivo. WSUS já está instalado na máquina virtual do VMM do dispositivo.  
  
Para obter mais informações sobre como configurar o WSUS, consulte o [guia de instalação passo a passo do WSUS](http://go.microsoft.com/fwlink/?LinkId=202417) no site do WSUS. Depois de configurar o WSUS, consulte [baixar e aplicar atualizações da Microsoft &#40; Analytics Platform System &#41; ](download-and-apply-microsoft-updates.md) para iniciar uma atualização.  
  
> [!WARNING]  
> Se você encontrar erros durante esse processo de configuração, pare e entre em contato com o suporte para obter assistência. Não ignorar erros ou continuar o processo após erros são recebidos.  
  
## <a name="before-you-begin"></a>Antes de começar  
Para configurar o WSUS, você precisa:  
  
-   Ter informações de logon de conta de administrador a Analytics Platform System dispositivo domínio.  
  
-   Ter um logon Analytics Platform System com permissões para acessar o **Console de administração** e exibir informações de estado do dispositivo.  
  
-   Sabe o endereço IP do servidor upstream do WSUS se você planeja sincronizar as atualizações em um servidor upstream do WSUS, em vez de sincronizar atualizações diretamente do Microsoft Update. Verifique se o servidor upstream do WSUS está configurado para permitir conexões anônimas e oferece suporte a SSL.  
  
-   Sabe o endereço IP do servidor proxy se seu dispositivo estiver usando um servidor proxy para acessar o servidor upstream ou o Microsoft Update.  
  
-   Na maioria dos casos, o WSUS precisa acessar servidores fora do dispositivo. Para dar suporte a esse cenário de uso, o sistema de plataforma de análise de DNS pode ser configurado para dar suporte a um encaminhador de nome externo que permitirá que os hosts Analytics Platform System e máquinas virtuais (VMs) usar servidores DNS externos para resolver nomes fora das dispositivo. Para obter mais informações, consulte [usar um encaminhador de DNS para resolver nomes de DNS do dispositivo não &#40; Analytics Platform System &#41; ](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>Para configurar o Windows Server Update Services (WSUS)  
  
1.  Faça logon na **Console de administração**. No **estado do dispositivo** , verifique se que o **Cluster** e **rede** colunas mostram verdes (ou **NA**) para todos os nós. Verifique se os indicadores de status de todos os nós no **estado de dispositivo**.  
  
    -   É seguro continuar verde ou indicadores NA.  
  
    -   Avalie os erros não críticos de aviso (amarelo). Em alguns casos mensagens de aviso não bloqueará as atualizações. Se houver um erro de volume de disco não críticos que não está na unidade C:\, você pode continuar para a próxima etapa antes de resolver o erro de volume do disco.  
  
    -   A maioria dos indicadores vermelhos devem ser resolvidos antes de continuar. Se houver falhas de disco, use o **alertas do Console do administrador** página para verificar se há falha de não mais de um disco em cada servidor ou uma matriz SAN. Se houver falha de não mais de um disco em cada servidor ou uma matriz SAN, você pode prosseguir para a próxima etapa antes de corrigir as falhas de disco. Certifique-se de entrar em contato com o suporte da Microsoft para corrigir as falhas de disco mais rápido possível.  
  
2.  Faça logon máquina virtual do VMM como um administrador de domínio do dispositivo.  
  
3.  Inicie o Assistente de configuração.  
  
    #### <a name="to-launch-the-configuration-wizard"></a>Para iniciar o Assistente de configuração  
  
    1.  No **painel do Gerenciador do servidor**, no **ferramentas** menu, clique em **Windows Server Update Services**.  
  
    2.  No painel esquerdo do **Update Services** janela, clique para expandir o servidor de gerenciamento de máquinas virtuais do nó (***appliance_domain*- VMM**) e, em seguida, clique em **Opções**.  
  
    3.  No **opções** painel, clique em **Assistente de configuração do servidor do WSUS** para iniciar o Assistente de configuração.  
  
        ![Menu do painel do Gerenciador do servidor](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  Se esta for a primeira vez que você executou o Assistente do WSUS, você poderá ser solicitado a configurar um diretório para armazenar as atualizações. `C:\wsus`é um local apropriado; No entanto, você pode fornecer um caminho diferente.  
  
        ![Caminho WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  Examine o **antes de começar** lista de itens para concluir antes de concluir o assistente.  
  
        ![Antes de começar o WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  Sobre o **ingressar no programa de aperfeiçoamento do Microsoft Update** página, selecione **Sim, gostaria de ingressar no programa de aperfeiçoamento do Microsoft Update**e, em seguida, clique em **próximo**.  
  
        ![Programa de aperfeiçoamento do WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    Agora você deve ver o **escolher servidor Upstream** página. Captura de tela a seguir é o ponto inicial do Assistente de configuração.  
  
    ![Sincronização do servidor Upstream do WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  Escolha o servidor upstream.  
  
    Sobre o **escolher servidor Upstream** página do Assistente de configuração do WSUS, você selecionará como o WSUS no nó de gerenciamento de máquina Virtual se conectará a um servidor upstream para obter atualizações de software. As duas opções são sincronizar o servidor upstream com [Microsoft Update](http://go.microsoft.com/fwlink/?LinkId=133349) ou sincronizar atualizações com outro servidor do Windows Server Update Services.  
  
    #### <a name="to-update-by-using-microsoft-update"></a>Para atualizar usando o Microsoft Update  
  
    1.  Se você optar por sincronizar com o Microsoft Update, você não precisa fazer alterações para o **escolher servidor Upstream** página. Clique em **Avançar**.  
  
        ![Sincronização do servidor Upstream do WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>Para atualizar a partir de outro servidor do WSUS  
  
    1.  Se você optar por sincronizar com uma fonte que não seja o Microsoft Update (um servidor upstream), especifique o servidor (Insira o endereço IP) e a porta em que esse servidor se comunicará com o servidor upstream.  
  
        ![Sincronização de WSUS do servidor Upstream do WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  Para usar o protocolo (SSL), selecione o **usar SSL ao sincronizar informações de atualização** caixa de seleção. Nesse caso os servidores usarão a porta 443 para sincronização.  
  
        ![Sincronização do servidor Upstream do WSUS de SSL do WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  Se este for um servidor de réplica, selecione o **for uma réplica do servidor upstream** caixa de seleção. É possível selecionar ambos **usar SSL ao sincronizar informações de atualização** e **for uma réplica do servidor upstream**.  
  
        ![Réplica do servidor Upstream do WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  Neste ponto, você tiver terminado com a configuração do servidor upstream. Clique em **próximo**, ou selecione **especifique um servidor proxy** no painel de navegação esquerdo.  
  
5.  Especifique o servidor proxy.  
  
    Se este servidor requer um servidor proxy para acessar o Microsoft Update ou outro servidor upstream, você pode configurar as configurações do servidor proxy aqui. Caso contrário, clique em **próximo**.  
  
    ![Proxy WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>Para definir configurações de servidor proxy  
  
    1.  Sobre o **especificar servidor Proxy** página do Assistente de configuração, selecione o **usar um servidor proxy ao sincronizar** caixa de seleção e, em seguida, digite o endereço IP de servidor de proxy (não o nome) e o número da porta (porta 80 por o padrão) nas caixas correspondentes.  
  
    2.  Se você deseja se conectar ao servidor proxy usando credenciais de usuário específicas, selecione o **usar credenciais de usuário para se conectar ao servidor proxy** caixa de seleção e, em seguida, digite o nome de usuário, domínio e senha do usuário correspondente caixas. Se você deseja habilitar a autenticação básica para o usuário se conectar ao servidor proxy, selecione o **permitir autenticação básica (a senha é enviada em texto não criptografado)** caixa de seleção.  
  
        ![Credenciais do Proxy WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  Neste ponto, você tiver terminado com a configuração do servidor proxy. Clique em **próximo** para ir para a próxima página, onde você pode começar a configurar o processo de sincronização.  
  
6.  Inicie a conexão.  
  
    ![Iniciar conexão do Proxy WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    Clique em **Iniciar conexão**.  
  
    Depois que a conexão for bem-sucedida, clique em **próximo** para ir para a próxima página, onde você pode escolher os idiomas.  
  
7.  Escolha os idiomas.  
  
    Selecione **baixar atualizações somente nestes idiomas**.  
  
    Selecione **inglês**e, em seguida, clique em **próximo**.  
  
    ![Escolher os idiomas](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  Escolha produtos.  
  
    > [!NOTE]  
    > Se você estiver usando um servidor Upstream, você não poderá escolher produtos. Se essa opção não estiver disponível, ignore esta etapa.  
  
    Cancele a seleção de todas as atualizações selecionadas.  
  
    Selecione **SQL Server 2014**, **Windows Server 2012 R2**, e **System Center 2012 R2 - Virtual Machine Manager**e, em seguida, clique em **próximo**.  
  
9. Escolha as classificações.  
  
    > [!NOTE]  
    > Se você estiver usando um servidor Upstream, pode não ser capaz de escolher classificações.  Se essa opção não estiver disponível, ignore esta etapa.  
  
    Cancele a seleção de todas as atualizações selecionadas anteriormente.  
  
    Selecione **atualizações críticas** e **atualizações de segurança** para as atualizações que serão sincronizadas para o dispositivo de sistema de plataforma de análise e, em seguida, clique em **próximo**.  
  
    ![Escolha classificações](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseClassifications.png "SQL_Server_PDW_WSUSChooseClassifications")  
  
10. Configure o agendamento de sincronização.  
  
    Selecione **sincronizar manualmente**e, em seguida, clique em **próximo**.  
  
    ![Definir agenda de sincronização](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. Começar a sincronização inicial.  
  
    Selecione **começar a sincronização inicial**, em seguida, clique em **próximo**.  
  
12. Conclua.  
  
    Clique em **Concluir**.  
  
## <a name="bkmk_WSUSGroup"></a>Grupo de servidores de dispositivo no WSUS  
Depois de configurar o WSUS para Analytics Platform System, a próxima etapa é agrupar os servidores de aplicativo. Adicionando todos os servidores de dispositivo a um grupo, o WSUS poderá aplicar atualizações de software para todos os servidores no dispositivo.  
  
> [!NOTE]  
> O sistema do WSUS foi projetado para ser executado de forma assíncrona. Iniciar atividade nem sempre resulta em uma atualização imediatamente. Portanto, talvez seja necessário aguardar um pouco até que os computadores serão visíveis nas caixas de diálogo do WSUS. Executando o `setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"` comando descrito no final do tópico [baixar e aplicar atualizações da Microsoft &#40; Analytics Platform System &#41; ](download-and-apply-microsoft-updates.md) pode ajudar a atualizar as caixas de diálogo.  
  
#### <a name="to-group-the-appliance-servers"></a>Para agrupar os servidores de aplicativo  
  
1.  Abra o console do WSUS, clique no **todos os computadores** e, em seguida, clique em **adicionar grupo de computadores**.  
  
    ![Adicione um grupo de computadores. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  Insira o nome "APS" para o grupo de computadores e, em seguida, clique em **adicionar**.  
  
    ![Insira um nome para seu novo grupo de computadores. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  Clique em **todos os computadores** novamente, alterar o status no **Status** menu suspenso para **qualquer**e, em seguida, clique em **atualizar**. Você pode precisar expandir **todos os computadores** clicando no controle de árvore à esquerda para ver o novo grupo que você acabou de adicionar.  
  
    ![Alterar o status para qualquer e clique em Atualizar. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  Selecione todos os computadores que fazem parte do dispositivo, com o botão direito e, em seguida, clique **alterar associação**.  
  
    ![Alterar a associação para todos os computadores PDW. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  Selecione o novo grupo de computadores que você criou clicando na caixa de seleção e, em seguida, clicando em **Okey**.  
  
    ![Associação de grupo de computadores do conjunto](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  Selecione o novo grupo de computadores, alterar seu **Status** para **qualquer**e, em seguida, clique em **atualizar**. Todos os computadores agora devem ser atribuídos a esse grupo e listados no painel direito. Geralmente é seguro continuar quando nós mostram avisos como **esse nó não relatou o status ainda**.  
  
    ![Alterar o Status para qualquer e clique em Atualizar. ] (./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
  
