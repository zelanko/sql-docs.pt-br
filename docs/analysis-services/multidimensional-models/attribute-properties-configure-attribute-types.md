---
title: Configurar tipos de atributo | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time dimensions [Analysis Services]
- attributes [Analysis Services], types
- slowly changing dimensions
- account dimensions [Analysis Services]
- currency dimensions [Analysis Services]
- Type property
ms.assetid: c2c6a3da-555e-4362-a83f-88da28427520
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 740d140999a182df59eb9741c5addedd9dac0aac
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-properties---configure-attribute-types"></a>Propriedades de atributo - configurar tipos de atributo
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], os tipos de atributo ajudam a classificar um atributo em termos de funcionalidade empresarial. Existem muitos tipos de atributo, sendo que a maioria é usada por aplicativos cliente para exibir ou oferecer suporte a um atributo. No entanto, alguns tipos de atributo também têm significado específico para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Por exemplo, alguns tipos de atributo identificam atributos que representam períodos de tempo em vários calendários de dimensões de tempo.  
  
##  <a name="setting_attibute_types"></a> Definindo tipos de atributo  
 O valor da propriedade **Type** de um atributo determina seu tipo. Vários assistentes do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] configuram os tipos de atributo ao definir dimensões ou atributos. Esses assistentes do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também configuram os tipos de atributo quando os assistentes adicionam funcionalidades às dimensões. Por exemplo, o Assistente de Business Intelligence aplica diversos tipos de atributo aos atributos de uma dimensão quando o assistente adiciona inteligência de contas para identificar nas dimensão os atributos que contêm nomes, códigos, números e estrutura de conta. O Assistente de Business Intelligence também utiliza tipos de atributo, como para conversão de moeda. Para obter mais informações, consulte [Criar uma dimensão de tipo Moeda](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).  
  
 As tabelas a seguir listam os tipos de atributo disponíveis no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Essas tabelas separam os tipos de atributo nas seguintes categorias:  
  
