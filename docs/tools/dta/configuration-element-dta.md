---
title: "O elemento de configuração (DTA) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Configuration element
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 84a9a5596e7bf4fed05820f3cae387b52005e84e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="configuration-element-dta"></a>Elemento de configuração (DTA)
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
|**Comprimento e tipo de dados**|Nenhuma.|  
|**Valor padrão**|Nenhuma.|  
|**Ocorrência**|Opcional. Pode ser usado uma vez para cada elemento **DTAInput** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento DTAInput &#40; DTA &#41;](../../tools/dta/dtainput-element-dta.md)|  
|**Elementos filho**|[Elemento Server para Configuration &#40; DTA &#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivo de entrada XML com configuração especificada pelo usuário (DTA)](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

