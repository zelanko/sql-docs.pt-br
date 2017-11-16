---
title: "Configurar o IIS 7 para sincronização da Web | Microsoft Docs"
ms.custom: 
ms.date: 09/12/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IIS 7 server configuration [SQL Server replication]
- Web synchronization, IIS 7 servers
ms.assetid: c201fe2c-0a76-44e5-a233-05e14cd224a6
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: c0e55c0e35039490f0ce4cd8a7fb6d7e232c05aa
ms.openlocfilehash: ecc4752f5bf52931df9c7af62b5828b92f8f0123
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="configure-iis-7-for-web-synchronization"></a>Configurar o IIS 7 para sincronização da Web
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Os procedimentos deste tópico guiarão você pelo processo de configuração manual do Serviços de Informações da Internet (IIS) versão 7 e mais recentes da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para uso com sincronização da Web para replicação de mesclagem. 
  
 A configuração do IIS 7 ou mais recente é a primeira das três etapas necessárias para habilitar a sincronização da Web.  
  
 Para obter uma visão geral de todo o processo de configuração, consulte [Configurar Sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
> [!IMPORTANT]  
>  Certifique-se de que seu aplicativo use apenas versões [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] ou posteriores e que as versões anteriores do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] não estejam instaladas no servidor IIS. Versões anteriores do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] podem provocar erros, como: "Formato inválido de uma mensagem durante a sincronização da Web. Verifique se os componentes de replicação estão adequadamente configurados no servidor Web".  
  
 Para usar a sincronização da Web, é necessário configurar o IIS concluindo as etapas a seguir. Cada etapa é descrita em detalhes neste tópico.  
  
1.  Instale e configure o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener no computador que está executando o IIS.  
  
2.  Configure o protocolo SSL. O SSL é necessário para a comunicação entre o IIS e todos os assinantes.  
  
3.  Configure a autenticação IIS.  
  
4.  Configure uma conta e defina as permissões para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener Replicação.  
  
## <a name="installing-the-sql-server-replication-listener"></a>Instalando o SQL Server Replication Listener  

Há suporte para sincronização da Web no IIS, a partir da versão 5.0. O Assistente para Configurar Sincronização da Web do IIS versão 5 e 6 não está disponível com o IIS versão 7.0 e superior. **A partir do SQL Server 2012, para usar o componente de sincronização da Web no servidor IIS, você deve instalar o SQL Server com replicação. Essa pode ser a edição gratuita do SQL Server Express.**
  
#### <a name="to-install-and-configure-the-sql-server-replication-listener"></a>Para instalar e configurar o SQL Server Replication Listener  
  
1.  Instale a replicação do SQL Server no computador com IIS.

2. Crie um novo diretório de arquivos para replisapi.dll no computador que está executando o IIS. É possível criar o diretório onde desejar, mas é recomendável criá-lo no diretório \<*drive*>:\Inetpub. Por exemplo, crie o diretório \<*drive*>:\Inetpub\SQLReplication\\.  
  
3.  Copie replisapi.dll do diretório [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]com\ para o diretório de arquivos que você criou na etapa 1.  
  
4.  Registre replisapi.dll:  
  
    1.  Clique em **Iniciar**e em **Executar**. Na caixa **Abrir** , insira **cmd**e clique em **OK**.  
  
    2.  No diretório criado na etapa 1, execute o comando a seguir:  
  
         **regsvr32 replisapi.dll**  
  
5.  Crie um novo site para replicação ou use um site existente. Esse site será acessado pelos componentes de replicação durante a sincronização. Os procedimentos deste tópico pressupõem o Site Padrão. Para obter mais informações sobre como criar sites, consulte a documentação do IIS  
  
