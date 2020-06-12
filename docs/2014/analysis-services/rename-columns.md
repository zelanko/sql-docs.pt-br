---
title: 'Lição 3: renomear colunas | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5fc8ba1a-2b30-4775-9b3b-c09dee711b3e
author: minewiskan
ms.author: owend
ms.openlocfilehash: ef23d99b4542880d9756bbdad2e5cfb368b4f43c
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84539358"
---
# <a name="lesson-3-rename-columns"></a>Lição 3: Renomear colunas
  Nesta lição, você renomeará muitas das colunas em cada tabela que você importou. A renomeação torna as colunas mais identificáveis e fáceis de navegar em ambos os designers de modelos, e também pelos usuários que selecionam campos em um aplicativo cliente. Para obter mais informações, consulte [Renomear uma tabela ou coluna &#40;SSAS Tabular&#41;](tabular-models/rename-a-table-or-column-ssas-tabular.md).  
  
> [!IMPORTANT]  
>  A renomeação das colunas não é necessária para concluir este tutorial; no entanto, as lições restantes, em particular as que incluem a criação de relações e de colunas e medidas calculadas que usam fórmulas DAX, referem-se aos nomes amigáveis de coluna descritos nesta lição. Se você optar por não renomear colunas, será necessário editar as fórmulas DAX nas lições 5, 6 e 7 para usar os nomes de coluna de origem originais fornecidos nesta lição.  
  
 Tempo estimado para conclusão desta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 2: Adicionar dados](lesson-2-add-data.md).  
  
## <a name="rename-columns"></a>Renomear colunas  
  
#### <a name="to-rename-columns"></a>Para renomear colunas  
  
1.  No designer de modelos, clique na tabela **Cliente** (guia).  
  
     Quando você clica em uma guia, essa tabela fica ativa na janela do designer de modelos.  
  
2.  Clique duas vezes no nome da coluna **CustomerKey** , digite `Customer  Id` e pressione Enter.  
  
    > [!TIP]  
    >  Você também pode renomear uma coluna na propriedade **nome da coluna** na janela **Propriedades** da coluna ou na exibição de diagrama.  
  
