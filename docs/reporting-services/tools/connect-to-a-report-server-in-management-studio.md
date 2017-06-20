---
title: "Conectar a um servidor de relatório no Management Studio | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connecttors.connectionproperties.f1
- sql13.swb.connecttors.login.f1
- sql13.swb.connection.login.reportserver.f1
helpviewer_keywords:
- report servers [Reporting Services], connections
- connections [Reporting Services], report server
- registering report servers
- report servers [Reporting Services], registering
- Connect to Server dialog box, Reporting Services
ms.assetid: c875ff87-ee7d-443a-a702-bdb4b6c27c6e
caps.latest.revision: 53
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 53ebe2ae1938dc656af351cf922f5d5d85d664b8
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="connect-to-a-report-server-in-management-studio"></a>Conectar-se a um servidor de relatório no Management Studio
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] fornece o Pesquisador de Objetos, que permite a conexão a qualquer servidor da família do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a navegação gráfica por seu conteúdo. Para o Reporting Services, você pode usar o Pesquisador de Objetos para fazer o seguinte:  
  
-   Habilitar os recursos de servidor de relatório.  
  
-   Definir padrões de servidor e configure definições de função.  
  
-   Gerenciar trabalhos em execução.  
  
-   Gerenciar agendas de trabalhos.  
  
 Você pode se conectar a um servidor de relatório de modo nativo ou a um servidor de relatório executado no modo integrado SharePoint. A sintaxe da conexão e os tipos de operações que você pode executar variam dependendo do modo do servidor de relatório e de suas permissões. Se estiver com problemas de conexão com um servidor de relatório ou de execução de tarefas específicas, pode ser devido a permissões não adequadas ou a você ter especificado o nome do servidor de relatório incorretamente. Para obter mais informações sobre permissões e sintaxe de conexão, consulte a tabela no final deste tópico.  
  
 Observe que você não pode usar o Pesquisador de Objetos para exibir ou gerenciar o conteúdo do servidor de relatório. O gerenciamento do conteúdo é feito pelo Gerenciador de Relatórios se o servidor de relatório estiver sendo executado no modo nativo ou por um site do SharePoint se o servidor de relatório estiver sendo executado no modo integrado do SharePoint.  
  
 O Pesquisador de Objetos permite que você abra conexões com diversas instâncias do servidor no mesmo espaço de trabalho desde que os servidores estejam registrados no mesmo grupo de servidores. Antes de você poder se conectar a uma instância do servidor de relatório no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], o servidor deve ser registrado. Se o servidor de relatório já tiver sido registrado, esta etapa poderá ser ignorada. As instruções para registrar servidores de relatório são fornecidas no final deste tópico.  
  
### <a name="to-connect-to-a-native-mode-report-server"></a>Para conectar-se a um servidor de relatório no modo nativo  
  
1.  Se o Pesquisador de Objetos ainda não estiver aberto, selecione-o no menu Exibir.  
  
2.  Clique em **Conectar** para exibir a lista de tipos de servidor e, então, selecione **Reporting Services**.  
  
3.  Na caixa de diálogo **Conectar-se ao Servidor** , digite o nome da instância do servidor de relatório. Os nomes das instâncias do servidor de relatório baseiam-se nos nomes das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por padrão, o nome da instância de um servidor de relatório local é apenas o nome do computador. Se você instalou o servidor de relatório como uma instância nomeada, use a seguinte sintaxe para especificar o servidor:  *\<servername > [\\< instancename\>]*.  
  
4.  Selecione o tipo de autenticação. Se você estiver usando a Autenticação do Windows, deverá se conectar usando suas credenciais. Se selecionar a autenticação Básica ou a autenticação Formulários, digite a conta e a senha.  
  
5.  Clique em **Conectar**. O servidor de relatório aparece no Pesquisador de Objetos.  
  
6.  Clique com o botão direito do mouse no nó do servidor para definir as propriedades do sistema e os padrões do servidor. Para obter mais informações, consulte [Definir propriedades do servidor de relatório &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md).  
  
### <a name="to-connect-to-a-sharepoint-integrated-mode-report-server"></a>Para conectar-se a um servidor de relatório no modo integrado do SharePoint   
  
1.  Se o Pesquisador de Objetos ainda não estiver aberto, selecione-o no menu Exibir.  
  
2.  Clique em Conectar para exibir a lista de tipos de servidor e, então, selecione **Reporting Services**.  
  
3.  Na caixa de diálogo **Conectar-se ao Servidor** , digite uma URL de um site do SharePoint. O exemplo a seguir ilustra a sintaxe: `http://<web server>/sites/<site>`.  
  
4.  Selecione o tipo de autenticação. Se você estiver usando a Autenticação do Windows, deverá se conectar usando suas credenciais. Se selecionar a autenticação Básica ou a autenticação Formulários, digite a conta e a senha.  
  
5.  Clique em **Conectar**. O servidor de relatório aparece no Pesquisador de Objetos.  
  
6.  Clique com o botão direito do mouse no nó do servidor para definir as propriedades do sistema e os padrões do servidor. Para obter mais informações, consulte [Definir propriedades do servidor de relatório &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md).  
  
### <a name="to-register-a-report-server"></a>Para registrar um servidor de relatório  
  
