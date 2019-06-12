---
title: Configurar um servidor de relatório no modo nativo para a Administração Local (SSRS) | Microsoft Docs
ms.date: 05/28/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- UAC
- installing Reporting Services
- Windows Vista
- Localhost
- windows server 2008
- Vista
ms.assetid: 312c6bb8-b3f7-4142-a55f-c69ee15bbf52
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 35355b32c8e4b59618cf146d9de04f3242ec6e6a
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403271"
---
# <a name="configure-a-native-mode-report-server-for-local-administration-ssrs"></a>Configurar um servidor de relatório no modo nativo para a Administração Local (SSRS)
  A implantação de um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um dos seguintes sistemas operacionais exigirá mais etapas de configuração se você desejar administrar localmente a instância do servidor de relatório. Este tópico explica como configurar o servidor de relatório para administração local. Se você ainda não tiver instalado ou configurado o servidor de relatório, confira [Instalar o SQL Server por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) e [Gerenciar um servidor de relatório no modo nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo|  
  
-   [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)]  
  
-   [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]  
  
-   [!INCLUDE[win8](../../includes/win8-md.md)]  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
-   [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
-   [!INCLUDE[win7](../../includes/win7-md.md)]  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
 Como o sistema operacional destacado limita as permissões, os membros do grupo Administradores local executam a maioria dos aplicativos como se estivessem usando a conta de Usuário Padrão.  
  
 Embora essa prática melhore a segurança geral do sistema, ela impede que você use as atribuições de funções internas predefinidas que o Reporting Services cria para administradores locais.  
  
-   [Visão geral de alterações de configuração](#bkmk_configuraiton_overview)  
  
-   [Para configurar um Servidor de Relatório Local e uma Administração do portal da Web](#bkmk_configure_local_server)  
  
-   [Para configurar o SQL Server Management Studio (SSMS) para a administração de servidor de relatórios local](#bkmk_configure_ssms)  
  
-   [Para configurar o SQL Server Data Tools (SSDT) para publicar um Servidor de Relatórios Local](#bkmk_configure_ssdt)  
  
-   [Informações adicionais](#bkmk_addiitonal_informaiton)  
  
##  <a name="bkmk_configuraiton_overview"></a> Visão geral de alterações de configuração  
 As seguintes alterações de configuração configuram o servidor para que você possa usar permissões de usuário padrão para gerenciar o conteúdo e as operações do servidor de relatório:  
  
-   Adicione URLs do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a sites confiáveis. Por padrão, o Internet Explorer que é executado nos sistemas operacionais listados é executado no **Modo Protegido**, um recurso que impede que solicitações do navegador alcancem processos de nível superior executados no mesmo computador. Você pode desabilitar o modo protegido para os aplicativos do servidor de relatório adicionando-os como Sites Confiáveis.  
  
-   Crie atribuições de função que concedam a você, o administrador do servidor de relatório, permissão para gerenciar o conteúdo e as operações, sem precisar usar o recurso **Executar como administrador** no Internet Explorer. Ao criar atribuições de funções para sua conta de usuário do Windows, você obtém acesso a um servidor de relatório com permissões de Gerenciador de Conteúdo e Administrador do Sistema por meio de atribuições explícitas de funções que substituem as atribuições de funções internas predefinidas que o Reporting Services cria.  
  
##  <a name="bkmk_configure_local_server"></a> Para configurar um Servidor de Relatório local e uma administração do portal da Web  
 Conclua as etapas de configuração nessa seção se você estiver navegando para um servidor de relatórios local e vir erros semelhantes ao seguinte:  
  
-   O usuário `'Domain\[user name]`' não tem as permissões necessárias. Verifique se as permissões suficientes foram concedidas e as restrições do UAC (Controle da conta de usuário) do Windows foram resolvidas.  
  
###  <a name="bkmk_site_settings"></a> Configurações de site confiável no navegador  
  
1.  Abra uma janela do navegador com permissões Executar como administrador. No menu **Iniciar**, clique com o botão direito do mouse em **Internet Explorer** e selecione **Executar como administrador**.  
  
2.  Selecione **Sim** quando solicitado para continuar.  
  
3.  No endereço de URL, insira a URL no portal da Web. Para obter instruções, acesse [O portal da Web de um servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/web-portal-ssrs-native-mode.md).  
  
4.  Clique em **Ferramentas**.  
  
5.  Clique em **Opções da Internet**.  
  
6.  Clique em **Segurança**.  
  
7.  Clique em **Sites Confiáveis**.  
  
8.  Clique em **Sites**.  
  
9. Adicione `https://<your-server-name>`.  
  
10. Desmarque a caixa de seleção **Exigir certificação do servidor (https:) para todos os sites desta zona** se não estiver usando HTTPS para o site padrão.  
  
11. Clique em **Adicionar**.  
  
12. Escolha **OK**.  
  
###  <a name="bkmk_configure_folder_settings"></a> Configurações de pasta do portal da Web  
  
1.  No portal da Web, na página inicial, clique em **Gerenciar pasta**.  
  
2.  Na página da pasta **Gerenciar**, clique em **Segurança** e, em seguida, selecione **Adicionar grupo ou usuário**.  
  
3.  Na página **Atribuição de Nova Função**, no campo **Grupo ou usuário**, digite a conta de usuário do Windows neste formato: `<domain>\<user>`.  
  
5.  Selecione **Gerenciador de Conteúdo**.  
  
6.  Escolha **OK**.  
  
###  <a name="bkmk_configure_site_settings"></a> Configurações de site do portal da Web  
  
1.  Abra seu navegador com privilégios administrativos e navegue até o portal da Web, `https://<server name>/reports`.  
  
2.  Selecione o ícone de engrenagem na linha superior da Página inicial e, em seguida **Configurações do Site** no menu suspenso. 
  
    ![Ícone de engrenagem](../media/ssrsgearmenu.png).
    >[!TIP]  
    >**Observação:** se a opção **Configurações do Site** não for exibida, feche e reabra o navegador, e navegue até o portal da Web com privilégios administrativos.  
  
3.  Na página Configurações do site, selecione **Segurança** e, em seguida, selecione **Adicionar grupo ou usuário**.  
  
4.  No campo **Nome do grupo ou do usuário** , conta de usuário do Windows neste formato: `<domain>\<user>`.  

5.  Selecione **Administrador do Sistema**.  
  
6.  Escolha **OK**.  
  
7.  Fechar portal da Web.  
  
8. Abra novamente o portal da Web no Internet Explorer sem usar **Executar como administrador**.  
  
##  <a name="bkmk_configure_ssms"></a> Para configurar o SQL Server Management Studio (SSMS) para a administração de servidor de relatórios local  
 Por padrão, você não pode acessar todas as propriedades do servidor de relatório disponíveis no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] a menos que inicie o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] com privilégios administrativos.  
  
 **Para configurar as atribuições de função do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]** , você não precisa iniciar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] com permissões elevadas a cada vez:  
  
-   No menu **Iniciar**, clique com botão direito em **Microsoft SQL Server [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]** e, em seguida, clique em **Executar como administrador**.  
  
-   Conecte-se ao servidor do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] local.  
  
-   No nó **Segurança** , clique em **Funções do Sistema**.  
  
-   Clique com o botão direito do mouse em **Administrador do Sistema** e clique em **Propriedades**.  
  
-   Na página **Propriedades de Função do Sistema** , selecione **Exibir propriedades do servidor de relatório**. Selecione as outras propriedades que você quer associar aos membros da função administradores do sistema.  
  
-   Clique em **OK**.  
  
-   Feche o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   Para adicionar um usuário à função do sistema "administrador do sistema", confira a seção [Configurações do Site do portal da Web](#bkmk_configure_site_settings) anteriormente neste artigo.  
  
 Agora, quando você abre o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e não seleciona explicitamente **Executar como administrador** , tem acesso às propriedades do servidor de relatório.  
  
##  <a name="bkmk_configure_ssdt"></a> Para configurar o SSDT (SQL Server Data Tools) para publicar em um servidor de relatório local  
 Se você instalou o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] em um dos sistemas operacionais listados na primeira seção desse tópico, e quiser que o SSDT interaja com um servidor de relatório de modo Nativo local, receberá erros de permissão a menos que abra o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] com permissões elevadas ou configure as funções de serviços de relatório. Por exemplo, se você não tiver permissões adequadas, terá problemas semelhantes aos seguintes:  
  
