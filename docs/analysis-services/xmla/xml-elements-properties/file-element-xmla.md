---
title: Arquivo de elemento (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: File Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.file
- http://schemas.microsoft.com/analysisservices/2003/engine#File
- urn:schemas-microsoft-com:xml-analysis#File
helpviewer_keywords: File element
ms.assetid: 3dfd0e9b-746b-4ce5-8a95-610d2e573739
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 15b48617d6dfa14f06d635cbaeec17aedc7b2460
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="file-element-xmla"></a>Elemento File (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Identifica um arquivo a ser usado pelo pai [Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) ou [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) comando, ou pelo pai [local](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <File>...</File>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [local](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md), [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **arquivo** elemento contém um nome de arquivo UNC e o elemento pai determina o uso do **arquivo** elemento.  
  
 Para **Backup** comandos, o **arquivo** elemento determina o nome do arquivo de backup criado pelo **Backup** comando. Se um caminho não for especificado como parte do nome do arquivo, o caminho especificado no **BackupDir** propriedade de configuração para a instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] é usado. Se o arquivo especificado já existir, ocorrerá um erro, a menos que o **AllowOverwrite** elemento do pai **Backup** estiver definido como **True**.  
  
 Para **restaurar** comandos, o **arquivo** elemento determina o nome do arquivo de backup a ser restaurado pelo **restaurar** comando.  
  
 Para **local** elementos, o **arquivo** elemento descreve um arquivo de backup remoto para um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância que contém partições remotas. Para obter mais informações sobre backup e restaurando partições remotas, consulte [fazendo backup, restauração e sincronizando bancos de dados &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento AllowOverwrite &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md)   
 [Propriedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
