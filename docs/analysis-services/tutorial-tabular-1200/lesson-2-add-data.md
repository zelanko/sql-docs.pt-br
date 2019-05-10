---
title: 'Lição 2: Adicionar dados | Microsoft Docs'
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6e5a4d0ec80da5c29d513e74df1becca2d5cbb84
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404868"
---
# <a name="lesson-2-add-data"></a>Lição 2: Adicionar dados
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você usará o Assistente de importação de tabela no SSDT para se conectar ao banco de dados de exemplo SQL AdventureWorksDW, selecionar dados, visualizar e filtrar os dados e, em seguida, importar os dados para seu espaço de trabalho do modelo.  
  
Usando o Assistente de importação de tabela, você pode importar dados de uma variedade de fontes relacionais: Access, SQL, Oracle, Sybase, Informix, DB2, Teradata e muito mais. As etapas de importação de dados de cada uma dessas fontes relacionais são bem parecidas com as descritas a seguir. Dados também podem ser selecionados usando um procedimento armazenado. Para saber mais sobre como importar dados e os diferentes tipos de fontes de dados, você pode importar, consulte [fontes de dados](../tabular-models/data-sources-supported-ssas-tabular.md).  
  
Tempo estimado para concluir esta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 1: Criar um novo projeto de modelo de tabela](lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Criar uma conexão  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2014-database"></a>Para criar uma conexão para um banco de dados AdventureWorksDW2014  
  
1.  No Gerenciador de modelos tabulares, clique com botão direito **fontes de dados** > **importar da fonte de dados**.  
  
    Isso inicia o Assistente de importação de tabela, que orienta você pela configuração de uma conexão a uma fonte de dados. Se você não vir o Gerenciador de modelos tabulares, clique duas vezes **Model. BIM** na **Gerenciador de soluções** para abrir o modelo no designer. 
    
    ![as-tabular-lesson2-tme](media/as-tabular-lesson2-tme.png) 

    Observação: Se você estiver criando seu modelo no nível de compatibilidade 1400, você verá a nova experiência obter dados, em vez do Assistente de importação de tabela. As caixas de diálogo aparecerá um pouco diferentes do que as etapas a seguir, mas você ainda poderá acompanhá-los. 
  
2.  No Assistente de importação de tabela, sob **bancos de dados relacionais**, clique em **Microsoft SQL Server** > **próximo**.  
  
3.  Na página **Conectar a um Banco de Dados Microsoft SQL Server** , em **Nome de Conexão Amigável**, digite **BD Adventure Works do SQL**.  
  
4.  Na **nome do servidor**, digite o nome do servidor onde você instalou o banco de dados AdventureWorksDW.  
  
5.  No **nome do banco de dados** campo, selecione **AdventureWorksDW**e, em seguida, clique em **próxima**.  
  
    ![as-tabular-lesson2-tiw-name](media/as-tabular-lesson2-tiw-name.png)
  
6.  Na página **Informações sobre Representação** , é necessário especificar as credenciais que o Analysis Services usará para se conectar à fonte de dados ao importar e processar dados. Verifique se a opção **Nome de usuário e senha específicos do Windows** está selecionada e, em **Nome de Usuário** e **Senha**, insira suas credenciais de logon do Windows e clique em **Avançar**.  
  
    > [!NOTE]  
    > O uso de uma conta de usuário e senha do Windows é o método mais seguro de conexão a uma fonte de dados. Para obter mais informações, consulte [representação](../tabular-models/impersonation-ssas-tabular.md).  
  
7.  Na página **Escolher como Importar os Dados** , verifique se a opção **Selecionar itens em uma lista de tabelas e exibições para escolher os dados a serem importados** está marcada. Para selecionar em uma lista de tabelas e exibições, clique em **Avançar** para exibir uma lista de todas as tabelas de origem do banco de dados de origem.  
  
8.  No **selecionar tabelas e exibições** , marque a caixa de seleção para as tabelas a seguir: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**,  **DimProductSubcategory**, e **FactInternetSales**.  
  
    **NÃO** clique em **Concluir**.  
  
## <a name="FilterData"></a>Filter the table data  
A tabela DimCustomer que você está importando do banco de dados de exemplo contém um subconjunto dos dados do banco de dados do SQL Server da Adventure Works original. Você filtrará algumas mais das colunas da tabela DimCustomer que não são necessárias quando importados em seu modelo. Quando possível, você vai querer filtrar os dados que não serão usados para economizar espaço na memória usado pelo modelo.  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>Para filtrar os dados da tabela antes de importar  
  
1.  Selecione a linha para o **DimCustomer** tabela e, em seguida, clique em **visualizar e filtrar**. A janela **Visualizar Tabela Selecionada** é aberta com todas as colunas da tabela DimCustomer de origem exibida.  
  
2.  Desmarque a caixa de seleção na parte superior das seguintes colunas: **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**. 

    ![as-tabular-lesson2-tiw-clear](media/as-tabular-lesson2-tiw-clear.png)
  
    Como os valores destas colunas não são pertinentes à análise de vendas da Internet, não há necessidade de importar essas colunas. Eliminação das colunas desnecessárias tornará seu modelo menor e mais eficiente.  
  
3.  Verifique se todas as outras colunas estão marcadas e clique em **OK**.  
  
    Observe as palavras **filtros aplicados** são exibidas agora na **detalhes do filtro** coluna no **DimCustomer** de linha; se você clicar no link você verá uma descrição de texto a filtros recém-aplicados.  
    
    ![como-tabela-lição 2--filtros aplicados](media/as-tabular-lesson2-applied-filters.png)
    
  
4.  Filtre as tabelas restantes desmarcando as caixas de seleção das colunas seguintes em cada tabela:  
    
    **DimDate**
    
      |coluna|  
      |--------|  
      |**DateKey**|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |coluna|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |coluna|  
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
  
      |coluna|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |coluna|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |coluna|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Import the selected tables and column data  
Agora que você visualizou e filtrou os dados desnecessários, você pode importar o restante dos dados que você deseja. O assistente importa os dados da tabela junto com as relações entre as tabelas. Novas tabelas e colunas são criadas no modelo e dados que você filtrou não serão importados.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>Para importar os dados da tabela e da coluna selecionadas  
  
1.  Examine as seleções. Se tudo estiver okey, clique em **concluir**.  
  
    Durante a importação dos dados, o assistente exibirá quantas linhas foram buscadas. Quando todos os dados tiverem sido importados, será exibida uma mensagem indicando êxito.  
    
    ![as-tabular-lesson2-success](media/as-tabular-lesson2-success.png) 
  
    > [!TIP]  
    > Para ver as relações que foram criadas automaticamente entre as tabelas importadas, na linha **Preparação de dados** , clique em **Detalhes**. 
  
2.  Clique em **Fechar**.  
  
    O assistente é fechado e o designer de modelos agora mostra as tabelas importadas. 
  
## <a name="save-your-model-project"></a>Salvar seu projeto de modelo  
É importante salvar frequentemente seu projeto de modelo.  
  
#### <a name="to-save-the-model-project"></a>Para salvar o projeto de modelo  
  
-   Click **Arquivo** > **Salvar Tudo**.  
  
## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [Lição 3: Marcar como tabela de data](lesson-3-mark-as-date-table.md).

  
  
