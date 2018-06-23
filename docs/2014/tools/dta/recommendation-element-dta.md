---
title: Elemento de recomendação (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Recommendation element
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 58535397a152ff1198cbb4cf713a6d0ec04a7eed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010146"
---
# <a name="recommendation-element-dta"></a>Elemento de recomendação (DTA)
  Contém informações sobre os índices hipotéticos que integram a configuração especificada pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Configuration>  
    ...code removed here...  
    <Table>  
      <Name>...</Name>  
      <Recommendation>  
      ...code removed here...  
      </Recommendation>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Pode usar uma vez para cada `Table` elemento.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento de tabela para esquema &#40;DTA&#41;](table-element-for-schema-dta.md)|  
|**Elementos filho**|[Criar elemento &#40;DTA&#41;](create-element-dta.md)<br /><br /> `Drop` Elemento. Para obter mais informações, consulte o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](http://go.microsoft.com/fwlink/?linkid=43100).|  
  
## <a name="remarks"></a>Remarks  
 Esse elemento tem o nome **RecommendationTypecomplexType** no esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. É usado para especificar os índices de uma configuração hipotética. Não confunda esse `Recommendation` elemento com os outros tipos que podem ser usados para especificar particionamento (`RecommendationPType`) ou modos de exibição (`RecommendationViewType`). Para obter informações sobre esses outros `Recommendation` tipos de elemento, consulte o [esquema XML do Orientador de otimização de mecanismo de banco de dados](http://go.microsoft.com/fwlink/?linkid=43100).  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivo de entrada XML com configuração especificada pelo usuário (DTA)](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  