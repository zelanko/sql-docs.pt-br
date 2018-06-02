---
title: Lote de elemento (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4644b8775212eae0cb6d912df9bc415c5fc96ec7
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34573938"
---
# <a name="batch-element-xmla"></a>Elemento Batch (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Executa um ou mais XML para comandos Analysis (XMLA) como uma operação em lote, em sequência ou em paralelo, em uma instância do Analysis Services.  
  
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
|Elementos pai|[Comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[Associações](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md), [DataSource](../../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md), [DataSourceView](../../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md), [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md), [paralela](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)<br /><br /> Um ou mais dos seguintes comandos do XMLA: [Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), [Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md), [ CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), [criar](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md), [excluir](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md), [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md), [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [Inserir](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [bloqueio](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md), [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md), [processo](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md), [Restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e), [instrução](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md), [assinar](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md), [Sincronizar](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md), [desbloquear](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md), [atualização](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|attribute|Description|  
|---------------|-----------------|  
|ProcessAffectedObjects|(Opcional **booliano** atributo) indica se todos os objetos que exigem o reprocessamento serão processados.<br /><br /> Se definido como true, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância processa todos os objetos que exigem o reprocessamento como resultado do processamento de um objeto incluído no **lote** comando.<br /><br /> Se definido como **false**, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância processa apenas os objetos incluídos no **lote** comando.|  
|Transaction|(Opcional **booliano** atributo) indica se o comando incluídos no **lote** comando são tratados como uma única transação ou transações individuais.<br /><br /> Se definido como true, todos os comandos incluídos no **lote** comando são considerados uma única transação. Se algum comando falhar, os comandos executados antes do comando com falha serão revertidos e o **lote** comando interrompe sem executar os comandos subsequentes.<br /><br /> Se definido como **false**, o **lote** comando tenta executar cada comando e confirmará os resultados de cada comando concluído com êxito.|  
  
## <a name="remarks"></a>Remarks  
  
> [!WARNING]  
>  Comando/Executar/Instrução não tem suporte no momento em uma operação de lote.  
  
 Para obter mais informações sobre como executar operações em lotes em XMLA, consulte [executando operações de lote &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md).  
  
## <a name="see-also"></a>Confira também
 [Comandos &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
