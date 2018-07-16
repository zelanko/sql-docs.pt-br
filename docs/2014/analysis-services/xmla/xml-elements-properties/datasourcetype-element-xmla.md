---
title: Elemento DataSourceType (XMLA) | Microsoft Docs
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
- DataSourceType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DataSourceType
- microsoft.xml.analysis.datasourcetype
- http://schemas.microsoft.com/analysisservices/2003/engine#DataSourceType
helpviewer_keywords:
- DataSourceType element
ms.assetid: f5a348b1-911b-4139-832e-4bcb6d80a728
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c911f2a0e224cb8ccc9e7fa5b32a89a972fd1c26
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37207666"
---
# <a name="datasourcetype-element-xmla"></a>Elemento DataSourceType (XMLA)
  Indica se um [local](location-element-xmla.md) elemento especificado para um [restaurar](../xml-elements-commands/restore-element-xmla.md) ou [sincronizar](../xml-elements-commands/synchronize-element-xmla.md) comando é local ou remoto.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Location>  
   ...  
   <DataSourceType>...</DataSourceType>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres (enumeração)|  
|Valor padrão|*Remoto*|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Local](location-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento `DataSourceType` determina se a fonte de dados definida pelo elemento `Location` contém uma fonte de dados local ou remota. Para obter mais informações sobre como fazer backup e restaurar partições remotas, consulte [fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
 O valor desse elemento é limitado a uma das cadeias de caracteres listadas na tabela a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Local*|O elemento `Location` define uma fonte de dados local. Se este valor for usado, os comandos `Restore` e `Synchronize` usarão as informações definidas no elemento `Location` para atualizar a fonte de dados, recuperada a partir de um arquivo de backup especificado no elemento `File` do comando `Backup` ou de um banco de dados especificado no elemento `Source` do comando `Synchronize`, identificado no elemento `DataSourceID` do elemento `Location`.<br /><br /> Este valor permite que os objetos usem o armazenamento OLAP (ROLAP), após a recuperação ou a sincronização, com o objetivo de usar um banco de dados diferente para seus dados e metadados. **Observação:** dados ROLAP, como os dados em tabelas de dimensões ou tabelas de write-back, não são restaurados ou sincronizados. Somente os metadados de objetos ROLAP são recuperados ou sincronizados.|  
|*Remoto*|O elemento `Location` define uma fonte de dados remota. Se este valor for usado, os comandos `Restore` e `Synchronize` usarão as informações definidas no elemento `Location` para recuperar ou sincronizar partições remotas, recuperadas a partir de um arquivo de backup especificado no elemento `File` do comando `Backup` ou de um banco de dados especificado no elemento `Source` do comando `Synchronize`, da instância remota identificada em `DataSourceID` do elemento `Location`.|  
  
## <a name="see-also"></a>Consulte também  
 [Elemento ConnectionString &#40;XMLA&#41;](connectionstring-element-xmla.md)   
 [Elemento DataSourceID &#40;XMLA&#41;](id-element-xmla.md)   
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
