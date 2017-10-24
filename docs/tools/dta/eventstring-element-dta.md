---
title: Elemento EventString (DTA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- EventString element
ms.assetid: f76c37b4-2f6e-4274-8ee2-87e89d98e8a2
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 85e5c89f87a0a6eda0173511f818e047fc0c51c9
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

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
  
|Atributo|Descrição|  
|---------------|-----------------|  
|**Weight**|Opcional. Especifica o fator de peso da consulta (um fator de importância) para o evento especificado. Use um tipo de dados **float** para especificar o peso. Por exemplo, **Peso**= "100,01". O valor mínimo que você pode especificar para **Weight** é "0."|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, tamanho é ilimitado.|  
|**Valor padrão**|Nenhuma.|  
|**Ocorrência**|Exigido uma vez se não houver outro tipo de carga de trabalho especificada. É preciso especificar um elemento filho **EventString**, **File**ou **Database** para o pai **Workload** , mas só pode ser usado um tipo. Por exemplo, se for especificada uma carga de trabalho com o elemento **EventString** , não será possível especificar uma carga de trabalho com o elemento **File** no mesmo arquivo de entrada XML.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Workload &#40; DTA &#41;](../../tools/dta/workload-element-dta.md)|  
|**Elementos filho**|Nenhuma.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso deste elemento, consulte [Amostra do arquivo de entrada XML com carga de trabalho embutida &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