6.  Crie um diretório virtual em IIS. O diretório virtual deve ser criado no site criado na etapa 4 e deve ser mapeado para o diretório que foi criado na etapa 1. Seja o mais restritivo possível ao atribuir a esse diretório. Você deve selecionar pelo menos as permissões de **Leitura** e **Execução** .  
  
    1.  No **Gerenciador dos Serviços de Informações da Internet (IIS)**, no painel **Conexões** , clique com o botão direito em **Site Padrão**e selecione **Adicionar Diretório virtual**.  
  
    2.  Para **Alias**, insira **SQLReplication**.  
  
    3.  Para **Caminho físico**, insira **\<unidade>:\Inetpub\SQLReplication\\** e, em seguida, clique em **OK**.  
  
7.  Configure o IIS para habilitar a execução de replisapi.dll.  
  
    1.  No **Gerenciador dos Serviços de Informações da Internet (IIS)**, clique em **Site Padrão**.  
  
    2.  No painel central, clique em **Mapeamentos do Manipulador**.  
  
    3.  No painel **Ações** , clique em **Adicionar Mapeamento de Módulo**.  
  
    4.  Para Caminho de **Solicitação** , insira **replisapi.dll**.  
  
    5.  Na lista suspensa **Módulo** , selecione **IsapiModule**.  
  
    6.  Para **Executável**, insira **\<unidade>:\Inetpub\SQLReplication\replisapi.dll**.  
  
    7.  Para **Nome**, insira **Replisapi**.  
  
    8.  Clique no botão **Restrições da Solicitação** , clique na guia **Acesso** e clique em **Executar**.  
  
    9. Clique em **OK** para fechar a caixa de diálogo **Restrições da Solicitação** e clique em **OK** novamente para fechar a caixa de diálogo **Adicionar Mapeamento de Módulo** . Quando for solicitado a permitir a extensão de ISAPI, clique em **Sim** para adicionar a extensão.  
  
    10. Verifique se Replisapi.dll está listado sob os mapeamentos do manipulador **Habilitados** . Se ele estiver na lista **Desabilitados** , clique com o botão direito do mouse na entrada Replisapi e clique em **Editar Permissões de Recurso**. Marque a caixa de seleção **Executar** e clique em **OK**.  
  
## <a name="configuring-iis-authentication"></a>Configurando a Autenticação IIS  
 Quando os computadores assinantes se conectam ao IIS, o IIS deve autenticar os assinantes para que eles possam acessar recursos e processos. A autenticação pode ser aplicada para o site da Web inteiro ou para o diretório virtual que você criou.  
  
 É recomendável usar a Autenticação Básica com SSL. A SSL é necessária, independentemente do tipo de autenticação usado.  
  
 É recomendável usar a Autenticação Básica com SSL. A SSL é necessária, independentemente do tipo de autenticação usado.  
  
#### <a name="to-configure-iis-authentication"></a>Para configurar a Autenticação IIS  
  
1.  No **Gerenciador dos Serviços de Informações da Internet (IIS)**, clique em **Site Padrão**.  
  
2.  No painel do meio, clique duas vezes em **Autenticação**.  
  
3.  Clique com o botão direito do mouse em Autenticação Anônima e escolha Desabilitar.  
  
4.  Clique com o botão direito do mouse em Autenticação Básica e escolha Habilitar.  
  
## <a name="configuring-secure-sockets-layer"></a>Configurando o protocolo SSL  
 Para configurar o SSL, especifique um certificado a ser usado pelo computador que está executando o IIS. A sincronização da Web para replicação de mesclagem dá suporte ao uso de certificados de servidor, mas não de certificados de cliente. Para configurar o IIS para implantação, você deve obter primeiro um certificado de uma CA (autoridade de certificação). Para obter mais informações sobre certificados, consulte a documentação do IIS.  
  
 Depois de instalar o certificado, você deve associar o certificado ao site da Web que é usado pela sincronização da Web. Para desenvolvimento e testes, você pode especificar um certificado autoassinado. O IIS 7 pode criar um certificado para você e registrá-lo em seu computador.  
  
 A diferença entre a implantação para produção e os procedimentos fornecidos aqui é que, em produção e em testes de pré-produção, você usa um certificado emitido por uma CA em vez de um certificado autoassinado.  
  
