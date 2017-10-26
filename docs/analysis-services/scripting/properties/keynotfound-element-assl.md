---
title: Elemento KeyNotFound (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- KeyNotFound Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- KeyNotFound
helpviewer_keywords:
- KeyNotFound element
ms.assetid: 2a93bbfa-2409-4e94-8b68-926532895a4c
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b193d4a9a7c87138287b28286a65e867430a0d36
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="keynotfound-element-assl"></a>Elemento KeyNotFound (ASSL)
  Especifica como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] responde quando encontra um erro de integridade referencial.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyNotFound>...</KeyNotFound>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*ReportAndContinue*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 Os erros de integridade referencial ocorrem quando um valor de chave estrangeira em uma tabela dependente não tem uma entrada correspondente na tabela pai. Esse erro ocorre quando o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] processa uma dimensão na qual a tabela de fatos faz referência a um valor de chave estrangeira que não existe na tabela de dimensões para essa dimensão ou quando o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] processa uma partição quando a tabela de dimensões principal para uma dimensão que está incluída na partição faz referência a um valor de chave que não existe em outra tabela de dimensões associada. Quando existem dimensões com hierarquias pai-filho e atributos pai, esse erro também pode ocorrer quando a tabela de dimensões principal para uma dimensão que está incluída na partição faz referência a um valor de chave que não existe na mesma tabela de dimensões.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*IgnoreError*|O processamento deve ignorar o erro e continuar.|  
|*ReportAndContinue*|O processamento deve relatar o erro e continuar.|  
|*ReportAndStop*|O processamento deve relatar o erro e parar.|  
  
 A enumeração que corresponde aos valores permitidos para **KeyNotFound** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ErrorOption>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

