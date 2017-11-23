---
title: "Atributos CSDLBI para Design de relatório | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 61ba3a27-790e-43bc-b421-e01bf2fdbda6
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cf0a6f94595778429b4ec850dac22757fc4a39e9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="csdlbi-attributes-for-report-design"></a>Atributos CSDLBI para design de relatórios

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  Esta seção descreve os atributos nas extensões de CSDL para modelagem de tabela que afeta o design de consulta [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
## <a name="model-attributes"></a>Atributos de Modelo  
 Estes atributos são definidos em um subelemento de um elemento [EntityContainer](http://msdn.microsoft.com/library/bb399169.aspx) de CSDL.  
  
|Nome do atributo|Tipo de dados|Descrição|  
|--------------------|---------------|-----------------|  
|Cultura|Texto|Indica a cultura usada para formatos de conversor de moedas. Se for omitido, pt-BR será usado.|  
|IsRightToLeft|Boolean|Indica se os valores de campos de texto devem ser lidos da direita para a esquerda por padrão|  
  
## <a name="entity-attributes"></a>Atributos da entidade  
 Estes atributos são definidos em um subelemento de um elemento EntitySet ou EntityType de CSDL.  
  
|Nome do atributo|Tipo de dados|Description|  
|--------------------|---------------|-----------------|  
|**Nome da referência**|Texto|O identificador usado para referenciar essa entidade em uma consulta DAX. Se for omitido, o nome será usado.|  
|**Caption**|Texto|O nome para exibição da entidade.|  
|**Documentação**|Texto|Texto descritivo para ajudar os usuários empresariais a compreenderem o significado dos dados.|  
|**Oculto**|Booliano|Indica se a entidade deve ser exibida. O padrão é **false**.|  
|**CollectionCaption**|Texto|Nome plural para referenciar um conjunto de instâncias da entidade. Se ele for omitido, o atributo Caption será usado.|  
|**DisplayKey**|MemberRef[]|Uma lista ordenada de campo(s) usada para identificar uma instância de entidade para um usuário empresarial. As referências podem incluir propriedades de instância e propriedades de navegação. Quando uma propriedade de navegação é referenciada, o **DisplayKey** da entidade de destino é exibido. Se o valor **DisplayKey** for omitido, o campo de chave será usado.|  
|**DefaultImage**|MemberRef|Uma referência ao campo que contém uma imagem usada para identificar visualmente uma instância de entidade para um usuário empresarial. Se for omitida, o primeiro campo de imagem na entidade será usado, caso exista.|  
|**DefaultDetails**|MemberRef[]|Uma lista ordenada de campos que representam o conjunto padrão de informações detalhadas exibidas para um usuário comercial sobre uma instância de entidade. Caso sejam omitidos, serão usados os primeiros cinco (5) campos na entidade, excluindo os já referenciados por **Key**, **DisplayKey**ou **DefaultImage**.|  
|**SortProperties**|MemberRef[]|Uma lista ordenada de campos através dos quais as instâncias de entidade costumam ser classificadas. Ao classificar nestes campos, o **SortDirection** especificado em cada campo é usado. Se ele for omitido, os campos **DisplayKey** serão usados|  
|**DefaultMeasure**|MemberRef|Uma referência a uma medida definida no modelo, ou a um campo numérico com uma função de agregação padrão, para indicar que a medida ou o campo dever ser usado como a representação padrão para várias instâncias da entidade. Se ela for omitida, uma contagem das instâncias de entidade será usada.|  
|**DefaultLocation**|MemberRef|Uma referência a um campo cujo valor representa a localização padrão associada a uma instância de entidade. Se ela for omitida, o primeiro campo de localização na entidade será usado, caso exista.|  
  
## <a name="field-attributes"></a>Atributos de campo  
 Estes atributos são definidos em um subelemento de uma propriedade CSDL ou elemento [NavigationProperty](http://msdn.microsoft.com/library/bb387104.aspx) .  
  
|Nome do atributo|Tipo de dados|Description|  
|--------------------|---------------|-----------------|  
|**Nome da referência**|Texto|O identificador usado para referenciar essa entidade em uma consulta DAX. Se ele for omitido, o nome do campo será usado.|  
|**Caption**|Texto|O nome para exibição da entidade. Se ele for omitido, o **ReferenceName** do campo será usado.|  
|**Documentação**|Texto|Texto descritivo para ajudar os usuários empresariais a compreenderem o significado do campo.|  
|**Oculto**|Booliano|Indica se o campo deve ser exibido. O padrão é **false**; isso significa que o campo é exibido.|  
|**DisplayFolder**|Texto|O nome (caminho completo) da pasta na qual este campo é exibido. Se ele for omitido, o campo será exibido na raiz do modelo.|  
|**ContextualNameRule**|Enum|Um valor que indica se e como o nome da propriedade deve ser modificado com base no contexto no qual é usado. Os valores possíveis são:  **None**,  **Role**,  **Merge**.|  
|**Alinhamento**|Enum|Um valor que indica como os valores de campos devem ser alinhados em uma apresentação de tabela. Os valores possíveis são **Default**, **Center**, **Left**, **Right**. Se ele for omitido, o padrão determina o alinhamento com base no tipo de dados do campo.|  
|**FormatString**|Texto|Uma cadeia de caracteres no formato .NET que indica como o valor do campo deve ser formatado por padrão. Se for omitida, o seguinte formato será assumido:<br /><br /> Campos - Datetime: data curta regional ou "d"<br /><br /> -Função de agregação de campos ponto flutuante e campos integrais com um padrão: número regional ou "n"<br /><br /> -Função de agregação inteiros sem nenhum padrão: número decimal regional ou "d"<br /><br /> Para todos os outros tipos de campos, nenhuma cadeia de caracteres de formato se aplica.|  
|**Unidades**|Texto|O símbolo que se aplica a valores de campos para expressar unidades. Se ele for omitido, as unidades são consideradas desconhecidas.|  
|**Largura**|Integer|A largura preferencial em caracteres que deve ser reservada para exibir os valores do campo em uma apresentação de tabela. Se ela for omitida, uma largura padrão se baseará no tipo de dados do campo.|  
|**SortDirection**|Enum|Um valor que indica como os valores de campos costumam ser classificados. Os valores possíveis são **Default**, **Ascending**, **Descending**. Se ele for omitido, o valor padrão atribuirá uma direção de classificação com base no tipo de dados do campo.|  
|**IsRightToLeft**|Booliano|Indica se o campo contém texto que deve ser lido da direita para a esquerda. Se ele for omitido, a configuração do modelo será assumida.|  
|**OrderBy**|MemberRef|Uma referência a outro campo dentro do modelo que define a ordem de classificação para os valores deste campo. Os valores para os dois campos devem ter um mapeamento 1:1 ou o comportamento de classificação será indefinido. Se ela for omitida, o campo será classificado com base em seu próprio valor.|  
|**Sumário**|Enum|Uma enumeração que descreve o subtipo ou o conteúdo do campo. Se ela for omitida, nenhum subtipo específico será assumido, a menos que o tipo de dados do campo seja Binary, caso em que Image será assumido. Para obter uma lista completa dos tipos de conteúdo com suporte, consulte a documentação de AMO.|  
|**DefaultAggregateFunction**|Enum|Um valor que indica a função padrão, caso exista, que costuma ser usada para agregar este campo. Os valores possíveis são **None**, **Sum**, **Average**, **Count**, **Min**, **Max**. Se ele for omitido, **Sum** será assumido para campos numéricos e **None** para todos os outros campos.|  
|**IsSimpleMeasure**|Booliano|Indica se uma medida é meramente uma agregação simples de um campo numérico. Estas agregações podem ser definidas facilmente na consulta quando necessário e, portanto, devem ser omitidas da definição modelo para melhorar o desempenho. Se ela for omitida, **false** será assumido.|  
|**KPI**<br /><br /> **KpiGoal**<br /><br /> **KpiStatus**|Subelemento|Indica que o elemento de medida será usado como um KPI. O subelemento de KPI usa os elementos KpiGoal e KpiStauts para definir a imagem de exibição associada e os intervalos de destino.|  
  
  
