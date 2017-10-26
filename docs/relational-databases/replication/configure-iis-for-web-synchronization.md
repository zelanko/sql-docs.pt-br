---
title: "Configurar IIS para sincronização da Web | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IIS server configuration [SQL Server replication]
- websync.log
- Web synchronization, IIS servers
ms.assetid: d651186e-c9ca-4864-a444-2cd6943b8e35
caps.latest.revision: 88
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: c0e55c0e35039490f0ce4cd8a7fb6d7e232c05aa
ms.openlocfilehash: 9555085ef832e4277da89e062aa28872b5eeb4fe
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="configure-iis-for-web-synchronization"></a>Configurar IIS para sincronização da Web
  Os procedimentos neste tópico compõem a segunda etapa para configurar a sincronização da Web para replicação de mesclagem. Esta etapa é executada depois que você habilita uma publicação para sincronização da Web. Para obter uma visão geral do processo de configuração, consulte [Configurar Sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md). Depois de concluir os procedimentos neste tópico, continue na terceira etapa, configurando uma assinatura para usar a sincronização da Web. A terceira etapa é descrita nos seguintes tópicos:  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Como configurar uma assinatura para usar a sincronização da Web \(SQL Server Management Studio\)](http://msdn.microsoft.com/library/ms345214.aspx)  
  
-   Programação [!INCLUDE[tsql](../../includes/tsql-md.md)] de replicação: [Como configurar uma Assinatura para usar a sincronização da Web (Programação Transact-SQL de replicação)](http://msdn.microsoft.com/library/ms345206.aspx)  
  
-   RMO: [Como configurar uma assinatura para usar sincronização da Web (programação RMO)](http://msdn.microsoft.com/library/ms345207.aspx)  
  
 A sincronização da Web usa um computador que esteja executando o IIS (Serviços de Informações da Internet) da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para sincronizar assinaturas pull para publicações de mesclagem. Existe suporte para as versões 5.0 e 6.0 do IIS e para o [!INCLUDE[iisver](../../includes/iisver-md.md)] . O Assistente para Configurar Sincronização da Web não tem suporte no [!INCLUDE[iisver](../../includes/iisver-md.md)].  
  
> [!IMPORTANT]  
>  Certifique-se de que seu aplicativo use apenas versões [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] ou posteriores e que as versões anteriores do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] não estejam instaladas no servidor IIS. Versões anteriores do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] podem causar erros. Esses erros incluem o seguinte: "Formato inválido de uma mensagem durante a sincronização da Web. Verifique se os componentes de replicação estão adequadamente configurados no servidor Web".  
  
> [!CAUTION]  
>  Não use WebSync e locais de pasta de instantâneo alternativos ao mesmo tempo.  
  
 Para usar a sincronização da Web, é necessário configurar o IIS concluindo as etapas a seguir. Cada etapa é descrita em detalhes neste tópico.  
  
1.  Configure o protocolo SSL. O SSL é necessário para a comunicação entre o IIS e todos os Assinantes.  
  
2.  Instale os componentes de conectividade do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador que está executando o IIS usando o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instale os componentes de conectividade doation Wizard. Se você planeja usar o Assistente para Configurar Sincronização da Web, mencionado na etapa 3, será preciso instalar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no computador que está executando o IIS.  
  
3.  Configure o computador que está executando o IIS para sincronização da Web. Você pode configurar o computador manualmente ou pode usar o Assistente para Configurar Sincronização da Web. Recomendamos o uso do assistente.  
  
    > [!NOTE]  
    >  Se o computador que está executando o IIS tiver uma versão de 64 bits do Windows, será necessário executar o comando a seguir para verificar se o servidor está configurado adequadamente para executar os aplicativos ISAPI (Internet Server API). Para obter mais informações, consulte a documentação do IIS.  
  
    ```  
    cscript %SystemDrive%\inetpub\AdminScripts\adsutil.vbs set w3svc/AppPools/Enable32bitAppOnWin64 1  
    ```  
  
4.  Defina as permissões apropriadas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener.  
  
5.  Execute a sincronização da Web em modo de diagnóstico para testar a conexão com o computador que está executando o IIS e verificar se o certificado SSL está instalado adequadamente.  
  
## <a name="configuring-secure-sockets-layer"></a>Configurando o protocolo SSL  
 Para configurar o protocolo SSL, especifique um certificado a ser usado pelo computador que está executando o IIS. A sincronização da Web para replicação de mesclagem oferece suporte ao uso de certificados de servidor, mas não de certificados de cliente. Para configurar o IIS para implantação, você deve obter primeiro um certificado de uma CA (autoridade de certificação). Uma autoridade de certificação é uma entidade responsável por estabelecer e atestar a autenticidade das chaves de criptografia públicas que pertencem a usuários, computadores ou outras autoridades de certificação. Para obter mais informações sobre certificados, consulte a documentação do IIS. Depois de instalar o certificado, você deve associar o certificado ao site da Web que é usado pela sincronização da Web.  
  
#### <a name="to-specify-a-certificate-for-deployment"></a>Para especificar um certificado para implantação  
  
1.  Faça logon no computador que está executando IIS como um administrador.  
  
2.  Inicie o **Gerenciador dos Serviços de Informações da Internet (IIS)**:  
  
    1.  Clique em **Iniciar**e em **Executar**.  
  
    2.  Na caixa **Abrir** , digite **inetmgr**e clique em **OK**.  
  
3.  Execute o Assistente de Certificado IIS:  
  
    1.  No **Gerenciador dos Serviços de Informações da Internet (IIS)**, expanda o nó **computador local** e depois expanda a pasta **Sites da Web** .  
  
    2.  Clique com o botão direito em **Site Padrão da Web**e depois clique em **Propriedades**.  
  
    3.  Na caixa de diálogo **Propriedades do Site Padrão da Web** , na guia **Segurança de Diretório** , clique em **Certificado do Servidor**.  
  
    4.  Conclua o Assistente de Certificado de Servidor Web.  
  
4.  Clique em **OK**.  
  
 Se não puder obter um certificado de servidor de uma CA, você poderá especificar um certificado a ser testado. Para configurar o IIS 6.0 para teste, instale um certificado usando o utilitário SelfSSL. Este utilitário está disponível no IIS 6.0 Resource Kit. Você pode baixar as ferramentas no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkId=30958). Para o IIS 5.0, vá para [Ajuda e Suporte da Microsoft](http://go.microsoft.com/fwlink/?LinkId=46229).  
  
> [!NOTE]  
>  Um certificado deve ser associado a um site da Web antes que esse site possa usar o SSL. O SelfSSL associa o certificado automaticamente com o site da Web padrão. Se já tiver um certificado ou se instalar depois um certificado de uma CA, você deve associar explicitamente esse certificado ao site da Web que é usado para a sincronização da Web. Certifique-se de haver somente um certificado associado ao site da Web utilizado para sincronizar as assinaturas. Se houver vários certificados, o Assinante usará o primeiro site da Web disponível.  
  
#### <a name="to-specify-a-certificate-for-testing-in-iis-60"></a>Para especificar um certificado para teste no IIS 6.0  
  
1.  Faça logon no computador que está executando IIS como um administrador.  
  
2.  Baixar e instalar o SelfSSL. Por padrão, o aplicativo é instalado em \<*unidade*>:\Arquivos de Programas\IIS Resources\SelfSSL. Os atalhos de aplicativos e de documentação são copiados em \<*unidade*>:\Documents and Settings\All Users \Menu Iniciar\Programas\IIS Resources\SelfSSL.  
  
3.  Execute o SelfSSL:  
  
    -   Para executar o SelfSSL com valores padrão para todos os parâmetros, localize o diretório de instalação para o aplicativo e clique duas vezes no SelfSSL.exe.  
  
        > [!NOTE]  
        >  Por padrão, o certificado instalado pelo SelfSSL é válido durante sete dias.  
  
    -   Para especificar valores para um ou mais parâmetros: clique em **Iniciar**e clique em **Executar**. Na caixa **Abrir** , insira **cmd**e clique em **OK**. Localize o diretório de instalação do SelfSSL, digite `SelfSSL`e depois especifique valores para um ou mais parâmetros. Para obter uma lista de parâmetros, digite `SelfSSL -?`.  
  
## <a name="installing-connectivity-components-and-sql-server-management-studio"></a>Instalando os componentes de conectividade e o SQL Server Management Studio  
  
#### <a name="to-install-sql-server-connectivity-components-and-sql-server-management-studio"></a>Para instalar os componentes de conectividade SQL Server e o SQL Server Management Studio  
  
1.  Faça logon como administrador no computador executando IIS.  
  
2.  No disco de instalação do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , inicie o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre como usar esse assistente, consulte [Instalar o SQL Server 2016 por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
3.  Na página **Seleção de Recursos** , selecione **Conectividade das Ferramentas de Cliente**.  
  
4.  Se você estiver planejando usar o Assistente para Configurar Sincronização da Web, selecione **Ferramentas de Gerenciamento - Básico**.  
  
5.  Conclua o assistente e depois reinicie o computador.  
  
    > [!NOTE]  
    >  Você pode instalar componentes adicionais, mas só os componentes de conectividade são necessários para a sincronização da Web.  
  
## <a name="configuring-the-computer-that-is-running-iis-by-using-the-configure-web-synchronization-wizard"></a>Configurando o computador que está executando IIS usando o Assistente para Configuração da Sincronização da Web  
 Configure o servidor IIS usando o Assistente para Configuração da Sincronização da Web ou manualmente. Recomendamos o uso do assistente, mas nós também fornecemos etapas para configuração manual na próxima seção. O Assistente para Sincronização da Web que está disponível com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] pode ser usado apenas para publicações criadas em um Publicador que estiver executando o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou em um Publicador que foi atualizado para o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. O assistente não pode ser usado para publicações no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. O assistente pode ser usado com assinaturas no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e em versões posteriores, e no [!INCLUDE[ssEWnoversion](../../includes/ssewnoversion-md.md)] 3.0 e em versões posteriores.  
  
 A configuração tem as seguintes características:  
  
-   Usa o site padrão em IIS. Porém, você pode usar outro site da Web. Para obter mais informações sobre como criar sites da Web, consulte a documentação de IIS.  
  
    > [!NOTE]  
    >  O site da Web que você especificar fornece acesso aos componentes que são usados pela sincronização da Web. O site da Web não fornece acesso a outros dados ou páginas da Web, a menos que você o configure para fazer isso.  
  
-   Cria um diretório virtual e seu alias associado. O alias é usado ao acessar os componentes de sincronização da Web. Por exemplo, se o endereço de IIS for `https://server.domain.com` e você especificar um alias de 'websync1', o endereço de acesso ao componente replisapi.dll será `https://server.domain.com/websync1/replisapi.dll`.  
  
-   Usa a Autenticação Básica. Recomendamos o uso da Autenticação Básica porque ela torna possível executar o IIS e o Publicador/Distribuidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em computadores separados (configuração recomendada) sem exigir delegação Kerberos. Usar o SSL com Autenticação Básica assegura que logons, senhas e todos os dados sejam criptografados em trânsito. (SSL é necessário, independentemente do tipo de autenticação usado.) Para obter mais informações sobre as práticas recomendadas para sincronização da Web, consulte a seção "Práticas recomendadas de segurança para a sincronização da Web" em [Configure a sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
#### <a name="to-configure-the-computer-that-is-running-iis-by-using-the-configure-web-synchronization-wizard"></a>Para configurar o computador que está executando IIS usando o Assistente para Configuração da Sincronização da Web  
  
1.  No computador que está executando o IIS, inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Conecte-se ao Publicador e depois expanda o nó do servidor.  
  
3.  Expanda a pasta **Publicações Locais** , clique com o botão direito do mouse na publicação e depois clique em **Configurar Sincronização da Web**.  
  
4.  No Assistente para Configuração da Sincronização da Web, na página **Tipo de Assinante** , selecione o **SQL Server**.  
  
5.  Na página **Servidor Web** :  
  
    1.  Selecione a instância de IIS que sincronizará as assinaturas.  
  
    2.  Selecione **Criar um novo diretório virtual**.  
  
    3.  No painel inferior da página, expanda a instância de IIS, expanda **Sites da Web**e clique em **Site Padrão**.  
  
6.  Na página **Informações do Diretório Virtual** :  
  
    1.  Na caixa **Alias** , digite um alias para o diretório virtual.  
  
    2.  Na caixa **Caminho** , digite um caminho para o diretório virtual. Por exemplo, se você digitou **websync1** na caixa **Alias** , digite **C:\Inetpub\wwwroot\websync1** na caixa **Caminho** . Clique em **Avançar**.  
  
    3.  Nas duas caixas de diálogo, clique em **Sim**. Isso especifica que você deseja criar uma nova pasta e deseja copiar o Internet Server API (ISAPI) DLL do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . .  
  
7.  Na página **Acesso Autenticado** :  
  
    1.  Certifique-se de que os servidores de domínio **Autenticação Integrada do Windows** e **Autenticação digest para servidores de domínio Windows** estejam desmarcados.  
  
    2.  Selecione **Autenticação Básica**.  
  
    3.  Nas caixas **Domínio Padrão** e **Realm** , digite o domínio do computador que está executando IIS.  
  
8.  Na página **Acesso ao Diretório** :  
  
    1.  Clique na caixa de diálogo **Adicionar**e depois em **Selecionar Usuários ou Grupos** , adicione as contas pelas quais os Assinantes farão conexões ao IIS. These are the accounts that you will specify on the **Web Server Information** page of the New Subscription Wizard or as the value for the [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)*@internet_login* parameter.  
  
9. Na página **Acesso ao Compartilhamento de Instantâneos** , digite o compartilhamento de instantâneo. As permissões apropriadas são definidas nesse compartilhamento de forma que os Assinantes possam acessar os arquivos de instantâneos. Para obter mais informações sobre permissões para compartilhamento, consulte [Proteger uma pasta de instantâneo](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
10. Na página **Concluindo o Assistente** , clique em **Concluir**.  
  
     Se ocorrer uma falha, como um erro de rede ao tentar configurar um computador remoto que esteja executando o IIS, todas as ações concluídas são revertidas e todas as ações restantes são canceladas. Se não for possível reverter uma ação concluída, o status na página final do assistente será **Êxito** e as ações concluídas permanecerão confirmadas.  
  
11. Se o computador que está executando o IIS estiver executando uma versão de 64 bits do Windows, replisapi.dll deverá ser copiado para o diretório adequado:  
  
    1.  Clique em **Iniciar**e em **Executar**. Na caixa **Abrir** , insira **iisreset**e clique em **OK**.  
  
    2.  Depois de interromper e reiniciar o IIS, copie replisapi.dll de [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]COM\replisapi para o diretório especificado na etapa 6b.  
  
    3.  Clique em **Iniciar**e em **Executar**. Na caixa **Abrir** , insira **cmd**e clique em **OK**.  
  
    4.  No diretório que você especificou na etapa 6b, execute o seguinte comando:  
  
         **regsvr32 replisapi.dll**  
  
## <a name="manually-configuring-the-computer-that-is-running-iis"></a>Configurando manualmente o computador que está executando o IIS  
 Para configurar manualmente o computador que está executando o IIS, você deve instalar e configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener e depois configurar a autorização para os Assinantes que irão se conectar ao IIS.  
  
#### <a name="to-install-and-configure-the-sql-server-replication-listener"></a>Para instalar e configurar o SQL Server Replication Listener  
  
1.  Crie um diretório de arquivos no computador que está executando o IIS para conter replisapi.dll. É possível criar o diretório onde desejar, mas é recomendável criá-lo no diretório \<*drive*>:\Inetpub. Por exemplo, crie o diretório \<*drive*>:\Inetpub\SQLReplication\\.  
  
    > [!IMPORTANT]  
    >  É altamente recomendável criar esse diretório em uma partição de sistema de arquivos NTFS e não em um sistema de arquivos FAT. Ao usar o sistema de arquivos NTFS file, você pode usar as permissões do sistema de arquivos NTFS para controlar com precisão os usuários que podem acessar a replicação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Copie replisapi.dll do diretório [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]com\ para o diretório de arquivos que você criou na etapa 1.  
  
3.  Registre replisapi.dll:  
  
    1.  Clique em **Iniciar**e em **Executar**. Na caixa **Abrir** , insira **cmd**e clique em **OK**.  
  
    2.  No diretório que você criou na etapa 1, execute o seguinte comando:  
  
         **regsvr32 replisapi.dll**  
  
4.  Crie um novo site da Web para replicação ou use um site existente. O site da Web será acessado pelos componentes de replicação durante a sincronização. Para obter mais informações sobre como criar sites da Web, consulte a documentação de IIS.  
  
5.  Crie um diretório virtual em IIS. O diretório virtual deve ser criado no site da Web que foi criado na etapa 4 e deve ser mapeado para o diretório que foi criado na etapa 1. Para obter mais informações sobre como criar diretórios virtuais, consulte a documentação de IIS. Recomendamos que você seja tão restritivo quanto possível ao conceder permissões a esse diretório. Você deve selecionar as permissões **Leitura** e **Executar** , mas pode desmarcar as permissões **Executar scripts**, **Gravação**e **Procurar** .  
  
6.  Configure o IIS para habilitar a execução de replisapi.dll. As permissões concedidas na etapa 4 são suficientes para as versões anteriores do IIS; porém o IIS versão 6.0 exige que as extensões Internet Server API (ISAPI) sejam habilitadas. Para obter mais informações, consulte "Configurando extensões ISAPI" e "Habilitando e desabilitando conteúdo dinâmico" na documentação do IIS 6.0.  
  
#### <a name="to-configure-iis-authentication"></a>Para configurar a autenticação de IIS  
  
-   Quando os Assinantes se conectarem ao IIS, o IIS deve autenticar os Assinantes antes que eles possam acessar recursos e processos. IIS oferece três tipos de autenticação: Anônima, Básica e Integrada. A autenticação pode ser aplicada para o site da Web inteiro ou para o diretório virtual que você criou.  
  
     É recomendável usar a Autenticação Básica com SSL. A SSL é necessária, independentemente do tipo de autenticação usado. Para obter mais informações sobre como configurar a autenticação, consulte a documentação de IIS.  
  
## <a name="setting-permissions-for-the-sql-server-replication-listener"></a>Definindo permissões para o SQL Server Replication Listener  
 Quando um Assinante se conecta ao computador que está executando o IIS, o Assinante é autenticado usando o tipo de autenticação que foi especificado quando você configurou o IIS. Depois de autenticar o Assinante, o IIS verifica se o Assinante está autorizado a invocar a replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você controla os usuários que podem invocar a replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definindo as permissões para replisapi.dll. É necessário configurar corretamente as permissões para impedir acesso não autorizado à replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para configurar as permissões mínimas para a conta sob a qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener é executado, realize o procedimento a seguir. As etapas no procedimento se aplicam ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] executando o IIS 6.0.  
  
 Além de realizar as etapas a seguir, certifique-se de que os logons necessários estão na lista de acesso à publicação (PAL). Para obter mais informações sobre a PAL, consulte [Secure the Publisher](../../relational-databases/replication/security/secure-the-publisher.md) (Proteger o publicador).  
  
#### <a name="to-configure-the-account-and-permissions"></a>Para configurar a conta e as permissões  
  
1.  Crie uma conta local no computador que está executando o IIS:  
  
    1.  Clique com o botão direito do mouse em **Meu Computador**e, em seguida, clique em **Gerenciar**.  
  
    2.  Em **Gerenciamento do Computador**, expanda **Usuários e Grupos Locais**.  
  
    3.  Clique com o botão direito do mouse em **Usuários**e depois clique em **Novo Usuário**.  
  
    4.  Digite um nome de usuário e uma senha forte.  
  
    5.  Clique em **Criar**e depois em **Fechar**.  
  
2.  Adicione a conta ao grupo IIS_WPG:  
  
    1.  Em **Gerenciamento do Computador**, expanda **Usuários e Grupos Locais**e clique em **Grupos**.  
  
    2.  Clique com o botão direito do mouse em **IIS_WPG**e depois clique em **Adicionar ao Grupo**.  
  
    3.  Na caixa de diálogo **Propriedades de IIS_WPG** , clique em **Adicionar**.  
  
    4.  Na caixa de diálogo **Selecionar Usuários, Computadores ou Grupos** , adicione a conta criada na etapa 1.  
  
    5.  Certifique-se de que o nome no campo **Deste local** é o nome do computador local em vez de um domínio. Se o nome não for de um computador local, clique em **Locais**. Na caixa de diálogo **Locais** , escolha o computador local e clique em **OK**.  
  
    6.  Nas caixas de diálogo **Selecionar usuários** e **Propriedades de IIS_WPG** , clique em **OK**.  
  
3.  Conceda as permissões mínimas para a conta na pasta que contém replisapi.dll:  
  
    1.  Localize a pasta que você criou para replisapi.dll, clique com o botão direito do mouse na pasta e depois clique em **Compartilhamento e Segurança**.  
  
    2.  Na guia **Segurança** , clique em **Adicionar**.  
  
    3.  Na caixa de diálogo **Selecionar Usuários, Computadores ou Grupos** , adicione a conta criada na etapa 1.  
  
    4.  Certifique-se de que o nome no campo **Deste local** é o nome do computador local em vez de um domínio. Se o nome não for de um computador local, clique em **Locais**. Na caixa de diálogo **Locais** , selecione o computador local e clique em **OK**.  
  
    5.  Certifique-se de que a conta tem permissão apenas para **Ler**, **Ler e Executar** e **Listar Conteúdo da Pasta**.  
  
    6.  Selecione qualquer usuário ou grupo que não requeira acesso ao diretório e clique em **Remover**.  
  
    7.  Clique em **OK**.  
  
4.  Crie um pool de aplicativos no **Gerenciador dos Serviços de Informação de Internet (IIS)**:  
  
    1.  Clique em **Iniciar**e em **Executar**.  
  
    2.  Na caixa **Abrir** , digite **inetmgr**e clique em **OK**.  
  
    3.  No **Gerenciador dos Serviços de Informação de Internet (IIS)**, expanda o nó do **computador local** .  
  
    4.  Clique com o botão direito do mouse em **Pools de Aplicativos**, aponte para **Novo** e clique em **Pool de Aplicativos**.  
  
    5.  Digite um nome para o pool no campo **Identificação do pool de aplicativos** e clique em **OK**.  
  
5.  Associe a conta com o pool de aplicativos:  
  
    1.  No **Gerenciador dos Serviços de Informação de Internet (IIS)**, expanda o nó do **computador local** e depois expanda **Pools de Aplicativos**.  
  
    2.  Clique com o botão direito do mouse no pool de aplicativos que você criou e depois clique em **Propriedades**.  
  
    3.  Na caixa de diálogo **Propriedades de \<ApplicationPoolName>**, na guia **Identidade**, clique em **Configurável**.  
  
    4.  Nos campos **Nome de usuário** e **senha** , digite a conta e senha que foram criadas na etapa 1.  
  
    5.  Clique em **OK**.  
  
6.  Associe o pool de aplicativos com o diretório virtual que é usado para a sincronização da Web:  
  
    1.  No **Gerenciador dos Serviços de Informação de Internet (IIS)**, expanda o nó do **computador local** e depois expanda **Sites da Web**.  
  
    2.  Expanda o site da Web que você está usando para a sincronização da Web, clique com o botão direito do mouse no diretório virtual que você criou para a sincronização da Web e depois clique em **Propriedades**.  
  
    3.  Na guia **Diretório Virtual** da caixa de diálogo **Propriedades de \<VirtualDirectoryName>**, na lista suspensa **Pool de aplicativos**, selecione o pool de aplicativos criado na etapa 5.  
  
    4.  Clique em **OK**.  
  
## <a name="testing-the-connection-to-replisapidll"></a>Testando a conexão com replisapi.dll  
 Execute a sincronização da Web em modo de diagnóstico para testar a conexão com o computador que está executando o IIS e certificar-se de que o certificado SSL (Secure Sockets Layer) está instalado adequadamente. Para executar a sincronização da Web em modo diagnóstico, você deve ser um administrador no computador que executa o IIS.  
  
#### <a name="to-test-the-connection-to-replisapidll"></a>Para testar a conexão com replisapi.dll  
  
1.  Certifique-se de que as configurações de rede local (LAN) no Assinante estão corretas:  
  
    1.  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer, no menu **Ferramentas** , clique em **Opções da Internet**.  
  
    2.  Na guia **Conexões** , clique em **Configurações da LAN**.  
  
    3.  Se um servidor proxy não for usado na LAN, desmarque **Detectar Automaticamente as Configurações** e **Usar um servidor proxy para a rede local**.  
  
    4.  Se um servidor proxy for usado, selecione **Usar um servidor proxy para a rede local** e **Ignorar servidor proxy para endereços locais**.  
  
    5.  Clique em **OK**.  
  
2.  No Assinante, no Internet Explorer, conecte-se ao servidor em modo de diagnóstico adicionando `?diag` ao endereço para o replisapi.dll. Por exemplo: `https://server.domain.com/directory/replisapi.dll?diag`.  
  
3.  Se o certificado especificado para o IIS não for reconhecido pelo sistema operacional Windows, a caixa de diálogo **Alerta da Segurança** será exibida. Esse alerta pode ocorrer porque o certificado é um certificado de teste ou porque o certificado foi emitido por uma autoridade de certificação (CA) que não é reconhecida pelo Windows.  
  
    > [!NOTE]  
    >  Se essa caixa de diálogo não aparecer, certifique-se de que o certificado para o servidor que você está acessando foi adicionado ao repositório de certificados no Assinante como um certificado confiável. Para obter mais informações sobre exportação de certificados, consulte a documentação do IIS.  
  
    1.  Na caixa de diálogo **Alerta de Segurança** , clique em **Exibir Certificado**.  
  
    2.  Na caixa de diálogo **Certificado** , na guia **Geral** , clique em **Instalar Certificado**.  
  
    3.  Conclua o Assistente para Importação de Certificados, aceitando os padrões.  
  
    4.  Na caixa de diálogo **Aviso de Segurança** , clique em **Sim**.  
  
    5.  Na caixa de diálogo de confirmação do Assistente para Importação de Certificados, clique em **OK**.  
  
    6.  Feche a caixa de diálogo **Certificado** .  
  
    7.  Na caixa de diálogo **Alerta de Segurança** , clique em **Sim**.  
  
    > [!NOTE]  
    >  Os certificados serão instalados para os usuários. Esse processo deve ser executado para cada usuário que sincronizará com o IIS.  
  
4.  Na caixa de diálogo **Conectar a \<ServerName>**, especifique o logon e a senha que o Agente de Mesclagem usará para se conectar ao IIS. Essas credenciais também serão especificadas no Assistente para Nova Assinatura.  
  
5.  Na janela do Internet Explorer chamada **Informação diagnóstica do SQL Websync**, verifique se o valor em cada coluna **Status** na página é **ÊXITO**.  
  
6.  Certifique-se de que o certificado está instalado corretamente no Assinante:  
  
    1.  Feche e depois reabra o Internet Explorer.  
  
    2.  Conecte ao servidor em modo diagnóstico. Se o certificado estiver instalado corretamente, a caixa de diálogo **Alerta de Segurança** não aparecerá. Se a caixa de diálogo aparecer, o Merge Agent apresentará falha quando tentar se conectar ao computador que está executando o IIS. Você deve certificar-se de que o certificado para o servidor que você está acessando foi adicionado ao repositório de certificados no Assinante como um certificado confiável. Para obter mais informações sobre exportação de certificados, consulte a documentação do IIS.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar Sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md)  
  
  

