---
title: Especificar informações de credenciais e de conexão para fontes de dados de relatório | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
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
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ce1866d4ffde34052a05ec6fbcbcd2c0dacaea42
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082236"
---
# <a name="specify-credential-and-connection-information-for-report-data-sources"></a>Especificar informações de credenciais e de conexão para fontes de dados de relatório
  Um servidor de relatório usa credenciais para se conectar a fontes de dados externas que fornecem conteúdo a relatórios ou informações de destinatário para assinaturas controladas por dados. Você pode especificar credenciais que usam a Autenticação do Windows, autenticação de banco de dados, nenhuma autenticação ou autenticação personalizada. Ao enviar uma solicitação de conexão pela rede, o servidor de relatório representará uma conta de usuário ou uma conta de execução autônoma. Para obter mais informações sobre o contexto de segurança sob o qual uma conexão é feita, consulte [Configuração de fontes de dados e conexões de rede](#DataSourceConfigurationConnections) mais adiante neste tópico.  
  
> [!NOTE]  
>  As credenciais são também usadas para autenticar usuários com acesso ao servidor de relatório. As informações sobre como autenticar os usuários para um servidor de relatório são fornecidas em outro tópico.  
  
 A conexão com uma fonte de dados externa é definida quando você cria o relatório. Ela pode ser gerenciada separadamente depois que o relatório for publicado. Você pode especificar uma cadeia de caracteres de conexão estática ou uma expressão que permita aos usuários selecionar uma fonte de dados a partir de uma lista dinâmica. Para obter mais informações sobre como especificar uma cadeia de conexão e de tipo de fonte dados, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
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
 Você também pode usar credenciais para representar a identidade de outro usuário. Para bancos de dados do SQL Server, usar a opções de representação define a [SETUSER](/sql/t-sql/statements/setuser-transact-sql) função.  
  
> [!IMPORTANT]  
>  Não use a representação para relatórios com suporte a assinaturas ou que usam agendas para gerar o histórico de relatório ou atualizar um instantâneo de relatório.  
  
### <a name="no-credentials"></a>Nenhuma credencial  
 Você pode configurar uma conexão de fonte de dados para não usar credenciais. A Microsoft recomenda que você sempre use credenciais para acessar fontes de dados; não usar credenciais não é aconselhado. Porém, você pode escolher executar um relatório sem credenciais nos seguintes casos:  
  
-   A fonte de dados remota não requer credenciais.  
  
-   As credenciais são passadas na cadeia de caracteres de conexão (recomendado somente para conexões seguras).  
  
-   O relatório é um sub-relatório que usa as credenciais do relatório pai.  
  
 Sob essas condições, o servidor de relatório se conecta a uma fonte de dados remota usando a execução autônoma que você deve definir antecipadamente. Como o servidor de relatório não se conecta a um servidor remoto usando suas credenciais de serviço, você deve especificar uma conta que o servidor de relatório possa usar para fazer a conexão. Para obter mais informações sobre como criar essa conta, consulte [Configurar a conta de execução autônoma &#40;Gerenciador de Configuração do SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
##  <a name="DataSourceConfigurationConnections"></a> Configuração de fontes de dados e conexões de rede  
 A tabela a seguir mostra como são feitas conexões para combinações específicas de tipos de credencial e extensões de processamento de dados. Se você estiver usando uma extensão de processamento de dados personalizada, consulte [Especificar conexões para extensões de processamento de dados personalizados](specify-connections-for-custom-data-processing-extensions.md).  
  
|**Tipo**|**Contexto para conexão de rede**|**Tipos de fonte de dados**<br /><br /> **(SQL Server, Oracle, ODBC, OLE DB, Analysis Services, XML, SAP NetWeaver BI, Hyperion Essbase)**|  
|--------------|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|  
|Segurança integrada|Representar o usuário atual|Para todos os tipos de fonte de dados, conecte-se usando a conta do usuário atual.|  
|Credenciais do Windows|Representar o usuário especificado|Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC e OLE DB: conecte usando a conta do usuário representado.|  
|Credenciais de banco de dados|Representar a conta de execução autônoma ou conta de serviço<br /><br /> (o Reporting Services remove as permissões de administrador ao enviar a solicitação de conexão que usa a identidade do serviço).|Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC e OLE DB:<br /><br /> Acrescente o nome de usuário e senha à cadeia de caracteres de conexão.<br /><br /> Para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]:<br /><br /> A conexão será bem-sucedida se você estiver usando o protocolo TCP/IP, caso contrário ela falhará.<br /><br /> Para XML:<br /><br /> Falha na conexão com o servidor de relatório se forem usadas as credenciais do banco de dados.|  
|None|Representar a conta de execução autônoma.|Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC e OLE DB:<br /><br /> Use as credenciais definidas na cadeia de caracteres de conexão. A conexão com o servidor de relatório falhará se a conta de execução autônoma estiver indefinida.<br /><br /> Para [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]:<br /><br /> A conexão sempre falhará se nenhuma credencial for especificada, mesmo se a conta de execução autônoma for definida.<br /><br /> Para XML:<br /><br /> Conecte-se como Usuário Anônimo se a conta de execução autônoma estiver definida; caso contrário, a conexão falhará.|  
  
## <a name="setting-credentials-programmatically"></a>Definindo credenciais programaticamente  
 Você pode definir credenciais em seu código para controlar o acesso a relatórios e ao servidor de relatório. Para obter mais informações, consulte [fontes de dados e métodos de Conexão](../report-server-web-service/methods/data-sources-and-connection-methods.md).  
  
## <a name="see-also"></a>Consulte também  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Gerenciar fontes de dados de relatório](../../integration-services/connection-manager/data-sources.md)   
 [O Gerenciador de relatórios &#40;modo nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de relatórios&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Configurar propriedades de fonte de dados para um relatório &#40;Gerenciador de relatórios&#41;](configure-data-source-properties-for-a-report-report-manager.md)  
  
  
