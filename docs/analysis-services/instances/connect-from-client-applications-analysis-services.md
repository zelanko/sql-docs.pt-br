---
title: Conecte-se de aplicativos de cliente (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connection.login.analysisserver.f1
- sql13.swb.connecttoas.connectionproperties.f1
- sql13.swb.connecttoas.login.f1
ms.assetid: b1e0f1d4-0b87-4ad3-8172-f746fe2f16a2
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 20302da167c1ba1d19fb1b65ab871d81f7170591
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="connect-from-client-applications-analysis-services"></a>Conectar-se de aplicativos cliente (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Se você é novato no Analysis Services, use as informações deste tópico para se conectar a uma instância existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando ferramentas e aplicativos comuns. Este tópico também explica como se conectar em identidades de usuário diferentes para fins de teste.  
  
-   [Conectar usando o SQL Server Management Studio (SSMS)](#bkmk_SSMS)  
  
-   [Conectar usando o Excel](#bkmk_excel)  
  
-   [Conectar-se usando SQL Server Data Tools](#bkmk_SSDT)  
  
-   [Testar conexões](#bkmk_tshoot)  
  
 A documentação de referência da cadeia de conexão é fornecida separadamente. Para obter mais informações, consulte [Propriedades da cadeia de conexão &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md).  
  
 As conexões bem-sucedidas dependem de uma configuração de porta válida e permissões de usuário apropriadas. Clique nos links a seguir para aprender mais sobre cada requisito.  
  
-   [Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
  
-   [Autorizar acesso a objetos e operações &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
##  <a name="bkmk_SSMS"></a> Conectar usando o SQL Server Management Studio (SSMS)  
 Conecte-se ao Analysis Services no SSMS para gerenciar interativamente instâncias de servidor e bancos de dados. Você também pode executar consultas XMLA ou MDX para executar tarefas administrativas ou recuperar dados. Diferente de outras ferramentas e aplicativos que somente carregam bancos de dados quando uma consulta é enviada, o SSMS carrega todos os bancos de dados quando você se conecta ao servidor, supondo que você tem permissão para exibir o banco de dados. Isso significa que, se você tiver vários bancos de dados de tabela no servidor, todos serão carregados na memória do sistema quando você se conectar usando o SSMS.  
  
 Você pode testar permissões executando o SSMS em uma identidade de usuário específica e, em seguida, conectar-se ao Analysis Services como esse usuário.  
  
 Mantenha pressionada a tecla Shift e clique com o botão direito do mouse no atalho do **SQL Server Management Studio** para acessar a opção **Executar como um usuário diferente** .  
  
1.  Inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Na caixa de diálogo **Conectar ao Servidor** , selecione o tipo de servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  Na guia Logon, insira o nome do servidor digitando o nome do computador no qual o servidor está sendo executado. Você pode especificar o servidor usando seu nome de rede ou um nome de domínio totalmente qualificado.  
  
     Para uma instância nomeada, o nome do servidor deve ser especificada neste formato: nome do servidor\nome da instância. Um exemplo desta convenção de nomenclatura pode ser ADV-SRV062\Finance para um servidor que tem um nome de rede ADV-SRV062, onde o Analysis Services foi instalado como uma instância nomeada chamada Finance.  
  
     Para servidores implantados em um cluster de failover, conecte-se usando o nome de rede do cluster SSAS. Esse nome é especificado durante a instalação do SQL Server, por exemplo, **Nome de Rede do SQL Server**. Observe que, se você tiver instalado o SSAS como uma instância nomeada em um Windows Server Failover Cluster (WSFC), nunca adicione o nome da instância à conexão. Essa prática é exclusiva do SSAS; em contrapartida, uma instância nomeada de um mecanismo de banco de dados relacional clusterizado não inclui o nome da instância. Por exemplo, se você tiver instalado o SSAS e o mecanismo de banco de dados como uma instância nomeada (Contoso-Accounting) com um Nome de rede do SQL Server de SQL-CLU, deveria conectar ao SSAS usando "SQL-CLU" e ao mecanismo de banco de dados como "SQL-CLU\Contoso-Accounting". Consulte [Como criar clusters de SQL Server Analysis Services](http://go.microsoft.com/fwlink/p/?LinkId=396548) para obter mais informações e exemplos.  
  
     Para servidores implantados em um cluster de balanceamento de carga de rede, conecte-se usando o nome do servidor virtual do NLB.  
  
3.  A autenticação é sempre a autenticação do Windows e a identidade do usuário é sempre o usuário do Windows que está se conectando através do Management Studio.  
  
     Para que a conexão seja bem-sucedida, você deve ter permissão para acessar o servidor ou um banco de dados no servidor. A maioria das tarefas que você deseja executar no Management Studio requer permissões administrativas. Verifique se a conta à qual está se conectando é um membro da função de administrador de servidor. Para obter mais informações, consulte [Conceder direitos de administração de servidor a uma instância do Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
4.  Clique em **Propriedades da Conexão** para especificar um banco de dados específico, definir os valores de tempo limite ou as opções de criptografia. As informações de conexão opcionais incluem as propriedades de conexão usadas somente para a conexão atual.  
  
5.  Clique na guia **Parâmetros de Conexão Adicionais** para definir as propriedades de conexão não disponíveis na caixa de diálogo Conectar ao Servidor. Por exemplo, você pode digitar `Roles=Reader` na caixa de texto.  
  
     A conexão através de uma função com menos permissão permite que você teste comportamentos de banco de dados quando essa função estiver em vigor.  
  
    ```  
    Provider=MSOLAP; Data Source=SERVERNAME; Initial Catalog=AdventureWorks2012; Roles=READER  
    ```  
  
##  <a name="bkmk_excel"></a> Conectar usando o Excel  
 O Microsoft Excel é geralmente usado para analisar dados corporativos. Como parte de uma instalação do Excel, o Office instala o provedor OLE DB do Analysis Services (MSOLAP DLL), o ADOMD.NET e outros provedores de dados de modo que você possa usar os dados nos servidores de rede com mais rapidez. Se você estiver usando uma versão mais recente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] com uma versão mais antiga do Excel, você provavelmente precisará instalar provedores de dados mais novos em cada estação de trabalho que se conecta ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Consulte [Provedores de dados usados em conexões do Analysis Services](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md) para obter mais informações.  
  
 Quando você instala uma conexão para uma cubo ou banco de dados modelo tabular do Analysis Services, o Excel salva as informações de conexão em um arquivo .odc para uso futuro. A conexão é feita no contexto de segurança do usuário Windows atual. A conta de usuário deve ter permissões de leitura no banco de dados para que a conexão seja bem-sucedida.  
  
 Ao usar o dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma pasta de trabalho do Excel, as conexões são mantidas durante uma solicitação de consulta. Isso é porque você provavelmente verá muitas conexões para cada sessão, mantidas por períodos de tempo muito curtos, quando estiver monitorando uma carga de trabalho de consulta do Excel.  
  
 Você pode testar permissões iniciando o Excel em uma identidade de usuário específica.  
  
 Mantenha pressionada a tecla Shift e clique com o botão direito do mouse no atalho do **Excel** para acessar a opção **Executar como usuário diferente** .  
  
1.  Na guia Dados do Excel, clique em **De Outras Fontes**e clique em **Do Analysis Services**. Digite o nome do servidor e selecione um cubo ou uma perspectiva para consulta.  
  
     Para servidores implantados em um cluster com balanceamento de carga, use o nome do servidor virtual atribuído ao cluster.  
  
2.  Ao configurar uma conexão no Excel, na última página do Assistente de Conexão de Dados, você poderá especificar configurações de autenticação para Serviços do Excel. Estas configurações são usadas para definir propriedades na pasta de trabalho se você carregá-las em um servidor do SharePoint que tem Serviços do Excel. As configurações são usadas nas operações de atualização de dados. As opções incluem **Autenticação do Windows**, **Serviço de Repositório Seguro** (SSS) e **Nenhum**.  
  
     Evite usar **Nenhuma**. O Analysis Services não permite especificar nome de usuário e senha na cadeia de conexão a menos que você esteja se conectando em um servidor que foi configurado para acesso de HTTP. De maneira semelhante, não use SSS a menos que você já saiba que a ID SSS do aplicativo de destino esteja mapeada para um conjunto de credenciais de usuário do Windows que têm acesso de usuário aos bancos de dados do Analysis Services. Para a maioria dos cenários, usar a opção padrão de autenticação do Windows é a melhor escolha para uma conexão de Analysis Services do Excel.  
  
 Para obter mais informações, consulte [Conectar ou importar dados do SQL Server Analysis Services](http://go.microsoft.com/fwlink/?linkID=215150).  
  
##  <a name="bkmk_SSDT"></a> Conectar-se usando SQL Server Data Tools  
 O SQL Server Data Tools é usado para criar soluções de BI, incluindo modelos do Analysis Services, relatórios do Reporting Services e pacotes SSIS. Ao criar relatórios ou pacotes, talvez você precise especificar uma conexão ao Analysis Services.  
  
 Os links a seguir explicam como se conectar ao Analysis Services em um projeto do Servidor de Relatório ou do Integration Services:  
  
-   [Tipo de conexão Analysis Services para MDX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)  
  
-   [Gerenciador de conexões do Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
> [!NOTE]  
>  Ao usar o SQL Server Data Tools em um projeto existente do Analysis Services, lembre-se de que você pode se conectar offline usando um projeto local ou com controle de versão, ou conectar-se no modo online para atualizar os objetos do Analysis Services enquanto o banco de dados está em execução. Para obter mais informações, consulte [Connect in Online Mode to an Analysis Services Database](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md). Mais comumente, as conexões do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] estão no modo de projeto, no qual as alterações são implantadas no banco de dados somente quando você implanta o projeto explicitamente.  
  
##  <a name="bkmk_tshoot"></a> Testar conexões  
 Você pode usar o SQL Server Profiler para monitorar as conexões ao Analysis Services. Os eventos Logon de Auditoria e Logout de Auditoria fornecem evidências de uma conexão. A coluna de identidade indica o contexto de segurança em que a conexão é estabelecida.  
  
1.  Inicie o **SQL Server Profiler** na instância do Analysis Services e, em seguida, inicie um novo rastreamento.  
  
2.  Em Seleção de Eventos, verifique se **Audit Login** e **Audit Logout** foram verificados na seção Auditoria de Segurança.  
  
3.  Conecte-se ao Analysis Services por meio de um serviço de aplicativo (como o SharePoint ou o Reporting Services) em um computador cliente remoto. O evento Logon da Auditoria mostrará a identidade do usuário que está se conectando ao Analysis Services.  
  
 Os erros de conexão são geralmente rastreados para uma configuração de servidor incompleta ou inválida. Sempre verifique a configuração do servidor primeiro:  
  
-   Execute ping no servidor de um computador remoto para garantir que ele permite conexões remotas.  
  
-   **As regras de firewall no servidor permitem conexões de entrada em clientes do mesmo domínio**  
  
     Com a exceção do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, todas as conexões para um servidor remoto exigem que você tenha configurado o firewall para permitir acesso à porta à qual o Analysis Services está escutando. Se você estiver recebendo erros de conexão, verifique se a porta está acessível e se as permissões de usuário foram concedidas para os bancos de dados apropriados.  
  
     Para testar, use o Excel ou o SSMS em um computador remoto, especificando o endereço IP e a porta usados pela instância do Analysis Services. Se você conseguir estabelecer a conexão, as regras de firewall são válidas para a instância e esta permite conexões remotas.  
  
     Além disso, quando o TCP/IP for o protocolo de conexão, lembre-se de que o Analysis Services exige que as conexões de cliente se originem no mesmo domínio ou em um domínio confiável. Se as conexões ultrapassarem os limites de segurança, você provavelmente precisará configurar o acesso HTTP. Para obter mais informações, consulte [Configurar o acesso HTTP ao Analysis Services nos Serviços de Informações da Internet &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
-   Você pode se conectar usando algumas ferramentas mas não outras? A causa do problema pode ser a versão incorreta de uma biblioteca de cliente. Você pode obter bibliotecas de cliente na página de download do SQL Server Feature Pack.  
  
 Os recursos que podem ajudar você a resolver falhas de conexão são os seguintes:  
  
 [Resolvendo problemas comuns de conectividade nos cenários de conectividade do SQL Server 2005 Analysis Services](http://technet.microsoft.com/library/cc917670.aspx). Este documento não é recente, mas as informações e as metodologias ainda se aplicam.  
  
## <a name="see-also"></a>Consulte também  
 [Conectar ao Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)   
 [Metodologias de autenticação com suporte no Analysis Services](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)   
 [Representação &#40; SSAS de tabela &#41;](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   
 [Criar uma fonte de dados &#40; SSAS Multidimensional &#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