3.  Renomeie as colunas restantes na tabela **Cliente** , bem como as colunas nas tabelas restantes, substituindo o nome de origem pelo nome amigável:  
  
     **Tabela Customer**  
  
    |Nome de origem|Nome amigável|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |CustomerAlternateKey|Customer Alternate Id|  
    |Nome|Nome|  
    |MiddleName|Middle Name|  
    |LastName|Sobrenome|  
    |NameStyle|Name Style|  
    |BirthDate|Birth Date|  
    |MaritalStatus|Estado Civil|  
    |EmailAddress|Endereço de Email|  
    |YearlyIncome|Renda Anual|  
    |TotalChildren|Total de Filhos|  
    |NumberChildrenAtHome|Number of Children At Home|  
    |EnglishEducation|Educação|  
    |EnglishOccupation|Occupation|  
    |HouseOwnerFlag|Owns House|  
    |NumberCarsOwned|Number of Cars Owned|  
    |AddressLine1|Linha de endereço 1|  
    |AddressLine2|Address Line 2|  
    |Telefone|Número do telefone|  
    |DateFirstPurchase|Date of First Purchase|  
    |CommuteDistance|Distância do Trabalho|  
  
     **Data**  
  
    |Nome de origem|Nome amigável|  
    |-----------------|-------------------|  
    |FullDateAlternateKey|Data|  
    |DayNumberOfWeek|Day Number of Week|  
    |EnglishDayNameOfWeek|Day Name|  
    |DayNumberOfMonth|Day of Month|  
    |DayNumberOfYear|Day of Year|  
    |WeekNumberOfYear|Week Number of Year|  
    |EnglishMonthName|Month Name|  
    |MonthNumberOfYear|Month|  
    |CalendarQuarter|Calendar Quarter|  
    |CalendarYear|Calendar Year|  
    |CalendarSemester|Calendar Semester|  
    |FiscalQuarter|Fiscal Quarter|  
    |FiscalYear|Fiscal Year|  
    |FiscalSemester|Fiscal Semester|  
  
     **Geografia**  
  
    |Nome de origem|Nome amigável|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |StateProvinceCode|State Province Code|  
    |StateProvinceName|State Province Name|  
    |CountryRegionCode|Country Region Code|  
    |EnglishCountryRegionName|Country Region Name|  
    |PostalCode|Código postal|  
    |SalesTerritoryKey|Sales Territory Id|  
  
     **Produto**  
  
    |Nome de origem|Nome amigável|  
    |-----------------|-------------------|  
    |ProductKey|Product Id|  
    |ProductAlternateKey|Product Alternate Id|  
    |ProductSubcategoryKey|Product Subcategory Id|  
    |WeightUnitMeasureCode|Weight Unit Code|  
    |SizeUnitMeasureCode|Size Unit Code|  
    |EnglishProductName|Nome do Produto|  
    |StandardCost|Custo Padrão|  
    |FinishedGoodsFlag|Is Finished Product|  
    |SafetyStockLevel|Safety Stock Level|  
    |ReorderPoint|Reorder Point|  
    |ListPrice|Preço da Lista|  
    |SizeRange|Size Range|  
    |DaysToManufacture|Days to Manufacture|  
    |ProductLine|Product Line|  
    |Preço do Revendedor|Preço do Revendedor|  
    |ModelName|Nome do modelo|  
    |LargePhoto|Large Photo|  
    |EnglishDescription|Description|  
    |StartDate|Product Start Date|  
    |EndDate|Product End Date|  
    |Status|Product Status|  
  
     **Categoria do Produto**  
  
    |Nome de origem|Nome amigável|  
    |-----------------|-------------------|  
    |ProductCategoryKey|Product Category Id|  
    |ProductCategoryAlternateKey|Product Category Alternate Id|  
    |EnglishProductCategoryName|Product Category Name|  
  
     **Product Subcategory**  
  
    |Nome de origem|Nome amigável|  
    |-----------------|-------------------|  
    |ProductSubcategoryKey|Product Subcategory Id|  
    |ProductSubcategoryAlternateKey|Product Subcategory Alternate Id|  
    |EnglishProductSubcategoryName|Product Subcategory Name|  
    |ProductCategoryKey|Product Category Id|  
  
     **Vendas pela Internet**  
  
    |Nome de origem|Nome amigável|  
    |-----------------|-------------------|  
    |ProductKey|Product Id|  
    |CustomerKey|Customer Id|  
    |PromotionKey|Promotion Id|  
    |CurrencyKey|Currency Id|  
    |SalesTerritoryKey|Sales Territory Id|  
    |SalesOrderNumber|Sales Order Number|  
    |SalesOrderLineNumber|Número da Linha do Pedido de Vendas|  
    |RevisionNumber|Número de Revisão|  
    |OrderQuantity|Order Quantity|  
    |UnitPrice|Preço Unitário|  
    |ExtendedAmount|Valor Ampliado|  
    |UnitPriceDiscountPct|Unit Price Discount Pct|  
    |DiscountAmount|Valor do desconto|  
    |ProductStandardCost|Custo Padrão do Produto|  
    |TotalProductCost|Custo Total do Produto|  
    |SalesAmount|Valor das Vendas|  
    |TaxAmt|Valor dos Impostos|  
    |CarrierTrackingNumber|Carrier Tracking Number|  
    |CustomerPONumber|Customer PO Number|  
    |OrderDate|Data do Pedido|  
    |DueDate|Due Date|  
    |ShipDate|Ship Date|  
  
## <a name="next-step"></a>Próxima etapa  
 Para continuar este tutorial, vá para a próxima lição: [Lição 4: Marcar como Tabela de Data](lesson-3-mark-as-date-table.md).  
  
  
