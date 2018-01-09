---
title: Elemento KeyDuplicate (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: KeyDuplicate Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: KeyDuplicate
helpviewer_keywords: KeyDuplicate element
ms.assetid: d7000b8b-e81f-4401-8738-00c2e0f73a59
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 97c4d349cecfc9fb1dd51c1c018110068b5be7dc
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="keyduplicate-element-assl"></a>Elemento KeyDuplicate (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Determina como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] manipula um erro de chave duplicada, caso seja encontrado algum durante o processamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyDuplicate>...</KeyDuplicate>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*IgnoreError*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 Os erros de chave duplicada são gerados apenas durante o processamento da dimensão, quando uma chave de atributo é encontrada mais de uma vez. Como as chaves de atributo devem ser exclusivas, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] descarta os registros duplicados. Os erros de chave duplicadas indicam uma falha na criação da dimensão, especificamente nas relações entre os atributos.  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*IgnoreError*|O processamento deve ignorar o erro e continuar.|  
|*ReportAndContinue*|O processamento deve relatar o erro e continuar.|  
|*ReportAndStop*|O processamento deve relatar o erro e parar.|  
  
 A enumeração que corresponde aos valores permitidos para **KeyDuplicate** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.ErrorOption>.  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
