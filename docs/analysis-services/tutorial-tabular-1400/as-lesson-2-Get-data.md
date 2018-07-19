---
title: 'Lição 2 do tutorial de serviços de análise: obter dados | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9adeebfbd3c49761adb816a7d28472a61ffca5cc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38007197"
---
# <a name="get-data"></a>Obter dados

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você deve usar **obter dados** para se conectar ao banco de dados de amostra AdventureWorksDW, selecionar dados, visualizar e filtrar e, em seguida, importar para seu espaço de trabalho do modelo.  
  
Ao usar obter dados, você pode importar dados de uma ampla variedade de fontes. Dados também podem ser consultados usando uma expressão de fórmula Power Query M ou um [expressão de consulta SQL nativa](../tabular-models/ssas-import-query.md).

> [!NOTE]
> Tarefas e as imagens neste tutorial mostram como se conectar a um banco de dados AdventureWorksDW2014 em um servidor de local. Em alguns casos, um banco de dados do AdventureWorksDW no Azure SQL Data Warehouse pode mostrar diferentes objetos. No entanto, eles são basicamente os mesmos.
  
Tempo estimado para concluir esta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 1: criar um novo projeto de modelo de tabela](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Criar uma conexão  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw-database"></a>Para criar uma conexão ao banco de dados AdventureWorksDW  
  
1.  Na **Gerenciador de modelos tabulares**, clique com botão direito **fontes de dados** > **importar da fonte de dados**.  
  
    Isso inicia **obter dados**, que orienta você pela conexão a uma fonte de dados. Se você não vir o Gerenciador de modelos tabulares, no **Gerenciador de soluções**, clique duas vezes em **Model. BIM** para abrir o modelo no designer. 
    
    ![as-lesson2-getdata](../tutorial-tabular-1400/media/as-lesson2-getdata.png)
  
2.  Em obter dados, clique em **banco de dados** > **banco de dados do SQL Server** > **Connect**.  
  
3.  No **banco de dados do SQL Server** caixa de diálogo, na **Server**, digite o nome do servidor onde você instalou o banco de dados AdventureWorksDW e, em seguida, clique em **Connect**.  

4.  Quando solicitado a inserir as credenciais, você precisa especificar as credenciais que do Analysis Services usa para se conectar à fonte de dados ao importar e processar dados. Na **modo de representação**, selecione **representar a conta**, em seguida, insira as credenciais e, em seguida, clique em **Connect**. É recomendável que usar uma conta em que a senha não expira.

    ![as-lesson2-account](../tutorial-tabular-1400/media/as-lesson2-account.png)
  
    > [!NOTE]  
    > O uso de uma conta de usuário e senha do Windows é o método mais seguro de conexão a uma fonte de dados.
  
5.  No navegador, selecione a **AdventureWorksDW** do banco de dados e, em seguida, clique em **Okey**. Isso cria a conexão ao banco de dados. 
  
6.  No navegador, selecione a caixa de seleção para as tabelas a seguir: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, e **FactInternetSales**.  

    ![como-lição 2-select-tables](../tutorial-tabular-1400/media/as-lesson2-select-tables.png)
  
Depois de clicar em Okey, Editor de consultas é aberto. Na próxima seção, você deve selecionar apenas os dados que você deseja importar.

  
## <a name="filter-the-table-data"></a>Filtrar os dados da tabela  

Tabelas no banco de dados de exemplo AdventureWorksDW têm dados que não não necessários incluir em seu modelo. Quando possível, você deseja filtrar os dados desnecessários para economizar espaço na memória usado pelo modelo. Você filtrará algumas das colunas de tabelas para que eles não sejam importados para o banco de dados do espaço de trabalho ou o banco de dados do modelo após ele ter sido implantado. 
  
#### <a name="to-filter-the-table-data-before-importing"></a>Para filtrar os dados da tabela antes de importar  
  
1.  No Editor de consultas, selecione a **DimCustomer** tabela. Uma exibição da tabela DimCustomer na fonte de dados (seu banco de dados AdventureWorksDW) é exibida. 
  
2.  Seleção múltipla (Ctrl + clique) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, em seguida, Clique com botão direito e, em seguida, clique em **remover colunas**. 

    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-columns.png)
  
    Como os valores destas colunas não são pertinentes à análise de vendas da Internet, não há necessidade de importar essas colunas. Eliminação das colunas desnecessárias torna seu modelo menor e mais eficiente.  

    > [!TIP]
    > Se você cometer um erro, você pode fazer backup ao excluir uma etapa na **etapas aplicadas**.   
    
    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-step.png)

  
4.  Filtre as tabelas restantes, removendo as colunas a seguir em cada tabela:  
    
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
  
      Nenhuma coluna foi removida.
  
## <a name="Import"></a>Import the selected tables and column data  

Agora que você visualizou e filtrou os dados desnecessários, você pode importar o restante dos dados que você deseja. O assistente importa os dados da tabela junto com as relações entre as tabelas. Novas tabelas e colunas são criadas no modelo e dados que você filtrou não serão importados.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>Para importar os dados da tabela e da coluna selecionadas  
  
1.  Examine as seleções. Se tudo estiver okey, clique em **importação**. A caixa de diálogo de processamento de dados mostra o status dos dados sendo importados de sua fonte de dados para o seu banco de dados do espaço de trabalho.
  
    ![as-lesson2-success](../tutorial-tabular-1400/media/as-lesson2-success.png) 
  
2.  Clique em **Fechar**.  

  
## <a name="save-your-model-project"></a>Salvar seu projeto de modelo  

É importante salvar frequentemente seu projeto de modelo.  
  
#### <a name="to-save-the-model-project"></a>Para salvar o projeto de modelo  
  
-   Click **Arquivo** > **Salvar Tudo**.  
  
## <a name="whats-next"></a>O que vem a seguir?

[Lição 3: Marcar como tabela de data](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md).

  
  
