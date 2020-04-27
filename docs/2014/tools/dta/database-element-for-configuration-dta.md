---
title: Elemento de banco de dados para configuração (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fbca62a5d32ed6b7ec30eb5d6dba6a82a2b80c64
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63298348"
---
# <a name="database-element-for-configuration-dta"></a>Elemento de banco de dados para configuração (DTA)
  Especifica o banco de dados em relação ao qual você deseja que o Orientador de Otimização do Mecanismo de Banco de Dados avalie a configuração hipotética (especificada pelo elemento`Configuration` ).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|DESCRIÇÃO|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Exigido uma ou mais vezes por elemento `Server`.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Server para Configuration &#40;DTA&#41;](server-element-for-configuration-dta.md)|  
|**Elementos filho**|[Elemento Name para Database &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [Elemento Schema para Database &#40;DTA&#41;](schema-element-for-database-dta.md)<br /><br /> [Elemento Recommendation &#40;DTA&#41;](recommendation-element-dta.md)|  
  
## <a name="remarks"></a>Comentários  
 Esse elemento tem o nome **DatabaseTypecomplexType** no esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. Não confunda esse elemento `Database` com o elemento cujo pai raiz é o elemento `Server` que ocorre no topo do arquivo de entrada XML. Para obter mais informações, veja [Elemento Database para servidor &#40;DTA&#41;](database-element-for-server-dta.md).  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso `Database` desse elemento, consulte a [amostra do arquivo de entrada XML com a configuração especificada pelo usuário &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
