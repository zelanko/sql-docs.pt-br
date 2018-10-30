---
title: Configurar um servidor de relatório para administração remota | Microsoft Docs
ms.date: 09/14/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- WMI provider [Reporting Services], remote configuration
- configuration management [WMI]
- report servers [Reporting Services], configuring
- remote server administration [Reporting Services]
ms.assetid: 8c7f145f-3ac2-4203-8cd6-2a4694395d09
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 25ac3270e936f80bce62bdeeb67965c4688dfbcf
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50020330"
---
# <a name="configure-a-report-server-for-remote-administration"></a>Configurar um servidor de relatório para administração remota
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você pode configurar instâncias de servidor de relatório local ou remotamente. Para configurar uma instância remota do servidor de relatório, é possível usar a ferramenta Configuração do Reporting Services ou gravar código personalizado que use o provedor WMI (Instrumentação de Gerenciamento do Windows) do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . A ferramenta Configuração do Reporting Services fornece uma interface gráfica para o provedor WMI, de maneira que você possa configurar um servidor de relatório sem precisar gravar código. Ao iniciar a ferramenta, você pode especificar um servidor remoto para se conectar.  
  
 Para poder usar a ferramenta para configurar um servidor de relatório remoto, siga as instruções deste tópico para habilitar portas no Firewall do Windows, conexões remotas e solicitações WMI remotas.  
  
 A configuração apropriada ajuda a evitar o seguinte erro:  
  
 `The machine could not be found.`  
  
 `"The RPC server is unavailable. (Exception from HRESULT: 0x800706BA)".`  
  
## <a name="prerequisites"></a>Prerequisites  
 Para modificar as configurações do firewall, você deve fazer logon localmente e ser membro do grupo Administradores local. Não é possível modificar as configurações do firewall do Windows de um computador remoto via conexão remota.  
  
 Para habilitar a administração remota para um usuário que não seja administrador, você deve conceder à conta as permissões de Ativação Remota de DCOM (Distributed Component Object Model). As instruções sobre como configurar o servidor para acesso de não administrador estão descritas neste tópico.  
  
 Algumas organizações têm políticas de grupo que impedem a administração remota do servidor em determinados sistemas operacionais ou para determinados usuários. Antes de começar a modificar as configurações do firewall, verifique com o administrador da rede se há restrições de administração remota.  
  
 Para obter mais informações, consulte [Conectando-se pelo Firewall do Windows](https://go.microsoft.com/fwlink/?LinkId=63615) na documentação do Platform SDK disponível no MSDN.  
  
## <a name="tasks"></a>Tarefas  
 As tarefas que habilitam a configuração remota do servidor de relatório incluem as seguintes:  
  
-   Habilitar portas no Firewall do Windows para permitir solicitações nas portas usadas pelo servidor de relatório e pela instância do Mecanismo de Banco de Dados do SQL Server.  Consulte [Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) e [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
-   Habilitar conexões remotas com a instância do Mecanismo de Banco de Dados que hospeda o banco de dados do servidor de relatório. Uma conexão remota é necessária para configurar a conexão com o banco de dados do servidor de relatório e gerenciar as chaves de criptografia.  
  
-   Habilitar a passagem das solicitações WMI remotas pelo firewall do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
-   Se você estiver configurando um servidor de relatório remoto para administração por um usuário que não seja administrador, deverá configurar permissões DCOM para habilitar o acesso WMI remoto a uma conta de usuário padrão do Windows. Pelo fato de a WMI usar DCOM como transporte para chamadas remotas, você deve definir as permissões do DCOM para que os usuários que não fizeram logon como administrador local possam configurar o servidor.  
  
-   Se você estiver configurando um servidor de relatório remoto para administração por um usuário não administrativo, também deverá configurar permissões WMI no namespace WMI do servidor de relatório. Por padrão, todos os membros do grupo Administrador local têm acesso ao namespace WMI do servidor de relatório. Para conceder acesso a não administradores, você deve configurar permissões.  
  
 As instruções sobre como executar essas tarefas são fornecidas neste tópico.  
  
### <a name="to-configure-remote-connections-to-the-report-server-database"></a>Para configurar conexões remotas com o banco de dados do servidor de relatório  
  
1.  Clique em **Iniciar**, aponte para **Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
2.  No painel esquerdo, expanda **Configuração de Rede do SQL Server**e clique em **Protocolos** da instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  No painel de detalhes, habilite os protocolos TCP/IP e Pipes Nomeados e reinicie o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="to-enable-remote-administration-in-windows-firewall"></a>Para habilitar a administração remota no Firewall do Windows  
  
1.  Faça logon como administrador local no computador para o qual deseja habilitar a administração remota.  
  
2.  Abra um prompt de comando com privilégios administrativos.  
  
3.  Execute o seguinte comando:  
  
    ```  
    netsh.exe firewall set service type=REMOTEADMIN mode=ENABLE scope=ALL  
    ```  
  
     Você pode especificar diferentes opções para Escopo. Para obter mais informações, consulte a documentação do Firewall do Windows.  
  
4.  Verifique se a administração remota está habilitada. Você pode executar o seguinte comando para mostrar o status:  
  
    ```  
    netsh.exe firewall show state  
    ```  
  
5.  Reinicialize o computador.  
  
### <a name="to-set-dcom-permissions-to-enable-remote-wmi-access-for-non-administrators"></a>Para definir permissões DCOM a fim de habilitar o acesso WMI remoto para não administradores  
  
1.  No menu Iniciar, aponte para **Ferramentas Administrativas**e clique em **Serviços de Componentes**.  
  
     No Windows Vista, no menu Iniciar, clique em **Todos os Programas**, clique em **Executar**e digite **mmc comexp.msc**.  
  
2.  Abra a pasta Serviços de Componentes.  
  
3.  Abra a pasta Computadores.  
  
4.  Selecione Meu Computador.  
  
5.  No menu **Ação** , selecione **Propriedades**.  
  
6.  Clique em **Segurança COM**.  
  
7.  Em **Permissões de Inicialização e Ativação**, clique em **Editar Limites**.  
  
8.  Caso não veja seu nome em **Permissão de Inicialização**, clique em **Adicionar**.  
  
9. Digite o nome de sua conta de usuário e clique em **OK**.  
  
10. Em **Permissões para \<Usuário ou Grupo>**, na coluna **Permitir**, selecione **Inicialização Remota** e **Ativação Remota** e, em seguida, clique em **OK**.  
  
### <a name="to-set-permissions-on-the-report-server-wmi-namespace-for-non-administrators"></a>Para definir permissões no namespace WMI do servidor de relatório para não administradores  
  
1.  No menu Iniciar, aponte para **Ferramentas Administrativas**e clique em **Gerenciamento do Computador**.  
  
2.  Abra a pasta Serviços e Aplicativos.  
  
3.  Clique com o botão direito do mouse em **Controle WMI**e selecione **Propriedades**.  
  
4.  Clique em **Segurança**.  
  
5.  Abra a pasta Root.  
  
6.  Abra a pasta Microsoft.  
  
7.  Abra a pasta SQLServer.  
  
8.  Abra a pasta ReportServer.  
  
9. Abra a pasta da instância. Se você instalou a instância padrão, a pasta será MSSQLSERVER.  
  
10. Abra a pasta v10.  
  
11. Selecione a pasta Admin e clique em **Segurança**.  
  
12. Clique em **Adicionar**e digite a conta de usuário que você usará para gerenciar o servidor.  
  
13. Na coluna **Permitir** , selecione **Habilitar Conta**, **Ativação Remota**e **Ler Segurança**e clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
  
  
