---
title: "Elemento de banco de dados de configuração (DTA) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Database element
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e65efde942a30cf6e173ad2558c0eb7899723d11
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="database-element-for-configuration-dta"></a>Elemento de banco de dados para configuração (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Especifica o banco de dados em relação ao qual você deseja que o orientador de otimização do mecanismo de banco de dados para avaliar a configuração hipotética (especificada pelo **configuração** elemento).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Exigido uma ou mais vezes por elemento **Server** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Server para Configuration &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
|**Elementos filho**|[Elemento Name para Database &#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Elemento Schema para Database &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)<br /><br /> [Elemento Recommendation &#40;DTA&#41;](../../tools/dta/recommendation-element-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 Esse elemento tem o nome **DatabaseTypecomplexType** no esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. Não confunda esse elemento **Database** com o elemento cujo pai raiz é o elemento **Server**, que ocorre na parte superior do arquivo de entrada XML. Para obter mais informações, veja [Elemento Database para servidor &#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md).  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento **Database**, veja a [Amostra de arquivo de entrada XML com a configuração especificada pelo usuário &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
