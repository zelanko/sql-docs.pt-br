---
title: Elemento DbStorageLocation | Microsoft Docs
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
helpviewer_keywords:
- DbStorageLocation element
ms.assetid: 1f448249-103a-479f-ae86-b0017acd0436
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 055780c9c91817a44dce6dfdaeb6ea3b541c05a3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37223996"
---
# <a name="dbstoragelocation-element"></a>Elemento DbStorageLocation
  Especifica a pasta na qual o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cria e gerencia todos os dados de banco de dados e arquivos de metadados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Database>  
...  
   <ddl100_100:DbStorageLocation>...</ddl100_100:DbStorageLocation>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|""|  
|Cardinalidade|0-1: Elemento opcional que pode ocorrer somente uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Banco de dados](database-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O `DbStorageLocation` propriedade de banco de dados deve ser definida como um caminho de pasta UNC existente ou uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia é a pasta de dados do servidor padrão. Se a pasta não existir, ocorrerá um erro ao executar um comando `Create`, `Attach` ou `Alter`.  
  
 Além disso, o `DbStorageLocation` propriedade de banco de dados não pode ser definida para apontar para a pasta de dados do servidor ou qualquer uma de suas subpastas. Se o local apontar para a pasta de dados do servidor ou qualquer uma de suas subpastas, ocorrerá um erro ao executar um comando `Create`, `Attach` ou `Alter`.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Anexar e desanexar bancos de dados do Analysis Services](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  
