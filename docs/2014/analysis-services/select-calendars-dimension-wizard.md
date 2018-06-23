---
title: Selecionar calendários (Assistente para dimensões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dimensionwizard.serverSpecialCalendars.f1
ms.assetid: 6e28a020-2586-4b13-9333-b499fb1b33af
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6796c7c3064adc65982b1d5aaec005249e224cae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012084"
---
# <a name="select-calendars-dimension-wizard"></a>Selecionar Calendários (Assistente para Dimensões)
  Use a página **Selecionar Calendários** para criar hierarquias adicionais representando calendários fiscais, de relatório, de fabricação ou ISO 8601 para a dimensão de tempo.  
  
> [!NOTE]  
>  Essa página será exibida apenas se você tiver selecionado **Dimensão de tempo de servidor** na página **Selecionar o Tipo de Dimensão** ou se você tiver selecionado **Criar a dimensão sem usar uma fonte de dados** na página **Definição de Dimensão** e **Dimensão de tempo** na página **Selecionar o tipo de dimensão** .  
  
## <a name="options"></a>Opções  
 **Calendário fiscal**  
 Selecione para criar uma hierarquia de tempo baseada em um calendário fiscal.  
  
 **Dia e mês de início**  
 Selecione o dia e o mês em que o calendário fiscal é iniciado.  
  
> [!NOTE]  
>  Essa opção está disponível apenas quando **Calendário fiscal** está selecionado.  
  
 **Convenção de nomenclatura do calendário fiscal**  
 Selecione a convenção de nomenclatura usada pelo calendário fiscal. Selecione **Nome do ano civil** ou **Nome do ano civil +1**.  
  
> [!NOTE]  
>  Essa opção está disponível apenas quando **Calendário fiscal** está selecionado.  
  
 **Calendário de relatório (ou marketing)**  
 Selecione para criar uma hierarquia de tempo baseada em um calendário de relatório.  
  
 **Semana e mês de início**  
 Selecione a semana e o mês em que o calendário de relatório é iniciado.  
  
> [!NOTE]  
>  Essa opção está disponível quando **Calendário de relatório (ou marketing)** está selecionado.  
  
 **Semana por padrão mensal**  
 Selecione a semana por padrão mensal usada pelo calendário de relatório.  
  
> [!NOTE]  
>  Essa opção está disponível quando **Calendário de relatório (ou marketing)** está selecionado.  
  
 A tabela a seguir lista as opções disponíveis para a semana por padrão mensal.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Semana 445**|O primeiro mês do trimestre tem 4 semanas, o segundo mês do trimestre tem 4 semanas e o terceiro mês do trimestre tem 5 semanas.|  
|**Semana 454**|O primeiro mês do trimestre tem 4 semanas, o segundo mês do trimestre tem 5 semanas e o terceiro mês do trimestre tem 4 semanas.|  
|**Semana 544**|O primeiro mês do trimestre tem 5 semanas, o segundo mês tem 4 semanas e o terceiro mês tem 4 semanas.|  
  
 **Calendário de produção**  
 Selecione para criar uma hierarquia de tempo baseada em um calendário de produção.  
  
 **Semana e mês de início**  
 Selecione a semana e o mês em que o calendário de produção é iniciado.  
  
> [!NOTE]  
>  Essa opção está disponível apenas quando **Calendário de produção** está selecionado.  
  
 **Trimestre com períodos extras**  
 Selecione ou digite o trimestre que conterá os períodos extras.  
  
> [!NOTE]  
>  Essa opção está disponível apenas quando **Calendário de produção** está selecionado.  
  
 **Calendário ISO 8601**  
 Selecione para criar uma hierarquia de tempo baseada no calendário ISO 8601.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda de F1 do Assistente de dimensão](dimension-wizard-f1-help.md)   
 [Dimensões &#40;Analysis Services - dados multidimensionais&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensões em modelos multidimensionais](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  