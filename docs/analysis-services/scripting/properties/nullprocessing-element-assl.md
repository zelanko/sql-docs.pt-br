---
title: Elemento NullProcessing (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5a33081488c3be0f98f498d31710abb3e742504f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="nullprocessing-element-assl"></a>NullProcessing Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Automatic*|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[O item de dados](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Preservar*|Preserva o valor nulo.<br /><br /> Observação: Esse valor não é suportado para medidas de contagem distinta.|  
|*Erro*|Gera um erro de chave nula. O valor de [NullKeyNotAllowed](../../../analysis-services/scripting/properties/nullkeynotallowed-element-assl.md) determina como a instância reage ao erro.<br /><br /> Observação: Esse valor não é suportado para medidas.|  
|*UnknownMember*|Gera um membro desconhecido e um erro de conversão nula. O valor de [NullKeyConvertedToUnknown](../../../analysis-services/scripting/properties/nullkeyconvertedtounknown-element-assl.md) determina como a instância reage ao erro.<br /><br /> Observação: Esse valor não tem suporte para colunas associadas às medidas.|  
|*ZeroOrBlank*|Converte o valor nulo em zero (para itens de dados numéricos) ou em uma cadeia de caracteres vazia (para itens de dados de cadeia de caracteres).<br /><br /> Observação: Esse valor fornece compatibilidade com versões anteriores do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|*Automatic*|Usa o processamento padrão apropriado para o elemento:<br /><br /> *ZeroOrBlank* para itens de dados OLAP.<br /><br /> *UnknownMember* para itens de dados de mineração de dados.|  
  
 A enumeração que corresponde aos valores permitidos para **NullProcessing** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.NullProcessing>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