> [!IMPORTANT]  
>  Um certificado autoassinado não é recomendável para uma instalação de produção. Certificados autoassinados não são seguros. Use certificados autoassinados apenas para desenvolvimento e testes.  
  
 Para configurar o SSL, você executará as etapas a seguir:  
  
1.  Configure o site para exigir o SSL e ignorar certificados de cliente.  
  
2.  Obtenha um certificado de uma CA ou crie um certificado autoassinado.  
  
3.  Associe o certificado ao site de replicação.  
  
#### <a name="to-require-ssl-security-for-a-web-site"></a>Para exigir segurança de SSL para um site  
  
1.  No **Gerenciador dos Serviços de Informações da Internet (IIS)**, expanda o nó do servidor local e clique no **Site Padrão** (ou no seu site de sincronização da Web se ele for diferente do site padrão).  
  
2.  No painel do meio, clique duas vezes em **Configurações de SSL**.  
  
3.  Marque a opção **Exigir SSL** . Em **Certificados de cliente**, verifique se o botão **Ignorar** está selecionado.  
  
#### <a name="to-create-a-self-signed-certificate-for-testing"></a>Para criar um certificado autoassinado para testes  
  
1.  Em **Gerenciador dos Serviços de Informações da Internet (IIS)**, clique no nó do servidor local e, em seguida, no painel central, clique duas vezes em **Certificados de Servidor**.  
  
2.  No painel **Ações** , clique em **Criar Certificado Autoassinado**.  
  
3.  Na caixa de diálogo **Criar Certificado Autoassinado** , digite um nome para o certificado e clique em **OK**.  
  
###### <a name="to-bind-a-certificate-to-a-web-site"></a>Para associar um certificado a um site  
  
1.  No painel **Conexões** , clique no **Site Padrão** (ou no seu site de sincronização da Web, se ele for diferente do site padrão).  
  
2.  No painel **Ações** , clique em **Associações**e, em seguida, em **Adicionar**. A caixa de diálogo **Adicionar Ligação do Site** será exibida.  
  
3.  Na lista suspensa **Tipo** , selecione **https**. Deixe as configurações padrão de **Endereço IP** e **Porta**.  
  
4.  Na lista suspensa **Certificado SSL** , selecione o certificado criado em "Para criar um certificado autoassinado para testes", clique em **OK**e, em seguida em **Fechar**.  
  
###### <a name="to-test-the-certificate"></a>Para testar o certificado  
  
1.  No **Noternet Noformation Services (IIS) Manager**, clique em **Site Padrão.**  
  
2.  No painel **Ações**, clique em **Procurar \*:443(https)**.  
  
3.  O Internet Explorer será aberto e exibirá uma mensagem informando que "Há um problema com o certificado de segurança deste site". Este aviso informa que o certificado associado não foi emitido por uma CA reconhecida e talvez não seja confiável. Esse é um aviso esperado, portanto, clique em **Continuar neste site (não recomendado)**.  
  
4.  Se for solicitado a **Conectar ao host local**, digite um nome de usuário e senha para continuar. Você deve ver a página padrão do site.  
  
## <a name="setting-permissions-for-the-sql-server-replication-listener"></a>Definindo permissões para o SQL Server Replication Listener  
 Quando um computador assinante se conecta ao computador que está executando o IIS, o assinante é autenticado usando o tipo de autenticação especificado quando o IIS foi configurado. Depois de autenticar o assinante, o IIS verifica se o assinante está autorizado a chamar a replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você controla os usuários que podem invocar a replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definindo as permissões para replisapi.dll. É necessário configurar corretamente as permissões para impedir acesso não autorizado à replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para configurar as permissões mínimas para a conta sob a qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener é executado, realize o procedimento a seguir. As etapas do procedimento a seguir se aplicam ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Server 2008 que está executando o IIS 7.0.  
  
 Além de realizar as etapas a seguir, certifique-se de que os logons necessários estão na lista de acesso à publicação (PAL). Para obter mais informações sobre a PAL, consulte [Secure the Publisher](../../relational-databases/replication/security/secure-the-publisher.md) (Proteger o publicador).  
  
 **Importante** a conta criada nesta seção é a conta que se conectará ao Publicador e ao Distribuidor durante a sincronização. Essa conta deve ser adicionada como uma conta de logon do SQL no servidor de distribuição e de publicação.  
  
 A conta usada para o SQL Server Replication Listener deve ter permissões conforme descrito no tópico Segurança do Agente de Mesclagem, na seção "Conectar-se ao Publicador ou ao Distribuidor".  
  
 Em resumo, a conta deve:  
  
