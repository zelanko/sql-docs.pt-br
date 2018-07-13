---
title: Elemento DatabaseName (XMLA) | Microsoft Docs
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
- DatabaseName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.databasename
- http://schemas.microsoft.com/analysisservices/2003/engine#DatabaseName
- urn:schemas-microsoft-com:xml-analysis#DatabaseName
helpviewer_keywords:
- DatabaseName element
ms.assetid: 5cfd9a1f-da53-497a-b677-c51be4641bd0
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc7969194f91afa5dcf4d795ce33fae39d00c398
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37183203"
---
# <a name="databasename-element-xmla"></a>Elemento DatabaseName (XMLA)
  Identifica o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados a ser restaurado pelo pai [restaurar](../xml-elements-commands/restore-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Restore>  
   ...  
   <DatabaseName>...</DatabaseName>  
   ...  
</Restore>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Restaurar](../xml-elements-commands/restore-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento `DatabaseName` identifica o banco de dados no qual o comando `Restore` restaura um arquivo de backup. Se esse elemento não for especificado ou contiver uma cadeia de caracteres vazia, o nome do banco de dados contido no arquivo de backup será usado.  
  
 Se o banco de dados já existir na instância de destino, ocorrerá um erro a não ser que o elemento `AllowOverwrite` para o comando pai `Restore` seja definido como `True`.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento AllowOverwrite &#40;XMLA&#41;](allowoverwrite-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
