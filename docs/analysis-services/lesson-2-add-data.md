---
title: 'Lição 2: Adicionar dados | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4a7c3756e6c8c35472b760d9fa3100b4f40ecfdc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019203"
---
# <a name="lesson-2-add-data"></a>Lição 2: Adicionar dados
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você usará o Assistente de importação de tabela no SSDT para se conectar ao banco de dados SQL AdventureWorksDW, selecionar dados, visualizar e filtrar os dados e, em seguida, importar os dados para seu espaço de trabalho do modelo.  
  
Usando o Assistente de importação de tabela, você pode importar dados de uma variedade de fontes relacionais: Access, SQL, Oracle, Sybase, Informix, DB2, Teradata e muito mais. As etapas de importação de dados de cada uma dessas fontes relacionais são bem parecidas com as descritas a seguir. Dados também podem ser selecionados usando um procedimento armazenado. Para saber mais sobre como importar dados e os diferentes tipos de fontes de dados, você pode importar, consulte [fontes de dados](../analysis-services/tabular-models/data-sources-ssas-tabular.md).  
  
Tempo estimado para concluir esta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas desta lição, você deve ter concluído a lição anterior: [Lição 1: Criar um novo projeto de modelo de tabela](../analysis-services/lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Criar uma conexão  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2014-database"></a>Para criar uma conexão para um banco de dados AdventureWorksDW2014  
  
1.  No Gerenciador de modelos de tabela, clique com botão direito **fontes de dados** > **importar de fonte de dados**.  
  
    Isso inicia o Assistente de importação de tabela, que fornece instruções para configurar uma conexão a uma fonte de dados. Se você não vir o Gerenciador de modelos de tabela, clique duas vezes em **Model.bim** na **Solution Explorer** para abrir o modelo no designer. 
    
    ![como-tabela-lição 2-tempo](../analysis-services/media/as-tabular-lesson2-tme.png) 

    Observação: Se você estiver criando o modelo de nível de compatibilidade 1400, você verá a nova experiência de obter dados em vez do Assistente de importação de tabela. As caixas de diálogo aparecerá um pouco diferentes do que as etapas abaixo, mas ainda será capaz de acompanhar. 
  
2.  No Assistente de importação de tabela, em **bancos de dados relacionais**, clique em **Microsoft SQL Server** > **próximo**.  
  
3.  Na página **Conectar a um Banco de Dados Microsoft SQL Server** , em **Nome de Conexão Amigável**, digite **BD Adventure Works do SQL**.  
  
4.  Em **nome do servidor**, digite o nome do servidor onde você instalou o banco de dados AdventureWorksDW.  
  
5.  No **nome do banco de dados** campo, selecione **AdventureWorksDW**e, em seguida, clique em **próximo**.  
  
    ![como tabular-lição 2-tiw-nome](../analysis-services/media/as-tabular-lesson2-tiw-name.png)
  
6.  Na página **Informações sobre Representação** , é necessário especificar as credenciais que o Analysis Services usará para se conectar à fonte de dados ao importar e processar dados. Verifique se a opção **Nome de usuário e senha específicos do Windows** está selecionada e, em **Nome de Usuário** e **Senha**, insira suas credenciais de logon do Windows e clique em **Avançar**.  
  
    > [!NOTE]  
    > O uso de uma conta de usuário e senha do Windows é o método mais seguro de conexão a uma fonte de dados. Para obter mais informações, consulte [representação](../analysis-services/tabular-models/impersonation-ssas-tabular.md).  
  
7.  Na página **Escolher como Importar os Dados** , verifique se a opção **Selecionar itens em uma lista de tabelas e exibições para escolher os dados a serem importados** está marcada. Para selecionar em uma lista de tabelas e exibições, clique em **Avançar** para exibir uma lista de todas as tabelas de origem do banco de dados de origem.  
  
8.  Na página **Selecionar tabelas e exibições** , marque a caixa de seleção para as tabelas a seguir: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**e **FactInternetSales**.  
  
    **NÃO** clique em **Concluir**.  
  
## <a name="FilterData"></a>Filter the table data  
A tabela DimCustomer que você está importando do banco de dados de exemplo contém um subconjunto dos dados do banco de dados do SQL Server Adventure Works original. Você filtrará pouco mais das colunas da tabela DimCustomer que não são necessárias quando importados para o seu modelo. Quando possível, você desejará filtrar dados que não possa ser utilizados para economizar espaço na memória usado pelo modelo.  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>Para filtrar os dados da tabela antes de importar  
  
1.  Selecione a linha para o **DimCustomer** de tabela e, em seguida, clique em **visualizar e filtrar**. A janela **Visualizar Tabela Selecionada** é aberta com todas as colunas da tabela DimCustomer de origem exibida.  
  
2.  Desmarque a caixa de seleção na parte superior das seguintes colunas: **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**. 

    ![como-tabela-lição 2-tiw-clear](../analysis-services/media/as-tabular-lesson2-tiw-clear.png)
  
    Como os valores destas colunas não são pertinentes à análise de vendas da Internet, não há necessidade de importar essas colunas. Eliminação de colunas desnecessárias reduzirá o modelo menor e mais eficiente.  
  
3.  Verifique se todas as outras colunas estão marcadas e clique em **OK**.  
  
    Observe que, agora, as palavras **Filtros aplicados** são exibidas na coluna **Detalhes do Filtro** na linha **DimCustomer** ; se você clicar nesse link, verá uma descrição textual dos filtros recém-aplicados.  
    
    ![como-tabela-lição 2--filtros aplicados](../analysis-services/media/as-tabular-lesson2-applied-filters.png)
    
  
4.  Filtre as tabelas restantes desmarcando as caixas de seleção das colunas seguintes em cada tabela:  
    
    **DimDate**
    
      |Coluna|  
      |--------|  
      |**DateKey**|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |Coluna|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |Coluna|  
      |-----------|  
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
  
    **DimProductCategory**
  
      |Coluna|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |Coluna|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |Coluna|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Import the selected tables and column data  
Agora que você visualizou e filtrou os dados desnecessários, você pode importar o restante dos dados que você deseja. O assistente importa os dados da tabela junto com as relações entre as tabelas. Novas tabelas e colunas são criadas no modelo e dados que você filtrou não serão importados.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>Para importar os dados da tabela e da coluna selecionadas  
  
1.  Examine as seleções. Se tudo estiver okey, clique em **concluir**.  
  
    Durante a importação dos dados, o assistente exibirá quantas linhas foram buscadas. Quando todos os dados tiverem sido importados, será exibida uma mensagem indicando êxito.  
    
    ![como-tabela-lição 2-êxito](../analysis-services/media/as-tabular-lesson2-success.png) 
  
    > [!TIP]  
    > Para ver as relações que foram criadas automaticamente entre as tabelas importadas, na linha **Preparação de dados** , clique em **Detalhes**. 
  
2.  Clique em **Fechar**.  
  
    O assistente for fechado e o designer de modelo agora mostra as tabelas importadas. 
  
## <a name="save-your-model-project"></a>Salvar seu projeto de modelo  
É importante salvar frequentemente seu projeto de modelo.  
  
#### <a name="to-save-the-model-project"></a>Para salvar o projeto de modelo  
  
-   Click **Arquivo** > **Salvar Tudo**.  
  
## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [lição 3: marcar como tabela de data](../analysis-services/lesson-3-mark-as-date-table.md).

  
  
