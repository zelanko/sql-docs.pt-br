---
title: Elemento de configuração (DTA)
description: No utilitário dta, o elemento Configuration especifica uma configuração especificada pelo usuário que consiste em estruturas de design físico existentes e hipotéticas.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Configuration element
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 265b66ece4d4430f7d26763cbd72f24f528dd959
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831635"
---
# <a name="configuration-element-dta"></a>Elemento de configuração (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Determina uma configuração especificada pelo usuário, que consiste em estruturas existentes e hipotéticas de design físico do Orientador de Otimização do Mecanismo de Banco de Dados, para análise, quando uma carga de trabalho é analisada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
    <Server>...</Server>  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions  
    <Configuration [SpecificationMode="Relative" | "Absolute"]>  
    ...code removed here...  
    </Configuration>  
</DTAInput>  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|Atributo de configuração|Descrição|  
|-----------------------------|-----------------|  
|**SpecificationMode**|Opcional. Especifica se o Orientador de Otimização do Mecanismo de Banco de Dados deve analisar a configuração especificada em relação à configuração existente atual ou como configuração totalmente nova e autônoma. Use um tipo de dados de **cadeia de caracteres** para especificar esse atributo com um dos seguintes valores permitidos:<br /><br /> **Relative**:<br />                  Avalia a configuração especificada em relação à configuração existente atual das estruturas de design físicas (índices, exibições indexadas, particionamento) do banco de dados que está sendo ajustado. Por exemplo:<br /><br /> `<Configuration SpecificationMode="Relative">`<br /><br /> **Absolute**:<br />                  Avalia a configuração especificada como uma configuração autônoma. Quando Absolute é especificado, o Orientador de Otimização do Mecanismo de Banco de Dados não considera a configuração existente. Por exemplo:<br /><br /> `<Configuration SpecificationMode="Absolute">`|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Pode ser usado uma vez para cada elemento **DTAInput** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento DTAInput &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)|  
|**Elementos filho**|[Elemento Server para Configuration &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivo de entrada XML com configuração especificada pelo usuário (DTA)](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