-   Ser um membro da lista de acesso à publicação (PAL).  
  
-   Ser mapeada para um logon associado a um usuário no banco de dados de publicação.  
  
-   Ser mapeada para um logon associado a um usuário no banco de dados de distribuição.  
  
-   Ter permissões de Leitura no compartilhamento de instantâneos.  
  
#### <a name="to-configure-the-account-and-permissions"></a>Para configurar a conta e as permissões  
  
1.  Crie uma conta local no computador que está executando o IIS:  
  
    1.  Abra o **Server Manager**. No menu Iniciar, clique com o botão direito do mouse em **Computador**e clique em **Gerenciar**.  
  
    2.  No **Server Manager**, expanda **Configuração**e, em seguida, expanda **Usuários Locais e Grupos**.  
  
    3.  Clique com o botão direito do mouse em **Usuários**e depois clique em **Novo Usuário**.  
  
    4.  Digite um nome de usuário e uma senha forte. Limpe **O usuário deve alterar a senha no próximo logon**.  
  
    5.  Clique em **Criar**e depois em **Fechar**.  
  
2.  Adicione a conta ao grupo IIS_IUSRS:  
  
    1.  No **Server Manager**, expanda **Configuração**e, em seguida, expanda **Usuários Locais e Grupos**e clique em **Grupos**.  
  
    2.  Clique com o botão direito do mouse em **IIS_IUSRS**e, em seguida, clique em **Adicionar ao Grupo**.  
  
    3.  Na caixa de diálogo **Propriedades de IIS_IUSRS** , clique em **Adicionar**.  
  
    4.  Na caixa de diálogo **Selecionar Usuários, Computadores ou Grupos** , adicione a conta criada na etapa 1.  
  
    5.  Verifique se **Deste local** exibe o nome do computador local (não um domínio). Se esse campo não exibir o nome do computador local, clique em **Locais**. Na caixa de diálogo **Locais** , selecione o computador local e clique em **OK**.  
  
    6.  Nas caixas de diálogo **Selecionar Usuários** e **Propriedades de IIS_IUSRS** , clique em**OK**.  
  
3.  Conceda as permissões mínimas de conta na pasta que contém replisapi.dll:  
  
    1.  No Windows Explorer, clique com o botão direito do mouse na pasta que você criou para replisapi.dll e clique em **Propriedades**.  
  
    2.  Na guia **Segurança** , clique em **Editar**.  
  
    3.  Na caixa de diálogo **Permissões para \<foldername>**, clique em **Adicionar** para adicionar a conta criada na etapa 1.  
  
    4.  Verifique se **Deste local** exibe o nome do computador local (não um domínio). Se esse campo não exibir o nome do computador local, clique em **Locais**. Na caixa de diálogo **Locais** , selecione o computador local e clique em **OK**.  
  
    5.  Verifique se a conta tem permissão apenas para **Ler**, **Ler e Executar** e **Listar Conteúdo da Pasta**.  
  
    6.  Selecione qualquer usuário ou grupo que não requeira acesso ao diretório, clique em **Remover**e clique em **OK**.  
  
