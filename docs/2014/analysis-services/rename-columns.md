---
title: 'Lição 3: Renomear colunas | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 5fc8ba1a-2b30-4775-9b3b-c09dee711b3e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 056f386db58f01f663cc04e82ce04e0c6c6597a6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748238"
---
# <a name="lesson-3-rename-columns"></a>Lição 3: Renomear colunas
  Nesta lição, você renomeará muitas das colunas em cada tabela que você importou. A renomeação torna as colunas mais identificáveis e fáceis de navegar em ambos os designers de modelos, e também pelos usuários que selecionam campos em um aplicativo cliente. Para obter mais informações, consulte [Renomear uma tabela ou coluna &#40;SSAS Tabular&#41;](tabular-models/rename-a-table-or-column-ssas-tabular.md).  
  
> [!IMPORTANT]  
>  A renomeação das colunas não é necessária para concluir este tutorial; no entanto, as lições restantes, em particular as que incluem a criação de relações e de colunas e medidas calculadas que usam fórmulas DAX, referem-se aos nomes amigáveis de coluna descritos nesta lição. Se você optar por não renomear colunas, será necessário editar as fórmulas DAX nas lições 5, 6 e 7 para usar os nomes de coluna de origem originais fornecidos nesta lição.  
  
 Tempo estimado para concluir esta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 2: Adicionar dados](lesson-2-add-data.md).  
  
## <a name="rename-columns"></a>Renomear colunas  
  
#### <a name="to-rename-columns"></a>Para renomear colunas  
  
1.  No designer de modelos, clique na tabela **Cliente** (guia).  
  
     Quando você clica em uma guia, essa tabela fica ativa na janela do designer de modelos.  
  
2.  Clique duas vezes o **CustomerKey** coluna Nome e, em seguida, digite `Customer  Id`, e pressione ENTER.  
  
    > [!TIP]  
    >  Você também pode renomear uma coluna na **nome da coluna** propriedade da coluna **propriedades** janela, ou na exibição de diagrama.  
  
3.  Renomeie as colunas restantes na tabela **Cliente** , bem como as colunas nas tabelas restantes, substituindo o nome de origem pelo nome amigável:  
  
     **Tabela Customer**  
  
    |Nome de origem|Nome amigável|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |CustomerAlternateKey|Customer Alternate Id|  
    |FirstName|First Name|  
    |MiddleName|Middle Name|  
    |LastName|Last Name|  
    |NameStyle|Name Style|  
    |BirthDate|Birth Date|  
    |MaritalStatus|Estado Civil|  
    |EmailAddress|Endereço de email|  
    |YearlyIncome|Renda Anual|  
    |TotalChildren|Total de Filhos|  
    |NumberChildrenAtHome|Number of Children At Home|  
    |EnglishEducation|Education|  
    |EnglishOccupation|Occupation|  
    |HouseOwnerFlag|Owns House|  
    |NumberCarsOwned|Number of Cars Owned|  
    |AddressLine1|Linha de endereço 1|  
    |AddressLine2|Address Line 2|  
    |Phone|Phone Number|  
    |DateFirstPurchase|Date of First Purchase|  
    |CommuteDistance|Distância do Trabalho|  
  
     **Data**  
  
    |Nome de origem|Nome amigável|  
    |-----------------|-------------------|  
    |FullDateAlternateKey|data|  
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
  
     **Geography**  
  
    |Nome de origem|Nome amigável|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |StateProvinceCode|State Province Code|  
    |StateProvinceName|State Province Name|  
    |CountryRegionCode|Country Region Code|  
    |EnglishCountryRegionName|Country Region Name|  
    |PostalCode|Postal Code|  
    |SalesTerritoryKey|Sales Territory Id|  
  
     **Product**  
  
    |Nome de origem|Nome amigável|  
    |-----------------|-------------------|  
    |ProductKey|Product Id|  
    |ProductAlternateKey|Product Alternate Id|  
    |ProductSubcategoryKey|Product Subcategory Id|  
    |WeightUnitMeasureCode|Weight Unit Code|  
    |SizeUnitMeasureCode|Size Unit Code|  
    |EnglishProductName|Nome do produto|  
    |StandardCost|Custo Padrão|  
    |FinishedGoodsFlag|Is Finished Product|  
    |SafetyStockLevel|Safety Stock Level|  
    |ReorderPoint|Reorder Point|  
    |ListPrice|Preço da Lista|  
    |SizeRange|Size Range|  
    |DaysToManufacture|Days to Manufacture|  
    |ProductLine|Product Line|  
    |Preço do Revendedor|Preço do Revendedor|  
    |ModelName|Model Name|  
    |LargePhoto|Large Photo|  
    |EnglishDescription|Descrição|  
    |StartDate|Product Start Date|  
    |EndDate|Product End Date|  
    |Status|Product Status|  
  
     **Categoria de produto**  
  
    |Nome de origem|Nome Amigável|  
    |-----------------|-------------------|  
    |ProductCategoryKey|Product Category Id|  
    |ProductCategoryAlternateKey|Product Category Alternate Id|  
    |EnglishProductCategoryName|Product Category Name|  
  
     **Subcategoria do produto**  
  
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
    |SalesOrderLineNumber|Sales Order Line Number|  
    |RevisionNumber|Número de Revisão|  
    |OrderQuantity|Order Quantity|  
    |UnitPrice|Preço Unitário|  
    |ExtendedAmount|Valor Ampliado|  
    |UnitPriceDiscountPct|Unit Price Discount Pct|  
    |DiscountAmount|Valor de desconto|  
    |ProductStandardCost|Custo Padrão do Produto|  
    |TotalProductCost|Custo Total do Produto|  
    |SalesAmount|Valor das Vendas|  
    |TaxAmt|Valor dos Impostos|  
    |CarrierTrackingNumber|Carrier Tracking Number|  
    |CustomerPONumber|Customer PO Number|  
    |OrderDate|Order Date|  
    |DueDate|Due Date|  
    |ShipDate|Ship Date|  
  
## <a name="next-step"></a>Próxima etapa  
 Para continuar este tutorial, vá para a próxima lição: [Lição 4: Marcar como tabela de data](lesson-3-mark-as-date-table.md).  
  
  
