---
title: Tipo de elemento (DimensionAttribute) (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Type Element (DimensionAttribute)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 64fce1f5-39b7-4d0a-ae60-21203a03bd0d
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cd1ed987305726ea9e08eb507e2a1451d99e525b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="type-element-dimensionattribute-assl"></a>Elemento Type (DimensionAttribute) (ASSL)
  Contém o tipo do atributo.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DimensionAttribute>  
      ...  
   <Type>...</Type>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Regular*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Conta*|O atributo representa o nome de uma conta.|  
|*AccountNumber*|O atributo representa o número de uma conta.|  
|*AccountType*|O atributo representa o tipo de uma conta.|  
|*Endereço*|O atributo representa um endereço.|  
|*AddressBuilding*|O atributo representa o identificador da construção do endereço.|  
|*AddressCity*|O atributo representa a cidade de um endereço.|  
|*AddressCountry*|O atributo representa o país ou a região do endereço.|  
|*AddressFax*|O atributo representa um número de fax.|  
|*AddressFloor*|O atributo representa o identificador de andar do endereço.|  
|*AddressHouse*|O atributo representa o número da casa de um endereço.|  
|*AddressPhone*|O atributo representa o número de telefone.|  
|*AddressQuarter*|O atributo representa o bairro de um endereço.|  
|*AddressRoom*|O atributo representa o identificador de sala de um endereço.|  
|*AddressStateOrProvince*|O atributo representa o estado de um endereço.|  
|*AddressStreet*|O atributo representa a rua do endereço.|  
|*AddressZip*|O atributo representa o código postal (CEP) do endereço.|  
|*BOMResource*|O atributo representa um recurso de uma conta de materiais (BOM).|  
|*Legenda*|O atributo representa uma legenda.|  
|*CaptionAbbreviation*|O atributo representa uma abreviação.|  
|*CaptionDescription*|O atributo representa uma descrição.|  
|*Canal*|O atributo representa um canal.|  
|*Cidade*|O atributo representa uma cidade.|  
|*Empresa*|O atributo representa uma empresa.|  
|*Continente*|O atributo representa um continente.|  
|*País*|O atributo representa um país ou uma região.|  
|*Região*|O atributo representa uma região.|  
|*CurrencyDestination*|O atributo representa a moeda de destino ou um câmbio da moeda.|  
|*CurrencyISOcode*|O atributo representa o código ISO de uma moeda.|  
|*CurrencName*|O atributo representa o nome de uma moeda.|  
|*CurrencySource*|O atributo representa a moeda de origem de um câmbio monetário.|  
|*CustomerGroup*|O atributo representa um grupo de clientes.|  
|*CustomerHousehold*|O atributo representa uma casa de clientes.|  
|*Clientes*|O atributo representa um cliente.|  
|*Data*|O atributo representa uma data.|  
|*DateCanceled*|O atributo representa uma data de cancelamento.|  
|*DateDuration*|O atributo representa uma duração.|  
|*DateEnded*|O atributo representa uma data de término.|  
|*DateModified*|O atributo representa uma data de modificação.|  
|*Propriedade DateStart*|O atributo representa uma data de início.|  
|*DayOfHalfYears*|O atributo representa o ordinal de dia de um semestre.|  
|*DayOfMonth*|O atributo representa o ordinal de dia de um mês.|  
|*DayOfQuarter*|O atributo representa o ordinal de dia de um trimestre.|  
|*DayOfTrimester*|O atributo representa o ordinal de dia de um quadrimestre.|  
|*DayOfWeek*|O atributo representa o ordinal de dia de uma semana.|  
|*DayOfYear*|O atributo representa o ordinal de dia de um ano.|  
|*Dias*|O atributo representa dias.|  
|*DaysOfTenDays*|O atributo representa o ordinal de dia de um período de dez dias.|  
|*FiscalDay*|O atributo representa dias em um calendário fiscal.|  
|*FiscalDayOfHalfYears*|O atributo representa o ordinal de dia de um semestre em um calendário fiscal.|  
|*FiscalDayOfMonth*|O atributo representa o ordinal de dia de um mês em um calendário fiscal.|  
|*FiscalDayOfQuarter*|O atributo representa o ordinal de dia de um trimestre em um calendário fiscal.|  
|*FiscalDayOfTrimester*|O atributo representa o ordinal de dia de um quadrimestre em um calendário fiscal.|  
|*FiscalDayOfWeek*|O atributo representa o ordinal de dia de uma semana em um calendário fiscal.|  
|*FiscalDayOfYear*|O atributo representa o ordinal de dia de um ano em um calendário fiscal.|  
|*FiscalHalfYears*|O atributo representa semestres em um calendário fiscal.|  
|*FiscalHalfYearsOfYear*|O atributo representa o ordinal de semestre de um ano em um calendário fiscal.|  
|*Mês*|O atributo representa meses em um calendário fiscal.|  
|*FiscalMonthOfHalfYears*|O atributo representa o ordinal de mês de um semestre em um calendário fiscal.|  
|*FiscalMonthOfQuarter*|O atributo representa o ordinal de mês de um trimestre em um calendário fiscal.|  
|*FiscalMonthOfTrimester*|O atributo representa o ordinal de mês de um quadrimestre em um calendário fiscal.|  
|*FiscalMonthOfYear*|O atributo representa o ordinal de mês de um ano em um calendário fiscal.|  
|*FiscalQuarter*|O atributo representa trimestres em um calendário fiscal.|  
|*FiscalQuarterOfHalfYear*|O atributo representa o ordinal de trimestre de um semestre em um calendário fiscal.|  
|*FiscalQuarterOfYear*|O atributo representa o ordinal de trimestre de um ano em um calendário fiscal.|  
|*FiscalTrimester*|O atributo representa quadrimestres em um calendário fiscal.|  
|*FiscalTrimesterOfYear*|O atributo representa o ordinal de quadrimestre de um ano em um calendário fiscal.|  
|*FiscalWeek*|O atributo representa semanas em um calendário fiscal.|  
|*FiscalWeekOfHalfYears*|O atributo representa o ordinal de semana de um semestre em um calendário fiscal.|  
|*FiscalWeekOfMonth*|O atributo representa o ordinal de semana de um mês em um calendário fiscal.|  
|*FiscalWeekOfQuarter*|O atributo representa o ordinal de semana de um trimestre em um calendário fiscal.|  
|*FiscalWeekOfTrimester*|O atributo representa o ordinal de semana de um quadrimestre em um calendário fiscal.|  
|*FiscalWeekOfYear*|O atributo representa o ordinal de semana de um ano em um calendário fiscal.|  
|*FiscalYear*|O atributo representa anos em um calendário fiscal.|  
|*FormattingColor*|O atributo representa a cor usada na formatação.|  
|*FormattingFont*|O atributo representa a fonte usada na formatação.|  
|*FormattingFontEffects*|O atributo representa os efeitos de fonte usados na formatação.|  
|*FormattingFontSize*|O atributo representa o tamanho de fonte usado na formatação.|  
|*FormattingOrder*|O atributo representa a ordem usada na formatação.|  
|*FormattingSubtotal*|O atributo representa um subtotal.|  
|*GeoBoundaryBottom*|O atributo representa o valor mais baixo de um limite geográfico.|  
|*GeoBoundaryFront*|O atributo representa o valor mais à frente de um limite geográfico.|  
|*GeoBoundaryLeft*|O atributo representa o valor mais à esquerda de um limite geográfico.|  
|*GeoBoundaryPolygon*|O atributo representa a definição de polígono de um limite geográfico.|  
|*GeoBoundaryRear*|O atributo representa o último valor de um limite geográfico.|  
|*GeoBoundaryRight*|O atributo representa o valor mais à direita de um limite geográfico.|  
|*GeoBoundaryTop*|O atributo representa o valor mais alto de um limite geográfico.|  
|*GeoCentroidX*|O atributo representa um centroide do eixo X de uma região geográfica.|  
|*GeoCentroidY*|O atributo representa um centroide do eixo Y de uma região geográfica.|  
|*GeoCentroidZ*|O atributo representa um centroide do eixo Z de uma região geográfica.|  
|*HalfYears*|O atributo representa semestres.|  
|*HalfYearsOfYear*|O atributo representa o ordinal de semestre de um ano.|  
|*Horas*|O atributo representa horas.|  
|*ID*|O atributo representa um identificador ou chave.|  
|*IsHoliday*|O atributo indica se uma data é um feriado.|  
|*ISO8601DayOfWeek*|O atributo representa o ordinal de dia de uma semana em um calendário ISO 8601.|  
|*ISO8601DayOfYear*|O atributo representa o ordinal de dia de um ano em um calendário ISO 8601.|  
|*ISO8601Days*|O atributo representa dias em um calendário ISO 8601.|  
|*ISO8601Week*|O atributo representa semanas em um calendário ISO 8601.|  
|*ISO8601WeekOfYear*|O atributo representa o ordinal de semana de um ano em um calendário ISO 8601.|  
|*ISO8601Year*|O atributo representa anos em um calendário ISO 8601.|  
|*IsWeekDay*|O atributo indica se uma data é um fim de semana.|  
|*IsWorkingDay*|O atributo indica se uma data é um dia útil.|  
|*ManufacturingDay*|O atributo representa dias em um calendário de produção.|  
|*ManufacturingDayOfHalfYears*|O atributo representa o ordinal de dia de um semestre em um calendário de produção.|  
|*ManufacturingDayOfMonth*|O atributo representa o ordinal de dia de um mês em um calendário de produção.|  
|*ManufacturingDayOfQuarter*|O atributo representa o ordinal de dia de um trimestre em um calendário de produção.|  
|*ManufacturingDayOfTrimester*|O atributo representa o ordinal de dia de um quadrimestre em um calendário de produção.|  
|*ManufacturingDayOfWeek*|O atributo representa o ordinal de dia de uma semana em um calendário de produção.|  
|*ManufacturingDayOfYear*|O atributo representa o ordinal de dia de um ano em um calendário de produção.|  
|*ManufacturingHalfYears*|O atributo representa semestres em um calendário de produção.|  
|*ManufacturingHalfYearsOfYear*|O atributo representa o ordinal de semestre de um ano em um calendário de produção.|  
|*ManufacturingMonth*|O atributo representa meses em um calendário de produção.|  
|*ManufacturingMonthOfHalfYears*|O atributo representa o ordinal de mês de um semestre em um calendário de produção.|  
|*ManufacturingMonthOfQuarter*|O atributo representa o ordinal de mês de um trimestre em um calendário de produção.|  
|*ManufacturingMonthOfTrimester*|O atributo representa o ordinal de mês de um quadrimestre em um calendário de produção.|  
|*ManufacturingMonthOfYear*|O atributo representa o ordinal de mês de um ano em um calendário de produção.|  
|*ManufacturingQuarter*|O atributo representa trimestres em um calendário de produção.|  
|*ManufacturingQuarterOfHalfYear*|O atributo representa o ordinal de trimestre de um semestre em um calendário de produção.|  
|*ManufacturingQuarterOfYear*|O atributo representa o ordinal de trimestre de um ano em um calendário de produção.|  
|*ManufacturingTrimester*|O atributo representa quadrimestres em um calendário de produção.|  
|*ManufacturingTrimesterOfYear*|O atributo representa o ordinal de quadrimestre de um ano em um calendário de produção.|  
|*ManufacturingWeek*|O atributo representa semanas em um calendário de produção.|  
|*ManufacturingWeekOfHalfYears*|O atributo representa o ordinal de semana de um semestre em um calendário de produção.|  
|*ManufacturingWeekOfMonth*|O atributo representa o ordinal de semana de um mês em um calendário de produção.|  
|*ManufacturingWeekOfQuarter*|O atributo representa o ordinal de semana de um trimestre em um calendário de produção.|  
|*ManufacturingWeekOfTrimester*|O atributo representa o ordinal de semana de um quadrimestre em um calendário de produção.|  
|*ManufacturingWeekOfYear*|O atributo representa o ordinal de semana de um ano em um calendário de produção.|  
|*ManufacturingYear*|O atributo representa anos em um calendário de produção.|  
|*Minutes (minutos) (minutos)*|O atributo representa minutos.|  
|*MonthOfHalfYears*|O atributo representa o ordinal de mês de um semestre.|  
|*MonthOfQuarter*|O atributo representa o ordinal de mês de um trimestre.|  
|*MonthOfTrimester*|O atributo representa o ordinal de mês de um quadrimestre.|  
|*MonthOfYear*|O atributo representa o ordinal de mês de um ano.|  
|*Meses*|O atributo representa meses.|  
|*OrganizationalUnit*|O atributo representa uma unidade organizacional.|  
|*OrgTitle*|O atributo representa um cargo organizacional.|  
|*PercentOwnership*|O atributo representa uma porcentagem da propriedade.|  
|*PercentVoteRight*|O atributo representa uma porcentagem dos direitos de voto.|  
|*Pessoa*|O atributo representa uma pessoa.|  
|*PersonContact*|O atributo representa as informações de contado de uma pessoa.|  
|*PersonDemographic*|O atributo representa as informações demográficas de uma pessoa.|  
|*PersonFirstName*|O atributo representa o nome de uma pessoa.|  
|*PersonFullName*|O atributo representa o nome completo de uma pessoa.|  
|*PersonLastName*|O atributo representa o sobrenome de uma pessoa.|  
|*PersonMiddleName*|O atributo representa o nome do meio de uma pessoa.|  
|*PhysicalColor*|O atributo representa uma cor.|  
|*PhysicalDensity*|O atributo representa densidade.|  
|*PhysicalDepth*|O atributo representa profundidade.|  
|*PhysicalHeight*|O atributo representa altura.|  
|*PhysicalSize*|O atributo representa um tamanho.|  
|*PhysicalVolume*|O atributo representa volume.|  
|*PhysicalWeight*|O atributo representa peso.|  
|*PhysicalWidth*|O atributo representa largura.|  
|*Ponto*|O atributo representa um ponto.|  
|*CEP*|O atributo representa um CEP.|  
|*Product*|O atributo representa um produto.|  
|*ProductBrand*|O atributo representa a marca de um produto.|  
|*ProductCategory*|O atributo representa a categoria de um produto.|  
|*ProductGroup*|O atributo representa o grupo de um produto.|  
|*ProductSKU*|O atributo representa uma unidade de manutenção de estoque de produto (SKU, Stock Keeping Unit).|  
|*ProjectCode*|O atributo representa um código de projeto.|  
|*Projectcompletion*|O atributo representa o estado de conclusão de um projeto.|  
|*ProjectEnddate*|O atributo representa a data de término de um projeto.|  
|*ProjectName*|O atributo representa o nome de um projeto.|  
|*ProjectStartDate*|O atributo representa a data de início de um projeto.|  
|*Promoção*|O atributo representa uma promoção.|  
|*QtyRangeHigh*|O atributo representa o valor mais alto de um intervalo de quantidades.|  
|*QtyRangeLow*|O atributo representa o valor mais baixo de um intervalo de quantidades.|  
|*Quantitativa*|O atributo representa um atributo quantitativo.|  
|*QuarterOfHalfYear*|O atributo representa o ordinal de trimestre de um semestre.|  
|*QuarterOfYear*|O atributo representa o ordinal de trimestre de um ano.|  
|*Trimestres*|O atributo representa trimestres.|  
|*Taxa*|O atributo representa uma taxa.|  
|*RateType*|O atributo representa um tipo de taxa.|  
|*Região*|O atributo representa uma região definida pelo cliente.|  
|*Regular*|O atributo representa um atributo regular.|  
|*RelationToParent*|O atributo representa uma relação a um pai.|  
|*ReportingDay*|O atributo representa dias em um calendário de relatório.|  
|*ReportingDayOfHalfYears*|O atributo representa o ordinal de dia de um semestre em um calendário de relatório.|  
|*ReportingDayOfMonth*|O atributo representa o ordinal de dia de um mês em um calendário de relatório.|  
|*ReportingDayOfQuarter*|O atributo representa o ordinal de dia de um trimestre em um calendário de relatório.|  
|*ReportingDayOfTrimester*|O atributo representa o ordinal de dia de um quadrimestre em um calendário de relatório.|  
|*ReportingDayOfWeek*|O atributo representa o ordinal de dia de uma semana em um calendário de relatório.|  
|*ReportingDayOfYear*|O atributo representa o ordinal de dia de um ano em um calendário de relatório.|  
|*ReportingHalfYears*|O atributo representa semestres em um calendário de relatório.|  
|*ReportingHalfYearsOfYear*|O atributo representa o ordinal de semestre de um ano em um calendário de relatório.|  
|*ReportingMonth*|O atributo representa meses em um calendário de relatório.|  
|*ReportingMonthOfHalfYears*|O atributo representa o ordinal de mês de um semestre em um calendário de relatório.|  
|*ReportingMonthOfQuarter*|O atributo representa o ordinal de mês de um trimestre em um calendário de relatório.|  
|*ReportingMonthOfTrimester*|O atributo representa o ordinal de mês de um quadrimestre em um calendário de relatório.|  
|*ReportingMonthOfYear*|O atributo representa o ordinal de mês de um ano em um calendário de relatório.|  
|*ReportingQuarter*|O atributo representa trimestres em um calendário de relatório.|  
|*ReportingQuarterOfHalfYear*|O atributo representa o ordinal de trimestre de um semestre em um calendário de relatório.|  
|*ReportingQuarterOfYear*|O atributo representa o ordinal de trimestre de um ano em um calendário de relatório.|  
|*ReportingTrimester*|O atributo representa quadrimestres em um calendário de relatório.|  
|*ReportingTrimesterOfYear*|O atributo representa o ordinal de quadrimestre de um ano em um calendário de relatório.|  
|*ReportingWeek*|O atributo representa semanas em um calendário de relatório.|  
|*ReportingWeekOfHalfYears*|O atributo representa o ordinal de semana de um semestre em um calendário de relatório.|  
|*ReportingWeekOfMonth*|O atributo representa o ordinal de semana de um mês em um calendário de relatório.|  
|*ReportingWeekOfQuarter*|O atributo representa o ordinal de semana de um trimestre em um calendário de relatório.|  
|*ReportingWeekOfTrimester*|O atributo representa o ordinal de semana de um quadrimestre em um calendário de relatório.|  
|*ReportingWeekOfYear*|O atributo representa o ordinal de semana de um ano em um calendário de relatório.|  
|*ReportingYear*|O atributo representa anos em um calendário de relatório.|  
|*Representante*|O atributo representa um representante.|  
|*Cenário*|O atributo representa um cenário.|  
|*Seconds (segundos) (segundos)*|O atributo representa segundos.|  
|*Sequência*|O atributo representa um atributo de sequência.|  
|*ShortCaption*|O atributo representa uma legenda curta.|  
|*StateOrProvince*|O atributo representa um estado.|  
|*TenDayOfHalfYears*|O atributo representa o ordinal de período de dez dias de um semestre.|  
|*TenDayOfQuarter*|O atributo representa o ordinal de período de dez dias de um trimestre.|  
|*TenDayOfTrimester*|O atributo representa o ordinal de período de dez dias de um quadrimestre.|  
|*TenDayOfYear*|O atributo representa o ordinal de período de dez dias de um ano.|  
|*TenDays*|O atributo representa períodos de dez dias.|  
|*TenDaysOfMonth*|O atributo representa o ordinal de período de dez dias de um mês.|  
|*Quadrimestre*|O atributo representa quadrimestres.|  
|*TrimesterOfYear*|O atributo representa o ordinal de quadrimestre de um ano.|  
|*UndefinedTime*|O atributo representa um período de tempo indefinido.|  
|*Utilitário*|O atributo representa um utilitário.|  
|*Versão*|O atributo representa uma versão.|  
|*WebHtml*|O atributo representa um conteúdo HTML.|  
|*WebMailAlias*|O atributo representa um alias de email.|  
|*WebUrl*|O atributo representa uma URL.|  
|*WebXmlOrXsl*|O atributo representa conteúdo XML ou XSL.|  
|*WeekOfHalfYears*|O atributo representa o ordinal de semana de um semestre.|  
|*WeekOfMonth*|O atributo representa o ordinal de semana de um mês.|  
|*WeekOfQuarter*|O atributo representa o ordinal de semana de um trimestre.|  
|*WeekOfTrimester*|O atributo representa o ordinal de semana de um quadrimestre.|  
|*WeekOfYear*|O atributo representa o ordinal de semana de um ano.|  
|*Semanas*|O atributo representa semanas.|  
|*Anos*|O atributo representa anos.|  
  
 A enumeração que corresponde aos valores permitidos para **tipo** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.AttributeType>.  
  
 O elemento que corresponde ao pai do **tipo** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos de elemento &#40; ASSL &#41;](../../../analysis-services/scripting/collections/attributes-element-assl.md)   
 [Elemento Dimension &#40; ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

