---
title: Elemento Server para configuração (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10a8fa9eed7f89d9706ab3388eccc881b165ef74
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48206906"
---
# <a name="server-element-for-configuration-dta"></a>Elemento de servidor para configuração (DTA)
  Contém as informações de identificação para o servidor onde você deseja que o orientador de otimização do mecanismo de banco de dados para avaliar a configuração hipotética (especificada pelo `Configuration` elemento).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Obrigatório uma vez por `Configuration` elemento.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento de configuração &#40;DTA&#41;](configuration-element-dta.md)|  
|**Elementos filho**|[Nome de elemento para o servidor &#40;DTA&#41;](name-element-for-server-dta.md)<br /><br /> [Elemento de banco de dados para a configuração &#40;DTA&#41;](database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>Comentários  
 Você pode especificar apenas um `Server` elemento para o `Configuration` elemento. Esse elemento tem o nome **ServerTypecomplexType** no [Esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados](http://go.microsoft.com/fwlink/?linkid=43100). Não confunda esse `Server` elemento com aquele que é o filho do `DTAInput` elemento. Para obter mais informações, consulte [Elemento de servidor &#40;DTA&#41;](server-element-dta.md).  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso, consulte a [Amostra de arquivo de entrada XML com a configuração especificada pelo usuário &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
