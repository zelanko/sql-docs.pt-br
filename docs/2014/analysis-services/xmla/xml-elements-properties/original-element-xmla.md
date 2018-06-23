---
title: Elemento original (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Original Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.original
- http://schemas.microsoft.com/analysisservices/2003/engine#Original
- urn:schemas-microsoft-com:xml-analysis#Original
helpviewer_keywords:
- Original element
ms.assetid: c98a3700-ac19-4341-85d9-5afedf662601
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 63ee76cd3b476b3a8dbf45a50ad0f9d22a55e0fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120201"
---
# <a name="original-element-xmla"></a>Elemento Original (XMLA)
  Contém o local de armazenamento de sistema arquivos original usado por um [pasta](folder-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Folder>  
   ...  
   <Original>...</Original>  
   ...  
</Folder>  
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
|Elementos pai|[Pasta](folder-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O `Original` elemento contém um caminho UNC para ser substituído pelo valor da [novo](new-element-xmla.md) elemento contido pelo pai `Folder` elemento para todos os objetos restaurados ou sincronizados, respectivamente, durante um [restaurar ](../xml-elements-commands/restore-element-xmla.md) ou [sincronizar](../xml-elements-commands/synchronize-element-xmla.md) comando. O valor desse elemento é comparado ao valor da [StorageLocation](../../scripting/properties/storagelocation-element-assl.md) elemento para cada cubo, grupo de medidas ou partição e, se uma correspondência for encontrada, o valor da `New` elemento é usado para atualizar o `StorageLocation` da objeto durante a restauração ou sincronização.  
  
 Para obter mais informações sobre backup e restauração de objetos, consulte [fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  