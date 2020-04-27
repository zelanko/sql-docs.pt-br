---
title: Elemento EventString (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- EventString element
ms.assetid: f76c37b4-2f6e-4274-8ee2-87e89d98e8a2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30e46515fda5bf03a96e9f1168b470f635698d07
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211112"
---
# <a name="eventstring-element-dta"></a>Elemento EventString (DTA)
  Especifica uma carga de trabalho de script do [!INCLUDE[tsql](../../includes/tsql-md.md)] diretamente no arquivo de entrada XML.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Workload>  
    <EventString Weight="...">  
    ...code removed here...  
    </EventString>  
</Workload>  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|Atributo|DESCRIÇÃO|  
|---------------|-----------------|  
|`Weight`|Opcional. Especifica o fator de peso da consulta (um fator de importância) para o evento especificado. Use um tipo de dados `float` para especificar o peso. Por exemplo, `Weight`="100.01". O valor mínimo que você pode especificar para `Weight` é "0."|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Tipo de dados e comprimento**|`string`, tamanho é ilimitado.|  
|**Valor padrão**|Nenhum.|  
|**C'**|Exigido uma vez se não houver outro tipo de carga de trabalho especificada. É preciso especificar um elemento filho `EventString`, `File` ou  `Database` para o pai `Workload`, mas só pode ser usado um tipo. Por exemplo, se for especificada uma carga de trabalho com o elemento `EventString`, não será possível especificar uma carga de trabalho com o elemento `File` no mesmo arquivo de entrada XML.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Workload &#40;DTA&#41;](workload-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso deste elemento, consulte [Amostra do arquivo de entrada XML com carga de trabalho embutida &#40;DTA&#41;](xml-input-file-sample-with-inline-workload-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
