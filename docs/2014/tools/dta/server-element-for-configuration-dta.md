---
title: Elemento Server para configuração (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2bc763d621d15f982a2670483683d3862e678c98
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63283682"
---
# <a name="server-element-for-configuration-dta"></a>Elemento de servidor para configuração (DTA)
  Contém as informações de identificação para o servidor onde você quer que o Orientador de Otimização do Mecanismo de Banco de Dados avalie uma configuração hipotética (especificada pelo elemento `Configuration` ).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Obrigatório uma vez por elemento `Configuration`.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Configuration &#40;DTA&#41;](configuration-element-dta.md)|  
|**Elementos filho**|[Elemento Name para Server &#40;DTA&#41;](name-element-for-server-dta.md)<br /><br /> [Elemento Database para Configuration &#40;DTA&#41;](database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>Comentários  
 Você pode especificar apenas um `Server` elemento para o `Configuration` elemento. Esse elemento tem o nome **ServerTypecomplexType** no [Esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados](https://go.microsoft.com/fwlink/?linkid=43100). Não confunda esse elemento `Server` com aquele que é o filho do elemento `DTAInput`. Para obter mais informações, consulte [Elemento de servidor &#40;DTA&#41;](server-element-dta.md).  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso, consulte a [Amostra de arquivo de entrada XML com a configuração especificada pelo usuário &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
