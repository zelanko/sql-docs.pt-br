---
title: Comando elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Command Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.command
- Command
- urn:schemas-microsoft-com:xml-analysis#Command
- http://schemas.microsoft.com/analysisservices/2003/engine#Command
helpviewer_keywords:
- Command element
ms.assetid: 9abc14df-7cbe-46bc-ba0f-f0691c19afad
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cea555f5bb40a0075a7a881ad4505d2d0c8602e7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="command-element-xmla"></a>Elemento Command (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém o comando a ser executado pelo [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Execute>  
   ...  
   <Command>  
      <Alter>...</Alter>  
      <!-- or -->  
      <Backup>...</Backup>  
      <!-- or -->  
      <Batch>...</Batch>  
      <!-- or -->  
      <BeginTransaction>...</BeginTransaction>  
      <!-- or -->  
      <Cancel>...</Cancel>  
      <!-- or -->  
      <ClearCache>...</ClearCache>  
      <!-- or -->  
      <CommitTransaction>...</CommitTransaction>  
      <!-- or -->  
      <Create>...</Create>  
      <!-- or -->  
      <Delete>...</Delete>  
      <!-- or -->  
      <DesignAggregations>...</DesignAggregations>  
      <!-- or -->  
      <Drop>...</Drop>  
      <!-- or -->  
      <Insert>...</Insert>  
      <!-- or -->  
      <Lock>...</Lock>  
      <!-- or -->  
      <MergePartitions>...</MergePartitions>  
      <!-- or -->  
      <NotifyTableChange>...</NotifyTableChange>  
      <!-- or -->  
      <Process>...</Process>  
      <!-- or -->  
      <Restore>...</Restore>  
      <!-- or -->  
      <RollbackTransaction>...</RollbackTransaction>  
      <!-- or -->  
      <SetPasswordEncryptionKey>...</SetPasswordEncryptionKey>  
      <!-- or -->  
      <Statement>...</Statement>  
      <!-- or -->  
      <Subscribe>...</Subscribe>  
      <!-- or -->  
      <Synchronize>...</Synchronize>  
      <!-- or -->  
      <Unlock>...</Unlock>  
      <!-- or -->  
      <Update>...</Update>  
      <!-- or -->  
      <UpdateCells>...</UpdateCells>  
   </Command>  
   ...  
</Execute>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Execute (executar)](../../../analysis-services/xmla/xml-elements-methods-execute.md)|  
|Elementos filho|[Alterar](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), [Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [lote](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md), [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [Cancelar](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md), [ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md) , [CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), [criar](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md), [excluir](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md), [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md), [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [Inserir](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [bloqueio](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md), [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md), [processo](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md), [Restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e), [instrução](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md), [ Assinar](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md), [sincronizar](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md), [desbloquear](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md), [atualização](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 O **comando** elemento é usado pelo **Execute** método para retransmitir comandos a uma fonte de dados. Enquanto o XML para especificação Analysis (XMLA) 1.1 oferece suporte apenas a **instrução** comando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] dá suporte a muitos novos comandos XMLA. Para obter mais informações sobre o comando XMLA com suporte [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [comandos &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML & #40; XMLA & #41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Propriedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
