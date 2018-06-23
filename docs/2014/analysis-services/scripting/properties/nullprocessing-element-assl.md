---
title: Elemento NullProcessing (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- NullProcessing Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NullProcessing
helpviewer_keywords:
- NullProcessing element
ms.assetid: 697be5c6-e9a6-4f74-9ff4-5f31400c2178
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 54b75b2e1a7bddd6f7b5df1aeda0311c1b60ff99
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007132"
---
# <a name="nullprocessing-element-assl"></a>NullProcessing Element (ASSL)
  Define como valores nulos são processados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataItem>  
   ...  
   <NullProcessing>...</NullProcessing>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Automático*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[O item de dados](../data-type/dataitem-data-type-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Preservar*|Preserva o valor nulo. **Observação:** esse valor não é suportado para medidas de contagem distinta.|  
|*Erro*|Gera um erro de chave nula. O valor de [NullKeyNotAllowed](nullkeynotallowed-element-assl.md) determina como a instância reage ao erro. **Observação:** esse valor não é suportado para medidas.|  
|*UnknownMember*|Gera um membro desconhecido e um erro de conversão nula. O valor de [NullKeyConvertedToUnknown](nullkeyconvertedtounknown-element-assl.md) determina como a instância reage ao erro. **Observação:** esse valor não há suporte para colunas associadas às medidas.|  
|*ZeroOrBlank*|Converte o valor nulo em zero (para itens de dados numéricos) ou em uma cadeia de caracteres vazia (para itens de dados de cadeia de caracteres). **Observação:** esse valor fornece compatibilidade com versões anteriores do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|*Automático*|Usa o processamento padrão apropriado para o elemento:<br /><br /> -   *ZeroOrBlank* para itens de dados OLAP.<br />-   *UnknownMember* para itens de dados de mineração de dados.|  
  
 A enumeração que corresponde aos valores permitidos para `NullProcessing` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.NullProcessing>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  