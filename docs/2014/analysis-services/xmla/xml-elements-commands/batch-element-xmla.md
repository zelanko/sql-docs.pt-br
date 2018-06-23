---
title: Lote de elemento (XMLA) | Microsoft Docs
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
- Batch Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Batch
- microsoft.xml.analysis.batch
- http://schemas.microsoft.com/analysisservices/2003/engine#Batch
helpviewer_keywords:
- Batch command
ms.assetid: 818f3212-9605-4e34-8623-1154d9fae1f0
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 76fcd68ca71db298bc66dc63a3fa20c394c196c8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120876"
---
# <a name="batch-element-xmla"></a>Elemento Batch (XMLA)
  Executa o XML de um ou mais comandos Analysis (XMLA) como uma operação em lote, em sequência ou em paralelo, em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Batch Transaction="Boolean" ProcessAffectedObjects="Boolean">  
      <Bindings>...</Bindings>  
      <DataSource>...</DataSource>  
      <DataSourceView>...</DataSourceView>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <Parallel>...</Parallel>  
      <!-- One or more XMLA commands -->  
   </Batch>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[Associações](../xml-elements-properties/bindings-element-xmla.md), [DataSource](../xml-elements-properties/source-element-xmla.md), [DataSourceView](../xml-elements-properties/datasourceview-element-xmla.md), [ErrorConfiguration](../../scripting/objects/errorconfiguration-element-assl.md), [paralela](../xml-elements-properties/parallel-element-xmla.md)<br /><br /> One or more of the following XMLA commands: [Alter](alter-element-xmla.md), [Backup](backup-element-xmla.md), [BeginTransaction](begintransaction-element-xmla.md), [ClearCache](clearcache-element-xmla.md), [CommitTransaction](committransaction-element-xmla.md), [Create](create-element-xmla.md), [Delete](delete-element-xmla.md), [DesignAggregations](designaggregations-element-xmla.md), [Drop](drop-element-xmla.md), [Insert](insert-element-xmla.md), [Lock](lock-element-xmla.md), [MergePartitions](mergepartitions-element-xmla.md), [NotifyTableChange](notifytablechange-element-xmla.md), [Process](process-element-xmla.md), [Restore](restore-element-xmla.md), [RollbackTransaction](rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e), [Statement](statement-element-xmla.md), [Subscribe](subscribe-element-xmla.md), [Synchronize](synchronize-element-xmla.md), [Unlock](unlock-element-xmla.md), [Update](update-element-xmla.md), [UpdateCells](drop-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|attribute|Description|  
|---------------|-----------------|  
|ProcessAffectedObjects|(Atributo `Boolean` opcional) Indica se todos os objetos que devem ser reprocessados serão processados.<br /><br /> Se for definido como true, a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] processará qualquer objeto que precise ser reprocessado em resultado do processamento de um objeto incluído no comando `Batch`.<br /><br /> Se for definido como `false`, a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] processará somente os objetos incluídos no comando `Batch`.|  
|Transaction|(Atributo `Boolean` opcional) Indica se o comando incluído no comando `Batch` é tratado como uma única transação ou transações individuais.<br /><br /> Se for definido como true, todos os comandos incluídos no comando `Batch` serão considerados como uma única transação. Se algum comando falhar, os comandos executados antes do comando com falha serão revertidos e o comando `Batch` vai parar sem executar os comandos subsequentes.<br /><br /> Se for definido como `false`, o comando `Batch` tentará executar cada comando e confirmará os resultados de cada comando concluído com êxito.|  
  
## <a name="remarks"></a>Remarks  
  
> [!WARNING]  
>  Comando/Executar/Instrução não tem suporte no momento em uma operação de lote.  
  
 Para obter mais informações sobre como executar operações em lotes em XMLA, consulte [executando operações de lote &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  