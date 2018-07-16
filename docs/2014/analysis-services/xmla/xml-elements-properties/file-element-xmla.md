---
title: Arquivo de elemento (XMLA) | Microsoft Docs
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
- File Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.file
- http://schemas.microsoft.com/analysisservices/2003/engine#File
- urn:schemas-microsoft-com:xml-analysis#File
helpviewer_keywords:
- File element
ms.assetid: 3dfd0e9b-746b-4ce5-8a95-610d2e573739
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b75a261f4a86d5a227e1018ad96a40d91db7b6c7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319216"
---
# <a name="file-element-xmla"></a>Elemento File (XMLA)
  Identifica um arquivo a ser usado pelo pai [Backup](../xml-elements-commands/backup-element-xmla.md) ou [restaurar](../xml-elements-commands/restore-element-xmla.md) comando, ou pelo pai [local](location-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <File>...</File>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Backup](../xml-elements-commands/backup-element-xmla.md), [local](location-element-xmla.md), [restaurar](../xml-elements-commands/restore-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento `File` contém um nome de arquivo UNC e o elemento pai determina o uso do elemento `File`.  
  
 Para comandos `Backup`, o elemento `File` determina o nome do arquivo de backup criado pelo comando `Backup`. Se um caminho não for especificado como parte do nome do arquivo, o caminho especificado na `BackupDir` propriedade de configuração para a instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] é usado. Se o arquivo especificado já existir, ocorrerá um erro, a não ser que o elemento `AllowOverwrite` do comando pai `Backup` seja definido como `True`.  
  
 Para comandos `Restore`, o elemento `File` determina o nome do arquivo de backup a ser restaurado pelo comando `Restore`.  
  
 Para elementos `Location`, o elemento `File` descreve um arquivo de backup remoto para uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que contém partições remotas. Para obter mais informações sobre como fazer backup e restaurar partições remotas, consulte [fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento AllowOverwrite &#40;XMLA&#41;](allowoverwrite-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
