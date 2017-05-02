---
title: Exibir arquivos de log offline | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Log File Viewer, viewing offline logs
- offline log files
ms.assetid: 9223e474-f224-4907-a4f2-081e11db58f5
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 339787b7252b5604a08770d417fe39d5b63aca70
ms.lasthandoff: 04/11/2017

---
# <a name="view-offline-log-files"></a>Exibir arquivos de log offline
  A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], você pode exibir arquivos de log [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma instância local ou remota de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando a instância de destino for offline ou não inicia.  
  
 Você pode acessar os arquivos de log offline de Servidores Registrados, ou programaticamente por WMI e o WQL (Linguagem WQL) consulta.  
  
> [!NOTE]  
>  Você também pode usar estes métodos para conectar-se a uma instância que está online, mas que, por algum motivo, você não consegue se conectar por meio de uma conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="before-you-begin"></a>Antes de começar  
 Para conectar-se a arquivos de log offline, uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser instalada no computador que você está usando para exibir os arquivos de log offline, e no computador onde estão localizados os arquivos de log que você deseja exibir. Se uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver instalada em ambos os computadores, você poderá exibir arquivos offline para instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e para instâncias que estão executando versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em qualquer computador.  
  
 Se você estiver usando os Servidores Registrados, a instância com a qual você deseja se conectar deverá estar registrada em **Grupos de Servidores Locais** ou **Servidores de Gerenciamento Central**. (A instância pode ser registrada por si própria ou ser membro de um grupo de servidores.) Para obter mais informações sobre como adicionar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aos Servidores Registrados, consulte os seguintes tópicos:  
  
-   [Criar ou editar um grupo de servidores &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [Registrar um servidor conectado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/register-a-connected-server-sql-server-management-studio.md)  
  
-   [Criar um servidor de gerenciamento central e um grupo de servidores &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md)  
  
 Para obter mais informações sobre como exibir os arquivos de log offline programaticamente através de consultas WMI e WQL, consulte os seguintes tópicos:  
  
-   [SqlErrorLogEvent Class](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogevent-class.md) (Este tópico mostra como recuperar valores para eventos registrados em um arquivo de log especificado.)  
  
-   [SqlErrorLogFile Class](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md) (Este tópico mostra como recuperar informações sobre todos os arquivos de log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].)  
  
##  <a name="BeforeYouBegin"></a> Permissões  
 Para conectar-se a um arquivo de log offline, você deve ter as permissões a seguir nos computadores local e remoto:  
  
-   Acesso de leitura ao namespace WMI **Root\Microsoft\SqlServer\ComputerManagement12** . Por padrão, todos usuários têm acesso de leitura por meio da permissão Habilitar Conta. Para obter mais informações, consulte o procedimento "Para verificar permissões de WMI" posteriormente nesta seção.  
  
-   Permissão de leitura para a pasta que contém os arquivos de logs de erros. Por padrão, os arquivos de logs de erros estão localizados no caminho a seguir (em que \<*Drive>* representa a unidade na qual você instalou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e \<*InstanceName*> é o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]):  
  
     **\<Drive>:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.\<InstanceName>\MSSQL\Log**  
  
 Para verificar as configurações de segurança do namespace WMI, você pode usar o snap-in Controle WMI.  
  
#### <a name="to-verify-wmi-permissions"></a>Para verificar permissões do WMI  
  
1.  Abra o snap-in Controle WMI. Para fazer isto, execute um destes procedimentos, dependendo do sistema operacional:  
  
    -   Clique em **Iniciar**, digite **wmimgmt.msc** na caixa **Iniciar Pesquisa** e pressione ENTER.  
  
    -   Clique em **Iniciar**, clique em **Executar**, digite **wmimgmt.msc**e pressione ENTER.  
  
2.  Por padrão, o snap-in Controle WMI gerencia o computador local.  
  
     Se você desejar conectar-se a um computador remoto, siga estas etapas:  
  
    1.  Clique com o botão direito do mouse em **Controle WMI (Local)**e clique em **Conectar-se a outro computador**.  
  
    2.  Na caixa de diálogo **Alterar computador gerenciado** , clique em **Outro computador**.  
  
    3.  Insira o novo nome do computador remoto e clique em **OK**.  
  
3.  Clique com o botão direito do mouse em **Controle WMI (Local)** ou **Controle WMI (***RemoteComputerName***)**e clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades do Controle WMI** , clique na guia **Segurança** .  
  
5.  Na árvore de namespace, localize e clique no seguinte namespace:  
  
     **Root\Microsoft\SqlServer\ComputerManagement10**  
  
6.  Clique em **Segurança**.  
  
7.  Verifique se a conta que será usada tem a permissão para **Habilitar Conta** . Esta permissão permite acesso de leitura a objetos WMI.  
  
### <a name="view-log-files"></a>Exibir Arquivos de Log  
 O procedimento a seguir mostra como exibir arquivos de log offline através de Servidores Registrados. O procedimento presume o seguinte:  
  
 A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o qual você deseja se conectar já está registrada em Servidores Registrados.  
  
##### <a name="to-view-log-files-for-instances-that-are-offline"></a>Para exibir arquivos de log para instâncias que estão offline  
  
1.  Se você desejar exibir arquivos de log offline em uma instância local, tenha certeza de iniciar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] com permissões elevadas. Para fazer isto, quando você iniciar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], clique com o botão direito do mouse em **SQL Server Management Studio**e clique em **Executar como administrador**.  
  
2.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no menu **Exibir** , clique em **Servidores Registrados**.  
  
3.  Na árvore de console, localize a instância na qual você deseja exibir os arquivos offline.  
  
4.  Siga um destes procedimentos:  
  
    -   Se a instância estiver em **Grupos de servidores Locais**, expanda **Grupos de servidores Locais**, expanda o grupo de servidores (se a instância for um membro de um grupo), clique com o botão direito do mouse na instância e clique em **Exibir o Log do SQL Server**.  
  
    -   Se a instância for o próprio Servidor de Gerenciamento Central, expanda **Servidores de Gerenciamento Central**, clique com o botão direito do mouse na instância, aponte para **Ações de Servidor de Gerenciamento Central**e clique em **Exibir Log do SQL Server**.  
  
    -   Se a instância estiver em **Servidores de Gerenciamento Central**, expanda **Servidores de Gerenciamento Central**, expanda o Servidor de Gerenciamento Central, clique com o botão direito do mouse na instância (ou expanda um grupo de servidores e clique com o botão direito do mouse na instância) e clique em **Exibir Log do SQL Server**.  
  
5.  Se você estiver se conectando a uma instância local, a conexão será feita usando as credenciais de usuário atuais.  
  
     Se você estiver se conectando a uma instância remota, na caixa de diálogo **Visualizador do Arquivo de Log – Conectar Como** , execute um destes procedimentos:  
  
    -   Para se conectar como o usuário atual, verifique se a caixa de seleção **Conectar-se como outro usuário** está desmarcada e clique em **OK**.  
  
    -   Para se conectar como outro usuário, marque a caixa de seleção **Conectar-se como outro usuário** e clique em **Definir Usuário**. Quando for solicitado, insira as credenciais de usuário (com o nome de usuário no formato *domain_name*\\*user_name*), clique em **OK**e em **OK** novamente para se conectar.  
  
    > [!NOTE]  
    >  Se os arquivos de log levarem muito tempo para carregar, você poderá clicar em **Parar** na barra de ferramentas do Visualizador do Arquivo de Log.  
  
## <a name="see-also"></a>Consulte também  
 [Visualizador do Arquivo de Log](../../relational-databases/logs/log-file-viewer.md)  
  
  