-   Quando você tentar implantar itens de relatório no servidor de relatório local, verá uma mensagem de erro semelhante à seguinte na janela **Lista de Erros** :  
  
    -   As permissões concedidas ao usuário 'Domain\\<nome de usuário\>' são insuficientes para a execução dessa operação.  
  
 **Para executar com permissões elevadas a cada vez que você abrir o SSDT:**  
  
1.  No menu Iniciar, selecione **Microsoft SQL Server** e, em seguida, clique com o botão direito em **SQL Server Data Tools**. Clique em **Executar como administrador**  
  
2.  Selecione **Sim** quando solicitado para continuar.  
  
Agora você deve poder implantar relatórios e outros itens em um servidor de relatório local.  
  
 **Para configurar as atribuições de função do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você não precisa iniciar o SSDT com permissões elevadas a cada vez:**  
  
-   Confira as seções [Configurações da pasta do portal da Web](#bkmk_configure_folder_settings) e [Configurações do Site do portal da Web](#bkmk_configure_site_settings) anteriores neste tópico.  
  
##  <a name="bkmk_addiitonal_informaiton"></a> Informações adicionais  
 Uma etapa de configuração adicional e comum relacionada à administração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é abrir a porta 80 no Windows Firewall para permitir o acesso ao computador do servidor de relatório. Para obter instruções, consulte [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
## <a name="see-also"></a>Confira também  
 [Gerenciar um servidor de relatórios de Modo Nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
