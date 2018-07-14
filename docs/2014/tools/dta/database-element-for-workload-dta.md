---
title: Elemento de banco de dados para carga de trabalho (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 112fca2a-37e5-4162-b2e7-b56eb8ab0c6f
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 085af567ae906835b33942a57e0590c9296f5198
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257612"
---
# <a name="database-element-for-workload-dta"></a>Elemento de banco de dados para carga de trabalho (DTA)
  Especifica o banco de dados em que se encontra a tabela de rastreamento da carga de trabalho.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Workload>  
  <Database>  
   ...code removed here...  
  </Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Exigido uma vez se não houver outro tipo de carga de trabalho especificada. Você deve especificar um `EventString`, um `File`, ou uma `Database` elemento filho para o `Workload` pai, mas apenas um tipo pode ser usado. Por exemplo, se uma carga de trabalho com o elemento `Database` for especificada, não será possível especificar uma carga de trabalho com o elemento `File` no mesmo arquivo XML de entrada.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento de carga de trabalho &#40;DTA&#41;](workload-element-dta.md)|  
|**Elementos filho**|[Nome de elemento para o banco de dados &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [Elemento de esquema para o banco de dados &#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 Esse elemento tem o nome **DatabaseDetailsTypecomplexType** no Esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. Não confunda este elemento do `Database` com aquele cujo pai raiz é o elemento `Configuration`. (Consulte [Elemento Database para Configuration &#40;DTA&#41;](database-element-for-configuration-dta.md).)  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso deste `Database` elemento, consulte o exemplo de código na [elemento de carga de trabalho &#40;DTA&#41;](workload-element-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
