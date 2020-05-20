---
title: Elemento de esquema para banco de dados (DTA)
description: No utilitário dta, o elemento Schema para Database especifica o esquema do banco de dados que você deseja ajustar.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Schema element
ms.assetid: d932e59c-953f-4ab4-934d-b6baf344835c
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: ee28954c4206e2e26edfa567bae5a1b282d41dea
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83151820"
---
# <a name="schema-element-for-database-dta"></a>Elemento de esquema para banco de dados (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Especifica o esquema do banco de dados que você deseja ajustar.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Database>  
...code removed here...  
    <Schema>...</Schema>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Exigido uma vez para o elemento do **Banco de Dados** especificado no elemento **Servidor** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Database para Server &#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md)|  
|**Elementos filho**|[Elemento Name para Schema &#40;DTA&#41;](../../tools/dta/name-element-for-schema-dta.md)<br /><br /> [Elemento Table para Schema &#40;DTA&#41;](../../tools/dta/table-element-for-schema-dta.md)|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, consulte [Elemento Server &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