|Termo|Definição|  
|----------|----------------|  
|[Tipos de atributo gerais](#general_attribute_types)|Esses valores estão disponíveis para todos os atributos e existem apenas para possibilitar a classificação dos atributos para uso por aplicativos cliente.|  
|[Tipos de atributo de dimensão de conta](#account_dimension_attribute_types)|Esses valores identificam um atributo que pertence a uma dimensão de contas. Para obter mais informações sobre dimensões de conta, consulte [Criar uma Conta de Finanças de dimensão de tipo pai-filho](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md).|  
|[Tipo de atributo de dimensão de moedas](#currency_dimension_attribute_types)|Esses valores identificam um atributo que pertence a uma dimensão de moedas. Para obter mais informações sobre dimensões de moeda, consulte [Criar uma dimensão de tipo de moeda](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).|  
|[Atributos de dimensão de alteração lenta](#slowly_changing_dimension_attribute_types)|Esses valores identificam um atributo que pertence a uma dimensão de alteração lenta.|  
|[Atributos de dimensão de tempo](#time_dimension_attribute_types)|Esses valores identificam um atributo que pertence a uma dimensão de tempo. Para obter mais informações sobre dimensões de tempo, consulte [Criar uma dimensão de tipo de data](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md).|  
  
###  <a name="general_attribute_types"></a> General Attribute Types  
  
|Valor do tipo de atributo|Description|  
|--------------------------|-----------------|  
|**Endereço**|Representa um endereço.|  
|**AddressBuilding**|Representa o identificador da construção do endereço.|  
|**AddressCity**|Representa a cidade do endereço.|  
|**AddressCountry**|Representa o país ou a região do endereço.|  
|**AddressFax**|Representa o número de telefone e fax.|  
|**AddressFloor**|Representa o identificador de andar do endereço.|  
|**AddressHouse**|Representa o número da casa do endereço.|  
|**AddressPhone**|Representa o número de telefone.|  
|**AddressQuarter**|Representa o quarteirão do endereço.|  
|**AddressRoom**|Representa o identificador de conjunto do endereço.|  
|**AddressStateOrProvince**|Representa o estado do endereço.|  
|**AddressStreet**|Representa a rua do endereço.|  
|**AddressZip**|Representa o Cep ou código postal do endereço.|  
|**BomResource**|Representa um recurso de uma conta de materiais (BOM).|  
|**Caption**|Representa uma legenda.|  
|**CaptionAbbreviation**|Representa uma abreviação.|  
|**CaptionDescription**|Representa uma descrição.|  
|**Canal**|Representa um canal.|  
|**Cidade**|Representa uma cidade.|  
|**Empresa**|Representa uma empresa.|  
|**Continente**|Representa um continente.|  
|**País**|Representa um país ou região.|  
|**Região**|Representa um município.|  
|**CustomerGroup**|Representa um grupo de clientes.|  
|**CustomerHousehold**|Representa uma casa de clientes.|  
|**Customers**|Representa um cliente.|  
|**DateCanceled**|Representa uma data de cancelamento.|  
|**DateDuration**|Representa uma duração.|  
|**DateEnded**|Representa uma data de término.|  
|**DateModified**|Representa uma data de modificação.|  
|**DateStart**|Representa uma data de início.|  
|**DeletedFlag**|Indica se um membro deve ou não ser excluído (em termos de funcionalidade empresarial.)<br /><br /> Observação: o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não usa esse tipo de atributo para determinar se um membro deve ser excluído. Em vez dele, o tipo de atributo destina-se a uso por aplicativos cliente apenas para exibição.|  
|**FormattingColor**|Representa a cor usada na formatação.|  
|**FormattingFont**|Representa a fonte usada na formatação.|  
|**FormattingFontEffects**|Representa os efeitos de fonte usados na formatação.|  
|**FormattingFontSize**|Representa o tamanho de fonte usado na formatação.|  
|**FormattingOrder**|Representa a ordem usada na formatação.|  
|**FormattingSubtotal**|Representa um subtotal.|  
|**GeoBoundaryBottom**|Representa o valor mais baixo de um limite geográfico.|  
|**GeoBoundaryFront**|Representa o valor à frente de um limite geográfico.|  
|**GeoBoundaryLeft**|Representa o valor mais à esquerda de um limite geográfico.|  
|**GeoBoundaryPolygon**|Representa a definição de polígono de um limite geográfico.|  
|**GeoBoundaryRear**|Representa o valor ao fundo de um limite geográfico.|  
|**GeoBoundaryRight**|Representa o valor mais à direita de um limite geográfico.|  
|**GeoBoundaryTop**|Representa o valor mais alto de um limite geográfico.|  
|**GeoCentroidX**|Representa um centroide do eixo X para uma região geográfica.|  
|**GeoCentroidY**|Representa um centroide do eixo Y para uma região geográfica.|  
|**GeoCentroidZ**|Representa um centroide do eixo Z para uma região geográfica.|  
|**ID**|Representa um identificador (ID) ou chave.|  
|**Imagem**|Representa uma imagem em um formato gráfico indefinido.|  
|**ImageBmp**|Representa uma imagem em um formato gráfico de bitmap.|  
|**ImageGif**|Representa uma imagem em formato gráfico GIF (Graphics Interchange Format).|  
|**ImageJpg**|Representa uma imagem em formato gráfico JPEG (Joint Photographic Experts Group).|  
|**ImagePng**|Representa uma imagem em formato gráfico PNG (Portable Network Graphics).|  
|**ImageTiff**|Representa uma imagem em formato gráfico TIFF (Tagged Image File Format).|  
|**OrganizationalUnit**|Representa uma unidade organizacional.|  
|**OrgTitle**|Representa um cargo organizacional.|  
|**PercentOwnership**|Representa um percentual de propriedade.|  
|**PercentVoteRight**|Representa um percentual de direitos de voto.|  
|**Person**|Representa uma pessoa.|  
|**PersonContact**|Representa as informações de contato de uma pessoa.|  
|**PersonDemographic**|Representa as informações demográficas de uma pessoa.|  
|**PersonFirstName**|Representa o primeiro nome de uma pessoa.|  
|**PersonFullName**|Representa o nome completo de uma pessoa.|  
|**PersonLastName**|Representa o sobrenome de uma pessoa.|  
|**PersonMiddleName**|Representa o nome do meio de uma pessoa.|  
|**PhysicalColor**|Representa uma cor.|  
|**PhysicalDensity**|Representa densidade.|  
|**PhysicalDepth**|Representa profundidade.|  
|**PhysicalHeight**|Representa altura.|  
|**PhysicalSize**|Representa um tamanho.|  
|**PhysicalVolume**|Representa volume.|  
|**PhysicalWeight**|Representa peso.|  
|**PhysicalWidth**|Representa largura.|  
|**Ponto**|Representa um ponto.|  
|**PostalCode**|Representa um código postal.|  
|**Product**|Representa um produto.|  
|**ProductBrand**|Representa uma marca de produto.|  
|**ProductCategory**|Representa uma categoria de produto.|  
|**ProductGroup**|Representa um grupo de produtos.|  
|**ProductSKU**|Representa uma unidade de manutenção de estoque de produto (SKU, Stock Keeping Unit).|  
|**Projeto**|Representa um projeto.|  
|**ProjectCode**|Representa um código de projeto.|  
|**ProjectCompletion**|Representa o estado de conclusão de um projeto.|  
|**ProjectEndDate**|Representa a data de término de um projeto.|  
|**ProjectName**|Representa o nome de um projeto.|  
|**ProjectStartDate**|Representa a data de início de um projeto.|  
|**Promoção**|Representa uma promoção.|  
|**QtyRangeHigh**|Representa o valor mais alto de um intervalo de quantidades.|  
|**QtyRangeLow**|Representa o valor mais baixo de um intervalo de quantidades.|  
|**Quantitative**|Representa um atributo quantitativo.|  
|**Rate**|Representa uma taxa.|  
|**RateType**|Representa um tipo de taxa.|  
|**Região**|Representa uma região definida pelo cliente.|  
|**Regular**|Representa um atributo regular.|  
|**RelationToParent**|Representa uma relação com um pai.|  
|**Representante**|Representa um representante.|  
|**Cenário**|Representa um cenário.|  
|**Sequência**|Representa um atributo de sequência.|  
|**ShortCaption**|Representa uma legenda curta.|  
|**StateOrProvince**|Representa um estado.|  
|**Utilitário**|Representa um utilitário.|  
|**Versão**|Representa uma versão.|  
|**WebHtml**|Representa conteúdo HTML.|  
|**WebMailAlias**|Representa um alias de email.|  
|**WebUrl**|Representa um endereço de URL.|  
|**WebXmlOrXsl**|Representa conteúdo XML ou XSL.|  
  
###  <a name="account_dimension_attribute_types"></a> Account Dimension Attribute Types  
  
|Valor do tipo de atributo|Description|  
|--------------------------|-----------------|  
|**Conta**|Representa o pai de uma conta. Normalmente, esse tipo de atributo é aplicado ao atributo pai de uma dimensão de contas.|  
|**AccountName**|Representa o nome de uma conta. Normalmente, esse tipo de atributo é aplicado aos atributos de chave de uma dimensão de contas.|  
|**AccountNumber**|Representa o número de uma conta.|  
|**AccountType**|Representa o tipo de uma conta. Esse tipo de atributo identifica a função de agregação de um membro de conta em uma dimensão do tipo conta no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
###  <a name="currency_dimension_attribute_types"></a> Tipo de atributo de dimensão de moedas  
  
|Valor do tipo de atributo|Description|  
|--------------------------|-----------------|  
|**CurrencyDestination**|Representa a moeda de destino de um câmbio monetário. Normalmente, esse tipo de atributo é aplicado ao atributo de chave de uma dimensão de relatório, para uso em conversão de moeda. Para obter mais informações sobre como a conversões de moeda, consulte [Conversões de moeda &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).|  
|**CurrencyIsoCode**|Representa o código da moeda da Organização de Padronização Internacional (ISO). Para obter mais informações sobre como a conversões de moeda, consulte [Conversões de moeda &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).|  
|**CurrencyName**|Representa o nome de uma moeda. Para obter mais informações sobre como a conversões de moeda, consulte [Conversões de moeda &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).|  
|**CurrencySource**|Representa a moeda de origem de um câmbio monetário. Normalmente, esse tipo de atributo é aplicado ao atributo de chave de uma dimensão de moedas, para uso em conversão de moeda. Para obter mais informações sobre como a conversões de moeda, consulte [Conversões de moeda &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).|  
  
###  <a name="slowly_changing_dimension_attribute_types"></a> Tipos de atributos de dimensão de alteração lenta  
  
|Valor do tipo de atributo|Description|  
|--------------------------|-----------------|  
|**ScdEndDate**|Representa a data de término efetiva para um membro de uma dimensão de alteração lenta.|  
|**ScdOriginalID**|Representa o identificador original de um membro em uma dimensão de alteração lenta.|  
|**ScdStartDate**|Representa a data de início efetiva para um membro de uma dimensão de alteração lenta.|  
|**ScdStatus**|Representa o status efetivo de um membro de uma dimensão de alteração lenta.|  
  
###  <a name="time_dimension_attribute_types"></a> Tipos de atributo de dimensão de tempo  
  
|Valor do tipo de atributo|Description|  
|--------------------------|-----------------|  
|**Data**|Representa uma data. Normalmente, esse tipo de atributo é aplicado ao atributo de chave de uma dimensão de tempo ou dimensão de tempo de servidor.|  
|**DayOfHalfYear**|Representa o ordinal de dia de um semestre.|  
|**DayOfMonth**|Representa o ordinal de dia de um mês.|  
|**DayOfQuarter**|Representa o ordinal de dia de um semestre.|  
|**DayOfTenDays**|Representa o ordinal de dia de um período de dez dias.|  
|**DayOfTrimester**|Representa o ordinal de dia de um quadrimestre.|  
|**DayOfWeek**|Representa o ordinal de dia de uma semana.|  
|**DayOfYear**|Representa o ordinal de dia de um ano.|  
|**Days (dias)**|Representa dias.|  
|**FiscalDate**|Representa uma data em um calendário fiscal.|  
|**FiscalDayOfHalfYear**|Representa o ordinal de dia de um semestre em um calendário fiscal.|  
|**FiscalDayOfMonth**|Representa o ordinal de dia de um mês em um calendário fiscal.|  
|**FiscalDayOfQuarter**|Representa o ordinal de dia de um trimestre em um calendário fiscal.|  
|**FiscalDayOfTrimester**|Representa o ordinal de dia de um quadrimestre em um calendário fiscal.|  
|**FiscalDayOfWeek**|Representa o ordinal de dia de uma semana em um calendário fiscal.|  
|**FiscalDayOfYear**|Representa o ordinal de dia de um ano em um calendário fiscal.|  
|**FiscalHalfYears**|Representa semestres em um calendário fiscal.|  
|**FiscalHalfYearOfYear**|Representa o ordinal de semestre de um ano em um calendário fiscal.|  
|**FiscalMonths**|Representa os meses em um calendário fiscal.|  
|**FiscalMonthOfHalfYear**|Representa o ordinal de mês de um semestre em um calendário fiscal.|  
|**FiscalMonthOfQuarter**|Representa o ordinal de mês de um trimestre em um calendário fiscal.|  
|**FiscalMonthOfTrimester**|Representa o ordinal de mês de um quadrimestre em um calendário fiscal.|  
|**FiscalMonthOfYear**|Representa o ordinal de mês de um ano em um calendário fiscal.|  
|**FiscalQuarters**|Representa os trimestres em um calendário fiscal.|  
|**FiscalQuarterOfHalfYear**|Representa o ordinal de trimestre de um semestre em um calendário fiscal.|  
|**FiscalQuarterOfYear**|Representa o ordinal de trimestre de um ano em um calendário fiscal.|  
|**FiscalTrimesters**|Representa os quadrimestres em um calendário fiscal.|  
|**FiscalTrimesterOfYear**|Representa o ordinal de quadrimestre de um ano em um calendário fiscal.|  
|**FiscalWeeks**|Representa as semanas em um calendário fiscal.|  
|**FiscalWeekOfHalfYear**|Representa o ordinal de semana de um semestre em um calendário fiscal.|  
|**FiscalWeekOfMonth**|Representa o ordinal de semana de um mês em um calendário fiscal.|  
|**FiscalWeekOfQuarter**|Representa o ordinal de semana de um trimestre em um calendário fiscal.|  
|**FiscalWeekOfTrimester**|Representa o ordinal de semana de um quadrimestre em um calendário fiscal.|  
|**FiscalWeekOfYear**|Representa o ordinal de semana de um ano em um calendário fiscal.|  
|**FiscalYears**|Representa os anos em um calendário fiscal.|  
|**HalfYears**|Representa semestres.|  
|**HalfYearOfYear**|Representa o ordinal de semestre de um ano.|  
|**Hours (horas)**|Representa horas.|  
|**IsHoliday**|Indica se uma data é um feriado.|  
|**ISO8601Date**|Representa uma data em um calendário ISO 8601.|  
|**ISO8601DayOfWeek**|Representa o ordinal de dia de uma semana em um calendário ISO 8601.|  
|**ISO8601DayOfYear**|Representa o ordinal de dia de um ano em um calendário ISO 8601.|  
|**ISO8601Weeks**|Representa semanas em um calendário ISO 8601.|  
|**ISO8601WeekOfYear**|Representa o ordinal de semana de um ano em um calendário ISO 8601.|  
|**ISO8601Years**|Representa os anos em um calendário ISO 8601.|  
|**IsPeakDay**|Indica se uma data é um dia de pico.|  
|**IsWeekDay**|Indica se uma data é um dia de semana.|  
|**IsWorkingDay**|Indica se uma data é um dia útil.|  
|**ManufacturingDate**|Representa uma data em um calendário de produção.|  
|**ManufacturingDayOfHalfYear**|Representa o ordinal de dia de um semestre em um calendário de produção.|  
|**ManufacturingDayOfMonth**|Representa o ordinal de dia de um mês em um calendário de produção.|  
|**ManufacturingDayOfQuarter**|Representa o ordinal de dia de um trimestre em um calendário de produção.|  
|**ManufacturingDayOfTrimester**|Representa o ordinal de dia de um quadrimestre em um calendário de produção.|  
|**ManufacturingDayOfWeek**|Representa o ordinal de dia de uma semana em um calendário de produção.|  
|**ManufacturingDayOfYear**|Representa o ordinal de dia de um ano em um calendário de produção.|  
|**ManufacturingHalfYears**|Representa semestres em um calendário de produção.|  
|**ManufacturingHalfYearOfYear**|Representa o ordinal de semestre de um ano em um calendário de produção.|  
|**ManufacturingMonths**|Representa os meses em um calendário de produção.|  
|**ManufacturingMonthOfHalfYear**|Representa o ordinal de mês de um semestre em um calendário de produção.|  
|**ManufacturingMonthOfQuarter**|Representa o ordinal de mês de um trimestre em um calendário de produção.|  
|**ManufacturingMonthOfTrimester**|Representa o ordinal de mês de um quadrimestre em um calendário de produção.|  
|**ManufacturingMonthOfYear**|Representa o ordinal de mês de um ano em um calendário de produção.|  
|**ManufacturingQuarters**|Representa os trimestres em um calendário de produção.|  
|**ManufacturingQuarterOfHalfYear**|Representa o ordinal de trimestre de um semestre em um calendário de produção.|  
|**ManufacturingQuarterOfYear**|Representa o ordinal de trimestre de um ano em um calendário de produção.|  
|**ManufacturingWeeks**|Representa as semanas em um calendário de produção.|  
|**ManufacturingWeekOfHalfYear**|Representa o ordinal de semana de um semestre em um calendário de produção.|  
|**ManufacturingWeekOfMonth**|Representa o ordinal de semana de um mês em um calendário de produção.|  
|**ManufacturingWeekOfQuarter**|Representa o ordinal de semana de um trimestre em um calendário de produção.|  
|**ManufacturingWeekOfTrimester**|Representa o ordinal de semana de um quadrimestre em um calendário de produção.|  
|**ManufacturingWeekOfYear**|Representa o ordinal de semana de um ano em um calendário de produção.|  
|**ManufacturingYears**|Representa os anos em um calendário de produção.|  
|**Minutes (minutos)**|Representa minutos.|  
|**Months**|Representa meses.|  
|**MonthOfHalfYear**|Representa o ordinal de mês de um semestre.|  
|**MonthOfQuarter**|Representa o ordinal de mês de um trimestre.|  
|**MonthOfTrimester**|Representa o ordinal de mês de um quadrimestre.|  
|**MonthOfYear**|Representa o ordinal de mês de um ano.|  
|**Trimestres**|Representa trimestres.|  
|**QuarterOfHalfYear**|Representa o ordinal de quadrimestre de um semestre.|  
|**QuarterOfYear**|Representa o ordinal de trimestre de um ano.|  
|**ReportingDate**|Representa uma data em um calendário de relatório.|  
|**ReportingDayOfHalfYear**|Representa o ordinal de dia de um semestre em um calendário de relatório.|  
|**ReportingDayOfMonth**|Representa o ordinal de dia de um mês em um calendário de relatório.|  
|**ReportingDayOfQuarter**|Representa o ordinal de dia de um trimestre em um calendário de relatório.|  
|**ReportingDayOfTrimester**|Representa o ordinal de dia de um quadrimestre em um calendário de relatório.|  
|**ReportingDayOfWeek**|Representa o ordinal de dia de uma semana em um calendário de relatório.|  
|**ReportingDayOfYear**|Representa o ordinal de dia de um ano em um calendário de relatório.|  
|**ReportingHalfYears**|Representa os semestres em um calendário de relatório.|  
|**ReportingHalfYearOfYear**|Representa o ordinal de semestre de um ano em um calendário de relatório.|  
|**ReportingMonths**|Representa os meses em um calendário de relatório.|  
|**ReportingMonthOfHalfYear**|Representa o ordinal de mês de um semestre em um calendário de relatório.|  
|**ReportingMonthOfQuarter**|Representa o ordinal de mês de um trimestre em um calendário de relatório.|  
|**ReportingMonthOfTrimester**|Representa o ordinal de mês de um quadrimestre em um calendário de relatório.|  
|**ReportingMonthOfYear**|Representa o ordinal de mês de um ano em um calendário de relatório.|  
|**ReportingQuarters**|Representa os trimestres em um calendário de relatório.|  
|**ReportingQuarterOfHalfYear**|Representa o ordinal de trimestre de um semestre em um calendário de relatório.|  
|**ReportingQuarterOfYear**|Representa o ordinal de trimestre de um ano em um calendário de relatório.|  
|**ReportingTrimesters**|Representa os quadrimestres em um calendário de relatório.|  
|**ReportingTrimesterOfYear**|Representa o ordinal de quadrimestre de um ano em um calendário de relatório.|  
|**ReportingWeeks**|Representa as semanas em um calendário de relatório.|  
|**ReportingWeekOfHalfYear**|Representa o ordinal de semana de um semestre em um calendário de relatório.|  
|**ReportingWeekOfMonth**|Representa o ordinal de semana de um mês em um calendário de relatório.|  
|**ReportingWeekOfQuarter**|Representa o ordinal de semana de um trimestre em um calendário de relatório.|  
|**ReportingWeekOfTrimester**|Representa o ordinal de semana de um quadrimestre em um calendário de relatório.|  
|**ReportingWeekOfYear**|Representa o ordinal de semana de um ano em um calendário de relatório.|  
|**ReportingYears**|Representa os anos em um calendário de relatório.|  
|**Seconds (segundos)**|Representa segundos.|  
|**TenDayOfHalfYear**|Representa o ordinal de período de dez dias de um semestre.|  
|**TenDayOfMonth**|Representa o ordinal de período de dez dias de um mês.|  
|**TenDayOfQuarter**|Representa o ordinal de período de dez dias de um trimestre.|  
|**TenDayOfTrimester**|Representa o ordinal de período de dez dias de um quadrimestre.|  
|**TenDayOfYear**|Representa o ordinal de período de dez dias de um ano.|  
|**TenDays**|Representa períodos de dez dias.|  
|**Quadrimestres**|Representa quadrimestres.|  
|**TrimesterOfYear**|Representa o ordinal de quadrimestre de um ano.|  
|**UndefinedTime**|Representa um período de tempo indefinido.|  
|**WeekOfYear**|Representa o ordinal de semana de um ano.|  
|**Weeks**|Representa semanas.|  
|**WinterSummerSeason**|Indica se a data faz parte da estação de inverno/verão.|  
|**Years**|Representa anos.|  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e hierarquias de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  

