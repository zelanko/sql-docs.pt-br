---
title: Nome de elemento para esquema (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Name element
ms.assetid: 014e4854-fed2-454b-8557-5f7c5bb6b17a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b28505c0a950339a8a65eb018df770fcba8a7118
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51292502"
---
# <a name="name-element-for-schema-dta"></a>Elemento nome para esquema (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Contém o nome do esquema.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Database>  
...code removed here  
    <Schema>  
        <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, entre 1 e 255 caracteres.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Necessário uma vez por elemento de **Esquema** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Schema para Database &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, consulte [Elemento Server &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
