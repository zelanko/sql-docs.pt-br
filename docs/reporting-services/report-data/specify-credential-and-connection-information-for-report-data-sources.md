---
title: "Especificar informações de credenciais e de conexão para fontes de dados de relatório | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- no credentials option [Reporting Services]
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- Windows authentication [Reporting Services]
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- unattended report processing [Reporting Services]
- reports [Reporting Services], security
- remote data sources [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- prompted credentials [Reporting Services]
- multiple connections
- stored credentials [Reporting Services]
- security [Reporting Services], data sources
- Windows integrated security [Reporting Services]
ms.assetid: fee1a663-a313-424a-aed2-5082bfd114b3
caps.latest.revision: "61"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.openlocfilehash: b16e0b6c380cfe47f2bc82ea0328d9386ada294c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="specify-credential-and-connection-information-for-report-data-sources"></a>Especificar informações de credenciais e de conexão para fontes de dados de relatório
  Um servidor de relatório usa credenciais para se conectar a fontes de dados externas que fornecem conteúdo a relatórios ou informações de destinatário para assinaturas controladas por dados. Você pode especificar credenciais que usam a Autenticação do Windows, autenticação de banco de dados, nenhuma autenticação ou autenticação personalizada. Ao enviar uma solicitação de conexão pela rede, o servidor de relatório representará uma conta de usuário ou uma conta de execução autônoma. Para obter mais informações sobre o contexto de segurança sob o qual uma conexão é feita, consulte [Configuração de fontes de dados e conexões de rede](#DataSourceConfigurationConnections) mais adiante neste tópico.  
  
> [!NOTE]  
>  As credenciais são também usadas para autenticar usuários com acesso ao servidor de relatório. As informações sobre como autenticar os usuários para um servidor de relatório são fornecidas em outro tópico.  
  
 A conexão com uma fonte de dados externa é definida quando você cria o relatório. Ela pode ser gerenciada separadamente depois que o relatório for publicado. Você pode especificar uma cadeia de caracteres de conexão estática ou uma expressão que permita aos usuários selecionar uma fonte de dados a partir de uma lista dinâmica. Para obter mais informações sobre como especificar um tipo de fonte de dados e uma cadeia de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
## <a name="when-credentials-are-used-in-report-builder"></a>Quando as credenciais são usadas no Construtor de Relatórios  
 No Construtor de Relatórios, as credenciais são usadas, em geral, quando você se conecta a um servidor de relatório ou a tarefas relacionadas a dados, tais como criar uma fonte de dados inserida, executar uma consulta de conjunto de dados ou visualizar um relatório. As credenciais não são armazenadas no relatório. Elas são gerenciadas separadamente no servidor de relatório ou no cliente local. A lista a seguir descreve os tipos de credenciais que talvez precisem ser fornecidos, o local em que são armazenados e como são usados:  
  
-   As credenciais do servidor de relatório inseridas na [Caixa de diálogo Logon do Reporting Services &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/reporting-services-login-dialog-box-report-builder.md).  
  
     Quando você salvar, publicar ou navegar em um servidor de relatório ou site do SharePoint pela primeira vez, talvez seja necessário inserir suas credenciais. As credenciais inseridas são usadas até a sessão do Construtor de Relatórios terminar. Se você optar por salvar as credenciais, elas serão armazenadas com segurança nas configurações de usuário de seu computador. Nas sessões subsequentes do Construtor de Relatórios, as credenciais salvas são usadas para se conectar ao mesmo servidor de relatório ou site do SharePoint. O administrador do servidor de relatório ou do SharePoint especifica o tipo de credencial a ser usado.  
  
-   As credenciais de fonte de dados inseridas na página [Caixa de diálogo Propriedades da Fonte de Dados, Credenciais &#40;Construtor de Relatórios&#41;](http://msdn.microsoft.com/library/4531f09f-d653-4c05-a120-d7788838bc99) de uma fonte de dados inserida.  
  
     Essas credenciais são usadas pelo servidor de relatório para fazer uma conexão de dados com a fonte de dados externa. Para alguns tipos de fontes de dados, as credenciais podem ser armazenadas com segurança no servidor de relatório. Essas credenciais permitem ao outros usuários executar o relatório sem fornecer credenciais para a conexão de dados subjacente.  
  
-   As credenciais de fonte de dados inseridas em [Caixa de diálogo Inserir Credenciais da Fonte de Dados &#40;Construtor de Relatórios&#41;](../../reporting-services/report-data/enter-data-source-credentials-dialog-box-report-builder.md) ao executar uma consulta de conjunto de dados, atualizar campos de conjuntos de dados ou visualizar o relatório.  
  
     Essas credenciais são usadas para fazer uma conexão de dados do Construtor de Relatórios com a fonte de dados ou visualizar um relatório configurado para solicitar credenciais. As credenciais que você insere nessa caixa de diálogo não são armazenadas no servidor de relatório e não estão disponível para uso de outros usuários. O Construtor de Relatórios armazena em cache as credenciais durante a sessão de edição de relatório de forma que você não precise inseri-las toda vez que executar a consulta ou visualizar o relatório.  
  
     Para fontes de dados compartilhadas, use a opção **Salvar minha senha** para salvar as credenciais localmente nas configurações de usuário de seu computador. O Construtor de Relatórios usa as credenciais salvas toda vez que uma conexão é feita com a fonte de dados externa correspondente.  
  
 Para obter mais informações, consulte [Caixa de diálogo Propriedades de Fonte de Dados, Geral &#40;Construtor de Relatórios&#41;](http://msdn.microsoft.com/library/b956f43a-8426-4679-acc1-00f405d5ff5b) e [Visualizando relatórios no Construtor de Relatórios](../../reporting-services/report-builder/previewing-reports-in-report-builder.md).  
  
## <a name="using-remote-data-sources"></a>Usando fontes de dados remotas  
 Se o relatório recuperar dados de um servidor de banco de dados remoto, verifique o seguinte:  
  
-   Se as credenciais fornecidas ao servidor de banco de dados são válidas. Se você estiver usando as credenciais de usuário do Windows, tenha certeza de que o usuário tem permissão para o servidor e banco de dados.  
  
-   Se as portas usadas pelo servidor de banco de dados estão abertas. Se você estiver acessando bancos de dados relacionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em computadores externos ou se o banco de dados do servidor de relatório estiver em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] externa , você deve abrir as portas 1433 e 1434 no computador externo. Certifique-se de reinicializar o servidor depois de abrir as portas. Para obter mais informações, veja [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
-   As conexões remotas devem ser habilitadas. Se você estiver acessando bancos de dados relacionais do SQL Server em computadores externos, poderá usar a ferramenta SQL Server Configuration Manager para verificar se as conexões remotas por TCP estão habilitadas.  
  
## <a name="ways-to-specify-credentials-for-connecting-to-remote-data-sources"></a>Maneiras de especificar credenciais para conexão com fontes de dados remotas  
 As fontes de dados que fornecem conteúdo para relatórios estão normalmente hospedadas em servidores remotos. Para recuperar dados de um relatório, um servidor de relatório deve se conectar ao servidor usando um conjunto de credenciais fornecido antecipadamente ou obtido no momento da execução. Ao configurar uma fonte de dados, você pode especificar credenciais das seguintes maneiras:  
  
-   Solicitar credenciais ao usuário.  
  
-   Armazenar credenciais.  
  
-   Usar a segurança integrada do Windows.  
  
-   Não use nenhuma credencial.  
  
 O ambiente de rede determina os tipos de conexões com suporte. Por exemplo, se o protocolo Kerberos versão 5 for habilitado, você poderá usar os recursos de delegação e representação disponíveis na Autenticação do Windows para oferecer suporte a conexões ao longo de vários servidores. Se sua rede não oferecer suporte a esses recursos de segurança, você precisará contornar as restrições de conexão. Se a delegação e a representação não estiverem habilitadas, as credenciais do Windows poderão ser passadas por uma conexão de computador antes que ela expire. Uma conexão de usuário de um computador cliente para um servidor de relatório conta como a primeira conexão. Se o usuário abrir um relatório que recupere dados de um servidor remoto, esse logon contará como a segunda conexão e falhará se você tiver especificado que a conexão deve usar a segurança integrada quando a delegação não estiver habilitada.  
  
 Se forem necessárias várias conexões para concluir uma viagem de ida e volta do computador cliente para uma fonte de dados de relatório externa, escolha uma das seguintes estratégias para efetuar a conexão com sucesso.  
  
-   Habilite os recursos de representação e delegação em seu domínio de modo que as credenciais possam ser delegadas a outros computadores sem limite.  
  
-   Use credenciais armazenadas ou credenciais de prompt para consultar fontes de dados externas para dados do relatório. As credenciais podem ser uma conta de domínio do Windows ou um logon de banco de dados.  
  
### <a name="prompted-credentials"></a>Credenciais solicitadas  
 Ao configurar uma conexão de fonte de dados de relatório para usar credenciais de prompt, cada usuário que acessa o relatório deve digitar um nome de usuário e senha para recuperar os dados. Essa abordagem é recomendada para relatórios que contêm dados confidenciais. As credenciais de prompt só podem ser usadas em relatórios executados sob demanda. As credenciais de prompt podem ser uma conta do Windows ou logon de banco de dados. Para usar a Autenticação do Windows, você deve selecionar **Usar as credenciais do Windows ao conectar-se à fonte de dados**. Caso contrário, o servidor de relatório passa credenciais ao servidor de banco de dados para autenticação do usuário. Se o servidor de banco de dados não puder autenticar as credenciais fornecidas, a conexão falhará.  
  
### <a name="windows-integrated-security"></a>Segurança integrada do Windows  
 Ao usar a opção **Segurança Integrada do Windows** , o servidor de relatório passa o token de segurança do usuário acessando o relatório ao servidor que hospeda a fonte de dados externa. Nesse caso, não é solicitado que o usuário digite um nome de usuário ou senha. Essa abordagem é recomendada se os recursos de personificação e delegação estiverem habilitados. Se esses recursos não estiverem habilitados, você deve usar essa aproximação apenas se todos os servidores que você deseja acessar estiverem localizados no mesmo computador.  
  
### <a name="stored-credentials"></a>Credenciais armazenadas  
 Você pode armazenar as credenciais usadas para acessar uma fonte de dados externa. As credenciais são armazenadas em criptografia reversível no banco de dados do servidor de relatório. Você pode especificar um conjunto de credenciais armazenadas para cada fonte de dados usada em um relatório. As credenciais fornecidas recuperam os mesmos dados para todo usuário que executa o relatório.  
  
 As credenciais armazenadas são recomendadas como parte de uma estratégia para acessar servidores de banco de dados remotos. As credenciais armazenadas são necessárias se você quiser oferecer suporte a assinaturas ou programar a criação de histórico de relatórios ou atualizar instantâneos de relatório. Quando um relatório é executado como um processo em segundo plano, o servidor de relatório é o agente que executa o relatório. Como não há contexto de usuário, o servidor de relatório deve obter informações de credencial do banco de dados do servidor de relatório para conectar-se à fonte de dados.  
  
 O nome de usuário e senha que você especifica podem ser credenciais do Windows ou um logon de banco de dados. Se você especificar as credenciais do Windows, o servidor de relatório passará as credenciais ao Windows para autenticação subsequente. Caso contrário, as credenciais são passadas ao servidor de banco de dados para autenticação.  
  
#### <a name="how-to-grant-allow-log-on-locally-permissions-to-domain-user-accounts"></a>Como conceder permissões "Permitir logon localmente" a contas de usuário de domínio  
 Se você usar credenciais armazenadas para conectar-se a uma fonte de dados externa, a conta de usuário de domínio do Windows deve ter permissão para efetuar logon localmente. Isso permite que o servidor de relatório represente o usuário no servidor de relatório e envie a solicitação à fonte de dados externa como o usuário representado.  
  
 Para conceder essa permissão, faça o seguinte:  
  
1.  No computador do servidor de relatório, em **Ferramentas Administrativas**, abra **Política de Segurança Local**.  
  
2.  Sob **Configurações de Segurança**, expanda **Políticas Locais**e clique em **Atribuição de Direitos de Usuário**.  
  
3.  No painel de detalhes, clique com o botão direito do mouse em **Permitir logon localmente** e clique com o botão direito do mouse em **Propriedades**.  
  
4.  Clique em **Adicionar Usuário ou Grupo**.  
  
5.  Clique em **Locais**, especifique um domínio ou outro local que você deseja pesquisar e clique em **OK**.  
  
6.  Digite a conta do Windows para a qual você quer permitir o logon interativo e, então, clique em **OK**.  
  
7.  Na caixa de diálogo **Propriedades de permitir logon localmente** , clique em **OK**.  
  
8.  Verifique se a conta que você selecionou não tem também permissões negadas:  
  
    1.  Clique com o botão direito em **Negar logon localmente** e clique com o botão direito do mouse em **Propriedades**.  
  
    2.  Se a conta estiver listada, selecione-a e clique em **Remover**.  
  
#### <a name="using-impersonation-with-stored-credentials"></a>Usando a representação em credenciais armazenadas  
 Você também pode usar credenciais para representar a identidade de outro usuário. Para bancos de dados do SQL Server, usar os conjuntos de opções de representação define a função [SETUSER](../../t-sql/statements/setuser-transact-sql.md) .  
  
> [!IMPORTANT]  
>  Não use a representação para relatórios com suporte a assinaturas ou que usam agendas para gerar o histórico de relatório ou atualizar um instantâneo de relatório.  
  
### <a name="no-credentials"></a>Nenhuma credencial  
 Você pode configurar uma conexão de fonte de dados para não usar credenciais. A Microsoft recomenda que você sempre use credenciais para acessar fontes de dados; não usar credenciais não é aconselhado. Porém, você pode escolher executar um relatório sem credenciais nos seguintes casos:  
  
-   A fonte de dados remota não requer credenciais.  
  
-   As credenciais são passadas na cadeia de caracteres de conexão (recomendado somente para conexões seguras).  
  
-   O relatório é um sub-relatório que usa as credenciais do relatório pai.  
  
 Sob essas condições, o servidor de relatório se conecta a uma fonte de dados remota usando a execução autônoma que você deve definir antecipadamente. Como o servidor de relatório não se conecta a um servidor remoto usando suas credenciais de serviço, você deve especificar uma conta que o servidor de relatório possa usar para fazer a conexão. Para obter mais informações sobre como criar essa conta, consulte [Configurar a conta de execução autônoma &#40;Gerenciador de Configuração do SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## <a name="user-name-and-password-login"></a>Logon de nome de usuário e senha  
 Quando você seleciona **Usar este nome de usuário e senha**, um nome de usuário e senha devem ser fornecidos para acessar a fonte de dados. Para um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , as credenciais talvez sejam de um logon de banco de dados. As credenciais são passadas para a fonte de dados para autenticação.  
  
##  <a name="DataSourceConfigurationConnections"></a> Configuração de fontes de dados e conexões de rede  
 A tabela a seguir mostra como são feitas conexões para combinações específicas de tipos de credencial e extensões de processamento de dados. Se você estiver usando uma extensão de processamento de dados personalizada, consulte [Especificar conexões para extensões de processamento de dados personalizados](../../reporting-services/report-data/specify-connections-for-custom-data-processing-extensions.md).  
  
|**Tipo**|**Contexto para conexão de rede**|**Tipos de fonte de dados**<br /><br /> **(SQL Server, Oracle, ODBC, OLE DB, Analysis Services, XML, SAP NetWeaver BI, Hyperion Essbase)**|  
|--------------|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|  
|Segurança integrada|Representar o usuário atual|Para todos os tipos de fonte de dados, conecte-se usando a conta do usuário atual.|  
|Credenciais do Windows|Representar o usuário especificado|Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC e OLE DB: conecte usando a conta do usuário representado.|  
|Credenciais de banco de dados|Representar a conta de execução autônoma ou conta de serviço<br /><br /> (o Reporting Services remove as permissões de administrador ao enviar a solicitação de conexão que usa a identidade do serviço).|Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC e OLE DB:<br /><br /> Acrescente o nome de usuário e senha à cadeia de caracteres de conexão.<br /><br /> Para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:<br /><br /> A conexão será bem-sucedida se você estiver usando o protocolo TCP/IP, caso contrário ela falhará.<br /><br /> Para XML:<br /><br /> Falha na conexão com o servidor de relatório se forem usadas as credenciais do banco de dados.|  
|Nenhum.|Representar a conta de execução autônoma.|Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC e OLE DB:<br /><br /> Use as credenciais definidas na cadeia de caracteres de conexão. A conexão com o servidor de relatório falhará se a conta de execução autônoma estiver indefinida.<br /><br /> Para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:<br /><br /> A conexão sempre falhará se nenhuma credencial for especificada, mesmo se a conta de execução autônoma for definida.<br /><br /> Para XML:<br /><br /> Conecte-se como Usuário Anônimo se a conta de execução autônoma estiver definida; caso contrário, a conexão falhará.|  
  
## <a name="setting-credentials-programmatically"></a>Definindo credenciais programaticamente  
 Você pode definir credenciais em seu código para controlar o acesso a relatórios e ao servidor de relatório. Para obter mais informações, consulte [Fontes de Dados e Métodos de Conexão](../../reporting-services/report-server-web-service/methods/data-sources-and-connection-methods.md).  
  
## <a name="see-also"></a>Consulte também  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Gerenciar fontes de dados de relatório](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Configurar propriedades de fonte de dados para um relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  
