---
title: Elemento de banco de dados para a carga de trabalho (DTA) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
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
- Database element
ms.assetid: 112fca2a-37e5-4162-b2e7-b56eb8ab0c6f
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e71d9a3077821fc4b34ee5cebac5441065ddf013
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhuma.|  
|**Valor padrão**|Nenhuma.|  
|**Ocorrência**|Exigido uma vez se não houver outro tipo de carga de trabalho especificada. É preciso especificar um elemento filho **EventString**, **File**ou **Database** para o pai **Workload** , mas só pode ser usado um tipo. Por exemplo, se uma carga de trabalho com o elemento **Database** for especificada, não será possível especificar uma carga de trabalho com o elemento **File** no mesmo arquivo de entrada XML.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Workload &#40; DTA &#41;](../../tools/dta/workload-element-dta.md)|  
|**Elementos filho**|[Elemento de nome de banco de dados &#40; DTA &#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Elemento Schema para Database &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Comentários  
 Esse elemento tem o nome **DatabaseDetailsTypecomplexType** no Esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. Não confunda este elemento **Database** com aquele cujo pai raiz é o elemento **Configuration**. (Consulte [Elemento Database para Configuration &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md).)  
  
## <a name="example"></a>Exemplo  
 Para exemplo de uso desse elemento **Database** , consulte o exemplo de código em [Elemento Workload &#40;DTA&#41;](../../tools/dta/workload-element-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

