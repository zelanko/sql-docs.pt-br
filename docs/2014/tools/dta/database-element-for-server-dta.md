---
title: Elemento de banco de dados do servidor (DTA) | Microsoft Docs
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
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9aaf9d744ad51a6d59a3c69b1f5a30fe77a59edc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153497"
---
# <a name="database-element-for-server-dta"></a>Elemento de banco de dados para servidor (DTA)
  Especifica o banco de dados que deseja ajustar em um servidor específico.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum.|  
|Valor padrão|Nenhuma.|  
|Ocorrência|Exigido uma ou mais vezes por `Server` elemento.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|Elemento pai|[Elemento de servidor &#40;DTA&#41;](server-element-dta.md)|  
|Elementos filho|[Nome de elemento para o banco de dados &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [Elemento de esquema para o banco de dados &#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 Esse elemento tem o nome **DatabaseDetailsTypecomplexType** no Esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. Não confunda este elemento do `Database` com aquele cujo pai raiz é o elemento `Configuration`. Para obter mais informações, veja [Elemento Database para configuração &#40;DTA&#41;](database-element-for-configuration-dta.md).  
  
## <a name="example"></a>Exemplo  
 Para um exemplo de uso de `Database` elemento, consulte [elemento de servidor &#40;DTA&#41;](server-element-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
