---
title: "Lição do Analysis Services tutorial 2: obter dados | Microsoft Docs"
description: Descreve como obter e importar dados no projeto do tutorial do Analysis Services.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: 1fd06f563581d42764b5b6f29b3c22d8129f9160
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/20/2018
---
# <a name="get-data"></a>Obter dados

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você deve usar **obter dados** para se conectar ao banco de dados de exemplo AdventureWorksDW, selecionar os dados, visualizar e filtrar e, em seguida, importar para seu espaço de trabalho do modelo.  
  
Usando obter dados, você pode importar dados de uma ampla variedade de fontes. Dados também podem ser consultados usando uma expressão de fórmula Power Query M ou um [expressão de consulta SQL nativa](../tabular-models/ssas-import-query.md).

> [!NOTE]
> Tarefas e as imagens neste tutorial mostram se conectar a um banco de dados AdventureWorksDW2014 em um servidor local. Em alguns casos, um banco de dados AdventureWorksDW no Azure SQL Data Warehouse pode mostrar diferentes objetos. No entanto, eles são basicamente os mesmos.
  
Tempo estimado para concluir esta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 1: criar um novo projeto de modelo de tabela](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Criar uma conexão  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw-database"></a>Para criar uma conexão ao banco de dados AdventureWorksDW  
  
1.  Em **Gerenciador de modelos tabulares**, clique com botão direito **fontes de dados** > **importar de fonte de dados**.  
  
    Isso inicia **obter dados**, que orienta você se conectar a uma fonte de dados. Se você não vir o Gerenciador de modelos de tabela, em **Solution Explorer**, clique duas vezes em **Model.bim** para abrir o modelo no designer. 
    
    ![as-lesson2-getdata](../tutorial-tabular-1400/media/as-lesson2-getdata.png)
  
2.  Em obter dados, clique em **banco de dados** > **o banco de dados do SQL Server** > **conectar**.  
  
3.  No **o banco de dados do SQL Server** caixa de diálogo, na **servidor**, digite o nome do servidor onde você instalou o banco de dados AdventureWorksDW e, em seguida, clique em **conectar**.  

4.  Quando solicitado a inserir as credenciais, você precisa especificar as credenciais que do Analysis Services usa para se conectar à fonte de dados ao importar e processar dados. Em **modo de representação**, selecione **representar a conta**, em seguida, insira as credenciais e, em seguida, clique em **conectar**. É recomendável que usar uma conta em que a senha não expira.

    ![as-lesson2-account](../tutorial-tabular-1400/media/as-lesson2-account.png)
  
    > [!NOTE]  
    > O uso de uma conta de usuário e senha do Windows é o método mais seguro de conexão a uma fonte de dados.
  
5.  No navegador, selecione o **AdventureWorksDW** banco de dados e, em seguida, clique em **Okey**. Isso cria a conexão ao banco de dados. 
  
6.  No navegador, marque a caixa de seleção para as tabelas a seguir: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, e **FactInternetSales**.  

    ![as-lesson2-select-tables](../tutorial-tabular-1400/media/as-lesson2-select-tables.png)
  
Depois de clicar em Okey, Editor de consultas é aberto. Na próxima seção, você seleciona somente os dados que você deseja importar.

  
## <a name="filter-the-table-data"></a>Filtrar os dados da tabela  

Tabelas no banco de dados de exemplo AdventureWorksDW possuem dados que não não necessários incluir em seu modelo. Quando possível, você deseja filtrar os dados desnecessários para economizar espaço na memória usado pelo modelo. Você filtrará algumas das colunas de tabelas para que eles não estiverem importados para o banco de dados do espaço de trabalho ou o banco de dados do modelo após ele ter sido implantado. 
  
#### <a name="to-filter-the-table-data-before-importing"></a>Para filtrar os dados da tabela antes de importar  
  
1.  No Editor de consultas, selecione o **DimCustomer** tabela. Uma exibição da tabela DimCustomer na fonte de dados (seus dados de exemplo AdventureWorksDW) é exibida. 
  
2.  Multisseleção (Ctrl + clique) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, em seguida, clique com botão direito e clique **remover colunas**. 

    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-columns.png)
  
    Como os valores destas colunas não são pertinentes à análise de vendas da Internet, não há necessidade de importar essas colunas. Eliminação de colunas desnecessárias torna seu modelo menor e mais eficiente.  

    > [!TIP]
    > Se você cometer um erro, você pode fazer backup, excluindo uma etapa na **etapas aplicadas**.   
    
    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-step.png)

  
4.  Filtre as tabelas restantes, removendo as seguintes colunas em cada tabela:  
    
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
  
      Nenhuma coluna foi removida.
  
## <a name="Import"></a>Import the selected tables and column data  

Agora que você visualizou e filtrou os dados desnecessários, você pode importar o restante dos dados que você deseja. O assistente importa os dados da tabela junto com as relações entre as tabelas. Novas tabelas e colunas são criadas no modelo e não é possível importar dados que você filtrou.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>Para importar os dados da tabela e da coluna selecionadas  
  
1.  Examine as seleções. Se tudo estiver okey, clique em **importação**. A caixa de diálogo de processamento de dados mostra o status dos dados sendo importados de sua fonte de dados para seu banco de dados do espaço de trabalho.
  
    ![as-lesson2-success](../tutorial-tabular-1400/media/as-lesson2-success.png) 
  
2.  Clique em **Fechar**.  

  
## <a name="save-your-model-project"></a>Salvar seu projeto de modelo  

É importante salvar frequentemente seu projeto de modelo.  
  
#### <a name="to-save-the-model-project"></a>Para salvar o projeto de modelo  
  
-   Click **Arquivo** > **Salvar Tudo**.  
  
## <a name="whats-next"></a>O que vem a seguir?

[Lição 3: Marcar como tabela de data](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md).

  
  