1.  Se não consegue se conectar a um servidor de relatório, ou você não tem permissão para acessá-lo ou ele deve ser registrado. Para registrar o servidor, clique em **Servidores Registrados** no menu Exibir,  
  
2.  Clique no ícone Reporting Services.  
  
3.  Clique com o botão direito do mouse em **Reporting Services**, aponte para **Novo**e clique em **Registro de Servidor**. A caixa de diálogo **Registro de Novo Servidor** é exibida.  
  
4.  Para **Nome do servidor**, digite um valor. O valor que você deve especificar variará, dependendo do modo do servidor:  
  
    -   Para um servidor de relatório de modo nativo, digite o nome da instância do servidor de relatório. Os nomes das instâncias do servidor de relatório baseiam-se nos nomes das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por padrão, o nome da instância de um servidor de relatório local é apenas o nome do computador. Se você instalou o servidor de relatório como uma instância nomeada, use a seguinte sintaxe para especificar o servidor:  *\<servername > [\\< instancename\>]*.  
  
    -   Para um servidor de relatório executado no modo integrado SharePoint, o servidor ao qual se conectar é o site do SharePoint ao qual o servidor está conectado. A conexão com o site do SharePoint é necessária de modo que você possa exibir os níveis de permissão que controlam o acesso às operações e ao conteúdo do servidor de relatório. Você pode especificar qualquer site na coleção de sites. O exemplo a seguir ilustra a sintaxe: `http://mysharepointsite`.  
  
5.  Para **Autenticação**, selecione qual modo de autenticação usar para acessar o servidor Web. Você deve escolher o modo de autenticação que o servidor de relatório já está usando.  
  
    -   Se você estiver usando a segurança padrão, escolha **Autenticação do Windows**.  
  
    -   Se você tiver instalado e implantado uma extensão de segurança personalizada, escolha **Autenticação de Formulários**.  
  
    -   Se você tiver configurado o servidor de relatório para usar autenticação Básica, escolha **Autenticação Básica**.  
  
    -   Se o servidor de relatório for configurado para o modo integrado do SharePoint, escolha **Autenticação do Windows**.  
  
6.  Clique em **Testar** para verificar a conexão.  
  
7.  Quando solicitado, clique em **OK**e em **Salvar**.  
  
## <a name="connection-syntax-and-permissions"></a>Sintaxe de conexão e permissões  
 A tabela a seguir resume a sintaxe de conexão, operações e permissões exigidas para executar operações específicas.  
  
 Ao especificar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] como Tipo de Servidor na caixa de diálogo **Conectar-se ao Servidor** , você pode especificar um nome do servidor de relatório ou um ponto de extremidade para o serviço Web.  
  
|Conectar-se a|Tarefas|Permissões|  
|----------------|-----------|-----------------|  
|Servidor de relatório de modo nativo, conectado como o padrão ou instância nomeada:<br /><br /> \<nome do servidor >\<_instância ><br /><br /> A conexão com o servidor de relatório é feita pelo provedor WMI do servidor de relatório.|Exibir e definir propriedades e padrões do servidor.<br /><br /> Exibir e cancelar trabalhos.<br /><br /> Criar e gerenciar agendas compartilhadas.<br /><br /> Criar, modificar ou excluir definições de funções.|Atribuído à função Administrador do Sistema.|  
|O servidor de relatório em modo nativo conectado como instância padrão ou nomeada por meio do ponto de extremidade ao serviço Web Servidor de Relatórios:<br /><br /> `http://<servername>/reportserver`<br /><br /> Especificando uma URL para que o servidor de relatório forneça um caminho alternativo de conexão com o servidor de relatório.|Exibir e definir propriedades e padrões do servidor.<br /><br /> Exibir e cancelar trabalhos.<br /><br /> Criar e gerenciar agendas compartilhadas.<br /><br /> Criar, modificar ou excluir definições de funções.|Atribuído à função Administrador do Sistema.|  
|Servidor de relatório no modo integrado do SharePoint, conectado por meio do site do SharePoint:<br /><br /> `http://<webserver>/<SharePointSite>`|Exibir e definir propriedades e padrões do servidor.<br /><br /> Exibir e cancelar trabalhos.<br /><br /> Criar e gerenciar agendas compartilhadas definidas para o site com o qual você está conectado.<br /><br /> Exibir os níveis de permissão definidos para o site ao qual você está conectado.|Nível de permissão de controle total no site do SharePoint ao qual você está conectado.|  
|O servidor de relatório de modo integrado do SharePoint conectado pelo nome da instância do servidor de relatório:<br /><br /> \<nome do servidor >\<_instância >|Exibir e definir propriedades e padrões do servidor.<br /><br /> Exibir e cancelar trabalhos.|Nível de permissão de controle total no site do SharePoint integrado ao servidor de relatório.<br /><br /> Observe que, quando você se conecta ao servidor de relatório ao invés do site do SharePoint, o número de tarefas que pode executar é reduzido significativamente. Isso se deve ao fato de o servidor de relatório poder apenas retornar dados de aplicativo armazenados ou gerenciados no banco de dados do servidor de relatório e não na configuração do SharePoint e bancos de dados de conteúdo.|  
  
## <a name="see-also"></a>Consulte também  
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Reporting Services no SQL Server Management Studio &#40;SSRS&#41;](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
  
