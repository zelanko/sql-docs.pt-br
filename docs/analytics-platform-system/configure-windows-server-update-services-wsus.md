---
title: Configurar o WSUS
description: Estas instruções orientam você pelas etapas para usar o assistente de configuração do Windows Server Update Services (WSUS) para configurar o WSUS para o Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 089b76d7167b8561c93b01837dc2189c833362fd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "76761900"
---
# <a name="configure-windows-server-update-services-wsus-in-analytics-platform-system"></a>Configurar o Windows Server Update Services (WSUS) no Analytics Platform System
Estas instruções orientam você pelas etapas para usar o assistente de configuração do Windows Server Update Services (WSUS) para configurar o WSUS para o Analytics Platform System. Você precisa configurar o WSUS antes de poder aplicar as atualizações de software ao dispositivo. O WSUS já está instalado na máquina virtual do VMM do dispositivo.  
  
Para obter mais informações sobre como configurar o WSUS, consulte o [Guia de instalação passo a passo do WSUS](https://go.microsoft.com/fwlink/?LinkId=202417) no site do WSUS. Depois de configurar o WSUS, consulte [baixar e aplicar atualizações da Microsoft &#40;sistema de plataforma de análise&#41;](download-and-apply-microsoft-updates.md) para iniciar uma atualização.  
  
> [!WARNING]  
> Se você encontrar erros durante esse processo de configuração, pare e entre em contato com o suporte para obter assistência. Não ignore erros ou continue no processo após os erros serem recebidos.  
  
## <a name="before-you-begin"></a>Antes de começar  
Para configurar o WSUS, você precisa:  
  
-   Tenha as informações de logon da conta do administrador de domínio do dispositivo do Analytics Platform System.  
  
-   Ter um logon do sistema de plataforma de análise com permissões para acessar o **console de administração** e exibir informações de estado do dispositivo.  
  
-   Saiba o endereço IP do servidor WSUS upstream se você estiver planejando sincronizar atualizações de um servidor WSUS upstream em vez de sincronizar atualizações diretamente do Microsoft Update. Verifique se o servidor do WSUS upstream está definido para permitir conexões anônimas e dá suporte a SSL.  
  
-   Saiba o endereço IP do servidor proxy se seu dispositivo estiver usando um servidor proxy para acessar o servidor upstream ou Microsoft Update.  
  
-   Na maioria dos casos, o WSUS precisa acessar servidores fora do dispositivo. Para dar suporte a esse cenário de uso, o DNS do sistema da plataforma de análise pode ser configurado para dar suporte a um encaminhador de nome externo que permitirá que os hosts do sistema da plataforma de análise e VMs (máquinas virtuais) usem servidores DNS externos para resolver nomes fora do dispositivo. Para obter mais informações, consulte [usar um encaminhador DNS para resolver nomes DNS que não são de dispositivo &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="to-configure-windows-server-update-services-wsus"></a>Para configurar o Windows Server Update Services (WSUS)  
  
1.  Faça logon no **console de administração**. Na guia **estado do dispositivo** , verifique se as colunas de **rede** e de **cluster** mostram verde (ou **na**) para todos os nós. Verifique os indicadores de status de todos os nós no **estado do dispositivo**.  
  
    -   É seguro continuar com indicadores verdes ou NA.  
  
    -   Avalie erros de aviso não críticos (amarelos). Em alguns casos, as mensagens de aviso não bloquearão as atualizações. Se houver um erro de volume de disco não crítico que não esteja em C:\ , você pode prosseguir para a próxima etapa antes de resolver o erro de volume de disco.  
  
    -   A maioria dos indicadores vermelhos deve ser resolvida antes de continuar. Se houver falhas de disco, use a página de **alertas do console de administração** para verificar se não há mais de uma falha de disco em cada servidor ou matriz San. Se não houver mais de uma falha de disco em cada servidor ou matriz SAN, você poderá prosseguir para a próxima etapa antes de corrigir as falhas de disco. Lembre-se de entrar em contato com o suporte da Microsoft para corrigir as falhas de disco assim que possível.  
  
2.  Faça logon na máquina virtual do VMM como um administrador de domínio do dispositivo.  
  
3.  Inicie o assistente de configuração.  
  
    #### <a name="to-launch-the-configuration-wizard"></a>Para iniciar o assistente de configuração  
  
    1.  No **painel de Gerenciador do servidor**, no menu **ferramentas** , clique em **Windows Server Update Services**.  
  
    2.  No painel esquerdo da janela **serviços de atualização** , clique para expandir o servidor do nó de gerenciamento de máquinas virtuais (**_appliance_domain_-VMM**) e clique em **Opções**.  
  
    3.  No painel **Opções** , clique em **Assistente de configuração do servidor do WSUS** para iniciar o assistente de configuração.  
  
        ![Menu do painel do Gerenciador do Servidor](./media/configure-windows-server-update-services-wsus/WSUS_Wiz0.png "WSUS_Wiz0")  
  
    4.  Se esta for a primeira vez que você executou o assistente do WSUS, você poderá ser solicitado a configurar um diretório para armazenar as atualizações. `C:\wsus`é um local apropriado; no entanto, você pode fornecer um caminho diferente.  
  
        ![caminho WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz1.png "WSUS_Wiz1")  
  
    5.  Examine a lista de itens **antes de começar** antes de concluir o assistente.  
  
        ![Antes de começar o WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz2.png "WSUS_Wiz2")  
  
    6.  Na página **ingressar no programa de aperfeiçoamento de Microsoft Update** , selecione **Sim, eu gostaria de ingressar no programa de aperfeiçoamento de Microsoft Update**e, em seguida, clique em **Avançar**.  
  
        ![Programa de aperfeiçoamento do WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz3.png "WSUS_Wiz3")  
  
    Agora você deve ver a página **escolher servidor upstream** . A captura de tela a seguir é o ponto de partida do assistente de configuração.  
  
    ![Sincronização do Servidor Upstream WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
4.  Escolha o servidor upstream.  
  
    Na página **escolher servidor upstream** do assistente de configuração do WSUS, você selecionará como o WSUS no nó Gerenciamento de máquinas virtuais se conectará a um servidor upstream para obter atualizações de software. As duas opções são sincronizar o servidor upstream com [Microsoft Update](https://go.microsoft.com/fwlink/?LinkId=133349) ou sincronizar atualizações com outro servidor Windows Server Update Services.  
  
    #### <a name="to-update-by-using-microsoft-update"></a>Para atualizar usando Microsoft Update  
  
    1.  Se você optar por sincronizar com Microsoft Update, não será necessário fazer nenhuma alteração na página **escolher servidor upstream** . Clique em **Avançar**.  
  
        ![Sincronização do Servidor Upstream WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4a.png "WSUS_Wiz4a")  
  
    #### <a name="to-update-from-another-wsus-server"></a>Para atualizar de outro servidor do WSUS  
  
    1.  Se você optar por sincronizar com uma fonte diferente de Microsoft Update (um servidor upstream), especifique o servidor (Insira o endereço IP) e a porta na qual esse servidor irá se comunicar com o servidor upstream.  
  
        ![Sincronização do Servidor Upstream WSUS a partir do WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4b.png "WSUS_Wiz4b")  
  
    2.  Para usar protocolo SSL (SSL), marque a caixa de seleção **usar SSL ao sincronizar informações de atualização** . Nesse caso, os servidores usarão a porta 443 para sincronização.  
  
        ![Sincronização do Servidor Upstream WSUS a partir do WSUS SSL](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4c.png "WSUS_Wiz4c")  
  
    3.  Se esse for um servidor de réplica, marque a caixa de seleção **Esta é uma réplica do servidor upstream**. É possível selecionar ambos **usar SSL ao sincronizar informações de atualização** e **esta é uma réplica do servidor upstream**.  
  
        ![Réplica do Servidor Upstream WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz4d.png "WSUS_Wiz4d")  
  
    4.  Neste ponto, você concluiu a configuração do servidor upstream. Clique em **Avançar**ou selecione **especificar servidor proxy** no painel de navegação esquerdo.  
  
5.  Especifique o servidor proxy.  
  
    Se esse servidor exigir que um servidor proxy acesse Microsoft Update ou um servidor de upstream diferente, você poderá definir as configurações do servidor proxy aqui; caso contrário, clique em **Avançar**.  
  
    ![Proxy WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5a.png "WSUS_Wiz5a")  
  
    #### <a name="to-configure-proxy-server-settings"></a>Para definir as configurações de servidor proxy  
  
    1.  Na página **especificar servidor proxy** do assistente de configuração, marque a caixa de seleção **usar um servidor proxy ao sincronizar** e, em seguida, digite o endereço IP do servidor proxy (não nome) e o número da porta (porta 80 por padrão) nas caixas correspondentes.  
  
    2.  Se quiser se conectar ao servidor proxy usando credenciais de usuário específicas, marque a caixa de seleção **Utilize credenciais de usuário para se conectar ao servidor proxy** e digite o nome de usuário, o domínio e a senha nas caixas correspondentes. Se você quiser habilitar a autenticação básica para o usuário que está se conectando ao servidor proxy, marque a caixa de seleção **Permitir autenticação básica (senha enviada em texto não criptografado)** .  
  
        ![Credenciais do Proxy WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz5b.png "WSUS_Wiz5b")  
  
    3.  Neste ponto, você concluiu a configuração do servidor proxy. Clique em **Avançar** para acessar a próxima página, em que é possível começar a configuração do processo de sincronização.  
  
6.  Inicie a conexão.  
  
    ![Iniciar conexão do proxy WSUS](./media/configure-windows-server-update-services-wsus/WSUS_Wiz6.png "WSUS_Wiz6")  
  
    Clique em **Iniciar conexão**.  
  
    Depois que a conexão for bem-sucedida, clique em **Avançar** para ir para a próxima página, onde você pode escolher os idiomas.  
  
7.  Escolha idiomas.  
  
    Selecione **baixar atualizações somente nesses idiomas**.  
  
    Selecione **Inglês**e clique em **Avançar**.  
  
    ![Escolha idiomas](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseLanguages.png "SQL_Server_PDW_WSUSChooseLanguages")  
  
8.  Escolha produtos.  
  
    > [!NOTE]  
    > Se você estiver usando um servidor upstream, talvez não seja possível escolher produtos. Se essa opção não estiver disponível, ignore esta etapa.

    > [!WARNING]  
    > Exclua todas as atualizações do SQL Server 2016.
  
    Desmarque todas as atualizações selecionadas.  
  
    Selecione **SQL Server 2012**, **SQL Server 2014**, **Windows Server 2012 R2**e **System Center 2012 R2-Virtual Machine Manager**e clique em **Avançar**.  
  
9. Escolha classificações.  
  
    > [!NOTE]  
    > Se você estiver usando um servidor upstream, talvez não seja possível escolher classificações.  Se essa opção não estiver disponível, ignore esta etapa.  
  
    Desmarque todas as atualizações selecionadas anteriormente.  
  
    Selecione **atualizações críticas** e **atualizações de segurança** para as atualizações que serão sincronizadas para o dispositivo de sistema de plataforma de análise e clique em **Avançar**.  
  
    ![Escolha classificações](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChooseClassifications.png "SQL_Server_PDW_WSUSChooseClassifications")  
  
10. Configure a agenda de sincronização.  
  
    Selecione **sincronizar manualmente**e clique em **Avançar**.  
  
    ![Definir agenda de sincronização](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSyncSchedule.png "SQL_Server_PDW_WSUSSyncSchedule")  
  
11. Inicie a sincronização inicial.  
  
    Selecione **Iniciar sincronização inicial**e clique em **Avançar**.  
  
12. Concluir.  
  
    Clique em **Concluir**.  
  
## <a name="group-the-appliance-servers-in-wsus"></a><a name="bkmk_WSUSGroup"></a>Agrupar os servidores de dispositivo no WSUS  
Depois de configurar o WSUS para o Analytics Platform System, a próxima etapa é agrupar os servidores de dispositivo. Ao adicionar todos os servidores de dispositivo a um grupo, o WSUS poderá aplicar atualizações de software a todos os servidores do dispositivo.  
  
> [!NOTE]  
> O sistema WSUS foi projetado para ser executado de forma assíncrona. A atividade de inicialização nem sempre resulta em uma atualização imediata. Portanto, talvez seja necessário aguardar um pouco até que os computadores fiquem visíveis nas caixas de diálogo do WSUS. Executar o `setup.exe /action=ReportMicrosoftUpdateClientStatus /DomainAdminPassword="<password>"` comando descrito no final do tópico [baixar e aplicar as atualizações da Microsoft &#40;o Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) pode ajudar a atualizar as caixas de diálogo.  
  
#### <a name="to-group-the-appliance-servers"></a>Para agrupar os servidores de dispositivo  
  
1.  Abra o console do WSUS, clique com o botão direito do mouse em **todos os computadores** e clique em **Adicionar grupo de computadores**.  
  
    ![Adicione um grupo de computadores.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSAddComputerGroup.png "SQL_Server_PDW_WSUSAddComputerGroup")  
  
2.  Digite o nome "APS" para o grupo de computadores e clique em **Adicionar**.  
  
    ![Insira o nome do seu novo grupo de computadores.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSpecifyGroupName.png "SQL_Server_PDW_WSUSSpecifyGroupName")  
  
3.  Clique em **todos os computadores** novamente, altere o status no menu suspenso **status** para **qualquer**e clique em **Atualizar**. Talvez seja necessário expandir **todos os computadores** clicando nele no controle de árvore à esquerda para ver o novo grupo que você acabou de adicionar.  
  
    ![Altere o status para Qualquer e clique em Atualizar.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusToAny.png "SQL_Server_PDW_WSUSChangeStatusToAny")  
  
4.  Selecione todos os computadores que fazem parte do dispositivo, clique com o botão direito do mouse em e clique em **Alterar Associação**.  
  
    ![Altere a associação de todos os computadores PDW.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeMembership.png "SQL_Server_PDW_WSUSChangeMembership")  
  
5.  Selecione o novo grupo de computadores que você criou clicando na caixa de seleção e, em seguida, clicando em **OK**.  
  
    ![Defina Associação a Grupos de Computadores](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSSetComputerGroupMembership.png "SQL_Server_PDW_WSUSSetComputerGroupMembership")  
  
6.  Selecione o novo grupo de computadores, altere seu **status** para **qualquer**e clique em **Atualizar**. Todos os computadores agora devem ser atribuídos a esse grupo e listados no painel direito. Em geral, é seguro continuar quando os nós mostrarem avisos como **este nó ainda não relataram o status**.  
  
    ![Altere o status para qualquer e clique em atualizar.](./media/configure-windows-server-update-services-wsus/SQL_Server_PDW_WSUSChangeStatusAnyRefresh.png "SQL_Server_PDW_WSUSChangeStatusAnyRefresh")  
  
