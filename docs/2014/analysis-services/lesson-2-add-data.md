---
title: 'Lição 2: Adicionar dados | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 13c3a8cc-b1db-4aba-ad9b-038b7971be8d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 696b4e9402e58da6308e6746cadbc25d43396d8f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729312"
---
# <a name="lesson-2-add-data"></a>Lição 2: Adicionar dados
  Nesta lição, você usará o Assistente de Importação de Tabela do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] para se conectar ao banco de dados SQL AdventureWorksDW, selecionar, visualizar e filtrar os dados, e importá-los para o workspace do modelo.  
  
 Usando o Assistente de importação de tabela, você pode importar dados de uma variedade de fontes relacionais: Access, SQL, Oracle, Sybase, Informix, DB2, Teradata e muito mais. As etapas de importação de dados de cada uma dessas fontes relacionais são bem parecidas com as descritas a seguir. Além disso, os dados podem ser selecionados por meio de um procedimento armazenado.  
  
 Para saber mais sobre como importar dados e os diferentes tipos de fontes de dados das quais você pode importar dados, consulte [Fontes de dados &#40;SSAS Tabular&#41;](data-sources-ssas-tabular.md).  
  
 Tempo estimado para concluir esta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 1: Criar um novo projeto de modelo de tabela](lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Criar uma conexão  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2012-database"></a>Para criar uma conexão com um banco de dados AdventureWorksDW2012.  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Importar de Fonte de Dados**.  
  
     Esse procedimento iniciará o Assistente de Importação de Tabela que o orientará no processo de configuração de uma conexão a uma fonte de dados. Se a opção **Importar da Fonte de Dados** estiver acinzentada, clique duas vezes em **Model.bim** no **Gerenciador de Soluções** para abrir o modelo no designer.  
  
2.  No **Assistente de Importação de Tabela**, em **Bancos de Dados Relacionais**, clique em **Microsoft SQL Server**e clique em **Avançar**.  
  
3.  No **conectar-se a um banco de dados do Microsoft SQL Server** página, na **nome de Conexão amigável**, tipo `Adventure Works DB from SQL`.  
  
4.  Na caixa **Nome do servidor**, digite o nome do servidor no qual você instalou o banco de dados AdventureWorksDW.  
  
5.  No campo **Nome do banco de dados** , clique na seta para baixo e selecione **AdventureWorksDW**e clique em **Avançar**.  
  
6.  Na página **Informações sobre Representação** , é necessário especificar as credenciais que o Analysis Services usará para se conectar à fonte de dados ao importar e processar dados. Verifique se a opção **Nome de usuário e senha específicos do Windows** está selecionada e, em **Nome de Usuário** e **Senha**, insira suas credenciais de logon do Windows e clique em **Avançar**.  
  
    > [!NOTE]  
    >  O uso de uma conta de usuário e senha do Windows é o método mais seguro de conexão a uma fonte de dados. Para obter mais informações, consulte [Representação &#40;SSAS de Tabela&#41;](tabular-models/impersonation-ssas-tabular.md).  
  
7.  Na página **Escolher como Importar os Dados** , verifique se a opção **Selecionar itens em uma lista de tabelas e exibições para escolher os dados a serem importados** está marcada. Para selecionar em uma lista de tabelas e exibições, clique em **Avançar** para exibir uma lista de todas as tabelas de origem do banco de dados de origem.  
  
8.  No **selecionar tabelas e exibições** , marque a caixa de seleção para as tabelas a seguir: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**,  **DimProductSubcategory**, e **FactInternetSales**.  
  
9. Desejamos atribuir às tabelas do modelo nomes mais explicativos. Clique na célula da coluna **Nome Amigável** de **DimCustomer**. Renomear a tabela removendo "Dim" de DimCustomer.  
  
10. Renomeie as outras tabelas:  
  
    |Nome de origem|Nome amigável|  
    |-----------------|-------------------|  
    |DimDate|data|  
    |DimGeography|Geografia|  
    |DimProduct|Produto|  
    |DimProductCategory|Product Category|  
    |DimProductSubcategory|Product Subcategory|  
    |FactInternetSales|Internet Sales|  
  
     **NÃO** clique em **Concluir**.  
  
 Agora que você se conectou ao banco de dados, selecionou as tabelas a serem importadas e atribuiu nomes amigáveis às tabelas, vá para a próxima seção, [Filtrar os dados da tabela antes de importar](#FilterData).  
  
##  <a name="FilterData"></a> Filtrar os dados da tabela  
 A tabela DimCustomer que você está importando do banco de dados contém um subconjunto dos dados contidos no banco de dados Adventure Works original do SQL Server. Você filtrará algumas das colunas da tabela DimCustomer que não são necessárias. Quando possível, você desejará filtrar dados que não serão usados para economizar espaço na memória usado pelo modelo.  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>Para filtrar os dados da tabela antes de importar  
  
1.  Selecione a linha da tabela **Customer** e clique em **Visualizar e Filtrar**. A janela **Visualizar Tabela Selecionada** é aberta com todas as colunas da tabela DimCustomer de origem exibida.  
  
2.  Desmarque a caixa de seleção na parte superior das seguintes colunas:  
  
    |Cliente|  
    |--------------|  
    |**SpanishEducation**|  
    |**FrenchEducation**|  
    |**SpanishOccupation**|  
    |**FrenchOccupation**|  
  
     Como os valores destas colunas não são pertinentes à análise de vendas da Internet, não há necessidade de importar essas colunas. A eliminação de colunas desnecessárias reduzirá o tamanho do modelo.  
  
3.  Verifique se todas as outras colunas estão marcadas e clique em **OK**.  
  
     Observe as palavras **filtros aplicados** são exibidas agora na **detalhes do filtro** coluna no **cliente** linha; se você clicar no link você verá uma descrição de texto a filtros recém-aplicados.  
  
4.  Filtre as tabelas restantes desmarcando as caixas de seleção das colunas seguintes em cada tabela:  
  
    |data|  
    |----------|  
    |**DateKey**|  
    |**SpanishDayNameOfWeek**|  
    |**FrenchDayNameOfWeek**|  
    |**SpanishMonthName**|  
    |**FrenchMonthName**|  
  
    |Geografia|  
    |---------------|  
    |**SpanishCountryRegionName**|  
    |**FrenchCountryRegionName**|  
    |**IpAddressLocator**|  
  
    |Produto|  
    |-------------|  
    |**SpanishProductName**|  
    |**FrenchProductName**|  
    |**FrenchDescription**|  
    |**ChineseDescription**|  
    |**ArabicDescription**|  
    |**HebrewDescription**|  
    |**ThaiDescription**|  
    |**GermanDescription**|  
    |**JapaneseDescription**|  
    |**TurkishDescription**|  
  
    |Product Category|  
    |----------------------|  
    |**SpanishProductCategoryName**|  
    |**FrenchProductCategoryName**|  
  
    |Product Subcategory|  
    |-------------------------|  
    |**SpanishProductSubcategoryName**|  
    |**FrenchProductSubcategoryName**|  
  
    |Internet Sales|  
    |--------------------|  
    |**OrderDateKey**|  
    |**DueDateKey**|  
    |**ShipDateKey**|  
  
 Agora que você visualizou e filtrou os dados desnecessários, poderá importar os dados. Vá para a próxima seção **Importar as tabelas e os dados de coluna selecionados**.  
  
##  <a name="Import"></a> Importar os dados de coluna e tabelas selecionadas  
 Agora você pode importar os dados selecionados. O assistente importa os dados da tabela junto com as relações entre as tabelas. São criadas novas tabelas e colunas no modelo usando os nomes amigáveis que você especificou, e os dados que você filtrou não serão importados.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>Para importar os dados da tabela e da coluna selecionadas  
  
1.  Examine as seleções. Se tudo estiver correto, clique em **Concluir**.  
  
     Durante a importação dos dados, o assistente exibirá quantas linhas foram buscadas. Quando todos os dados tiverem sido importados, será exibida uma mensagem indicando êxito.  
  
    > [!TIP]  
    >  Para ver as relações que foram criadas automaticamente entre as tabelas importadas, na linha **Preparação de dados** , clique em **Detalhes**.  
  
2.  Clique em **Fechar**.  
  
     O assistente é fechado e o modelo de designer fica visível. Cada tabela foi adicionada como uma nova guia no designer de modelos.  
  
## <a name="save-the-model-project"></a>Salve o Projeto de Modelo.  
 É importante salvar frequentemente seu projeto de modelo.  
  
#### <a name="to-save-the-model-project"></a>Para salvar o projeto de modelo  
  
-   Em [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Arquivo** e clique em **Salvar Tudo**.  
  
## <a name="next-step"></a>Próxima etapa  
 Para continuar este tutorial, vá para a próxima lição: [Lição 3: Renomear colunas](rename-columns.md).  
  
  
