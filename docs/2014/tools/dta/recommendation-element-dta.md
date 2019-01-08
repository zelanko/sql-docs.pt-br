---
title: Elemento de recomendação (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Recommendation element
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bcc0a95028b1f107f15752692d3dcad090fbe8b1
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356749"
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Pode ser usado uma vez para cada elemento `Table`.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Table para Schema &#40;DTA&#41;](table-element-for-schema-dta.md)|  
|**Elementos filho**|[Elemento Create &#40;DTA&#41;](create-element-dta.md)<br /><br /> Elemento `Drop`. Para obter mais informações, consulte o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](https://go.microsoft.com/fwlink/?linkid=43100).|  
  
## <a name="remarks"></a>Comentários  
 Esse elemento tem o nome **RecommendationTypecomplexType** no esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. É usado para especificar os índices de uma configuração hipotética. Não confunda esse elemento `Recommendation` com os outros tipos que podem ser usados para especificar particionamento (`RecommendationPType`) ou exibições (`RecommendationViewType`). Para obter informações sobre esses outros `Recommendation` tipos de elemento, consulte a [esquema XML do Orientador de otimização de mecanismo de banco de dados](https://go.microsoft.com/fwlink/?linkid=43100).  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivo de entrada XML com configuração especificada pelo usuário (DTA)](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