4.  Crie um pool de aplicativos no **Gerenciador dos Serviços de Informação de Internet (IIS)**:  
  
    1.  No **Gerenciador dos Serviços de Informações da Internet (IIS)**, no painel **Conexões** , expanda o nó do servidor local.  
  
    2.  Clique com o botão direito do mouse em **Pools de Aplicativos**e clique em **Adicionar Pool de Aplicativos**.  
  
    3.  Digite um nome para o pool de aplicativos, deixe os valores padrão para as pastas restantes e clique em **OK**.  
  
    > [!NOTE]  
    >  Se você prevê que terá mais de dois clientes de sincronização simultâneos, poderá criar um ambiente Web. Para obter mais informações, consulte “Criando um Ambiente Web” em [Configure a sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
5.  Associe a conta com o pool de aplicativos:  
  
    1.  No **Gerenciador dos Serviços de Informações da Internet (IIS)**, expanda o nó do servidor local e clique em **Pool de Aplicativos**.  
  
    2.  Clique com o botão direito do mouse no pool de aplicativos que você criou e clique em **Definir Padrões do Pool de Aplicativos**.  
  
    3.  Na caixa de diálogo **Padrões do Pool de Aplicativos** , role até a seção **Modelo de Processo** e clique no campo **Identidade** .  
  
    4.  Clique no botão de elipse à direita da linha **Identidade** .  
  
    5.  Clique no botão de opção **Conta Personalizada** e clique em **Definir**.  
  
    6.  Nos campos **Nome de usuário** e **Senha** , digite a conta e a senha que foram criadas na etapa 1 e clique em **OK**.  
  
    7.  Clique em **OK** para fechar a caixa de diálogo **Identidade do Pool de Aplicativos** e clique em **OK** novamente para fechar a caixa de diálogo **Padrões do Pool de Aplicativos**.  
  
6.  Associe o pool de aplicativos ao site de replicação:  
  
    1.  Em **Gerenciador dos Serviços de Informações da Internet (IIS)**, expanda o nó do servidor local e clique no **Site Padrão** (ou no seu site de sincronização da Web se ele for diferente do site padrão).  
  
    2.  No painel **Ações** , sob **Gerenciar Site**, clique em **Configurações Avançadas**.  
  
    3.  Na caixa de diálogo **Configurações Avançadas** , clique no botão de elipse à direita de **Pool de Aplicativos**.  
  
    4.  Na lista suspensa **Pool de aplicativos** , selecione o pool de aplicativos que você criou na etapa 4 e clique em **OK**.  
  
    5.  Clique em **OK** novamente para fechar as Configurações Avançadas.  
  
## <a name="testing-the-connection-to-replisapidll"></a>Testando a conexão com replisapi.dll  
 Execute a sincronização da Web em modo de diagnóstico para testar a conexão com o computador que está executando o IIS e certificar-se de que o certificado SSL está instalado adequadamente. Para executar a sincronização da Web em modo diagnóstico, você deve ser um administrador no computador que executa o IIS.  
  
#### <a name="to-test-the-connection-to-replisapidll"></a>Para testar a conexão com replisapi.dll  
  
1.  Certifique-se de que as configurações de rede local (LAN) no Assinante estão corretas:  
  
    1.  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer, no menu **Ferramentas** , clique em **Opções da Internet**.  
  
    2.  Na guia **Conexões** , clique em **Configurações da LAN**.  
  
    3.  Se um servidor proxy não for usado na LAN, desmarque **Detectar Automaticamente as Configurações** e **Usar um servidor proxy para a rede local**.  
  
    4.  Se um servidor proxy for usado, clique em **Usar um servidor proxy para a rede local** e **Ignorar servidor proxy para endereços locais**e clique em **OK**.  
  
2.  No Assinante, no Internet Explorer, conecte-se ao servidor em modo de diagnóstico adicionando `?diag` ao endereço para o replisapi.dll. Por exemplo: `https://server.domain.com/directory/replisapi.dll?diag`.  
  
    > [!NOTE]  
    >  No exemplo anterior, **server.domain.com** deve ser substituído pelo nome exato de **Emitido para** listado na seção **Certificados de Servidor** no Gerenciador do IIS.  
  
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
 [Sincronização da Web para replicação de mesclagem](../../relational-databases/replication/web-synchronization-for-merge-replication.md)   
 [Configurar a Sincronização da Web](../../relational-databases/replication/configure-web-synchronization.md)  
  
  

