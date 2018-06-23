---
title: Elemento location (XMLA) | Microsoft Docs
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
- Location Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.location
- urn:schemas-microsoft-com:xml-analysis#Location
- http://schemas.microsoft.com/analysisservices/2003/engine#Location
helpviewer_keywords:
- Location element
ms.assetid: cea5e776-f435-425a-9bce-812d727a2b71
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 51b0838b9843658b4081f9464c63274631ed74be
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120873"
---
# <a name="location-element-xmla"></a>Elemento Location (XMLA)
  Contém informações sobre um servidor remoto para o pai [Backup](../xml-elements-commands/backup-element-xmla.md), [restaurar](../xml-elements-commands/restore-element-xmla.md), ou [sincronizar](../xml-elements-commands/synchronize-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Location>  
```  
  
```  
  
<File>...</File> <!-- for Backup and Restore only -->  
<DataSourceID>...</DataSourceID>  
<DataSourceType>...</DataSourceType> <!-- for Restore and Synchronize only -->  
<ConnectionString>...</ConnectionString> <!-- for Restore and Synchronize only -->  
<Folders>...</Folders> <!-- for Restore and Synchronize only -->  
```  
  
```  
  
   </Location>  
   ...  
</Backup>  
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
|Elementos pai|[Backup](../xml-elements-commands/backup-element-xmla.md), [restaurar](../xml-elements-commands/restore-element-xmla.md), [sincronizar](../xml-elements-commands/synchronize-element-xmla.md)|  
  
## <a name="child-elements"></a>Elementos filho  
  
|Ancestral ou pai|Elemento filho|  
|------------------------|-------------------|  
|[Backup](id-element-xmla.md), [arquivo](file-element-xmla.md)|  
|[Restaurar](connectionstring-element-xmla.md), [DataSourceID](datasourceid-element-xmla.md), [DataSourceType](type-element-xmla.md), [arquivo](file-element-xmla.md), [pastas](folders-element-xmla.md)|  
|[Sincronizar](../xml-elements-commands/synchronize-element-xmla.md)|[ConnectionString](connectionstring-element-xmla.md), [DataSourceID](datasourceid-element-xmla.md), [DataSourceType](type-element-xmla.md), [pastas](folders-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 Para `Backup` comandos, o `Location` elemento fornece informações sobre como criar um arquivo de backup remoto para uma instância remota do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Para comandos `Restore`, o elemento `Location` fornece informações sobre a identificação e a conexão com uma instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] remota, bem como o arquivo de backup remoto utilizado para restaurar partições remotas naquela instância remota.  
  
 Para comandos `Synchronize`, o elemento  `Location` descreve uma fonte de dados a ser usada pela instância de destino ou uma instância remota definida na instância de origem que deve ser sincronizada com a instância de destino, dependendo do valor do elemento `DataSourceType` para o comando pai `Synchronize`.  
  
 Para obter mais informações sobre como fazer backup e restaurar instâncias remotas, consulte [fazendo backup e restaurando objetos (XMLA)](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento BackupRemotePartitions &#40;XMLA&#41;](backupremotepartitions-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  