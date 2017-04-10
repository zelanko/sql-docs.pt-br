---
title: "Recuperar dados de um modelo de minera&#231;&#227;o de dados (DMX) (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "recuperando dados do relatório"
  - "conjuntos de dados [Reporting Services], com consultas DMX"
  - "conjuntos de dados [Reporting Services], Analysis Services"
  - "consultas [Reporting Services], previsão de mineração de dados"
ms.assetid: d9cd3624-1594-4707-8887-55437dd7e07c
caps.latest.revision: 19
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 19
---
# Recuperar dados de um modelo de minera&#231;&#227;o de dados (DMX) (SSRS)
  Para usar os dados de um modelo de mineração de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em seu relatório, defina uma fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e um ou mais conjuntos de dados de relatório. Ao criar a definição da fonte de dados, é preciso especificar uma cadeia de conexão e as credenciais para que possa acessar a fonte de dados a partir de seu computador cliente.  
  
 É possível criar uma definição de fonte de dados inserida para ser usada em um único relatório ou uma definição de fonte de dados compartilhada que pode ser usada por vários relatórios. Os procedimentos contidos neste tópico descrevem como criar uma fonte de dados inserida. Para obter mais informações sobre fontes de dados compartilhadas, consulte [Conexões ou fontes de dados inseridas e compartilhadas &#40;Construtor de Relatórios e SSRS&#41;](../Topic/Embedded%20and%20Shared%20Data%20Connections%20or%20Data%20Sources%20\(Report%20Builder%20and%20SSRS\).md) e [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
 Depois de criar uma fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você poderá criar um ou mais conjuntos de dados. Para cada conjunto de dados, use um designer de consulta DMX (Data Mining Prediction Expression) para criar uma consulta DMX que especifica a coleção de campos. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas DMX do Analysis Services](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md).  
  
 Assim que você criar um conjunto de dados, o nome dele aparecerá no painel de dados do relatório como um nó abaixo da fonte de dados.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
### Para criar uma fonte de dados do Microsoft SQL Server Analysis Services  
  
1.  Na barra de ferramentas do painel Dados do Relatório, clique em **Nova** e em **Fonte de Dados**.  
  
2.  Na caixa de diálogo **Propriedades da Fonte de Dados**, digite um nome na caixa de texto **Nome** ou aceite o nome padrão.  
  
3.  Verifique se a opção **Conexão inserida** está selecionada.  
  
4.  Na lista suspensa **Tipo**, selecione **Microsoft SQL Server Analysis Services**.  
  
5.  Especifique uma cadeia de conexão que funcione com a sua fonte de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     Contate o administrador do banco de dados para obter informações sobre a conexão e as credenciais que devem ser usadas para se conectar à fonte de dados. O exemplo de cadeia de conexão a seguir especifica o banco de dados do [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] de amostra no cliente local.  
  
    ```  
    Data Source=localhost;Initial Catalog=AdventureWorksDW2012  
    ```  
  
6.  Clique em **Credenciais**.  
  
     Defina as credenciais que serão usadas na conexão com a fonte de dados. Para obter mais informações, consulte [Specify Credential and Connection Information for Report Data Sources](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
    > [!NOTE]  
    >  Para testar a conexão da fonte de dados, clique em **Editar**. Na caixa de diálogo **Propriedades de Conexão**, clique em **Testar Conexão**. Se o teste for bem-sucedido, você verá a mensagem informativa “Teste de conexão bem-sucedido”. Se o teste não for bem-sucedido, a mensagem de aviso informará o motivo pelo qual o teste não foi bem-sucedido.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     A fonte de dados será exibida no painel de dados do relatório.  
  
### Para criar um conjunto de dados no Microsoft SQL Server Analysis Services  
  
1.  No painel **Dados do Relatório**, clique com o botão direito do mouse no nome da fonte de dados que se conecta a uma fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e, em seguida, clique em **Adicionar Conjunto de Dados**.  
  
2.  Na caixa de diálogo **Propriedades do Conjunto de Dados**, digite um nome na caixa de texto **Nome**.  
  
3.  Na caixa **Fonte de dados**, verifique se o nome exibido é o nome da fonte de dados conectada a uma fonte de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
4.  Clique em **Designer de Consulta** para abrir o designer de consultas gráficas e criar uma consulta de maneira interativa. Se o designer de consulta abrir no modo MDX, clique em **Tipo de Comando DMX** (![Alterar para a exibição de linguagem de consulta DMX](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.png "Alterar para a exibição de linguagem de consulta DMX")) na barra de ferramentas para mudar para o designer de consulta de mineração de dados. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas DMX do Analysis Services](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md).  
  
     Opcionalmente, para importar uma consulta DMX existente de outro relatório, clique em **Importar** e navegue até o arquivo .rdl com a consulta DMX. Não há suporte para a importação de uma consulta a partir de um arquivo .dmx.  
  
5.  Depois de criar e executar sua consulta para ver os resultados do exemplo, clique em **OK**.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     O conjunto de dados e sua coleção de campos aparecerão no painel de dados do relatório abaixo do nó da fonte de dados.  
  
## Consulte também  
 [Tipo de conexão Analysis Services para DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  