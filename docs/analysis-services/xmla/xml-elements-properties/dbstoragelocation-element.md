---
title: Elemento DbStorageLocation | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DbStorageLocation element
ms.assetid: 1f448249-103a-479f-ae86-b0017acd0436
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cf7859b90400b1dc6962e16c4d2c4e43f5290b75
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|""|  
|Cardinalidade|0-1: Elemento opcional que pode ocorrer somente uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Banco de dados](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 A propriedade **DbStorageLocation** do banco de dados deve ser definida como um caminho de pasta UNC existente ou uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia é a pasta de dados do servidor padrão. Se a pasta não existir, ocorrerá um erro ao executar um comando **Create**, **Attach**ou **Alter** .  
  
 Além disso, a propriedade do banco de dados **DbStorageLocation** não pode ser definida para apontar para a pasta de dados do servidor nem qualquer uma de suas subpastas. Se o local apontar para a pasta de dados do servidor ou qualquer uma de suas subpastas, ocorrerá um erro ao executar um comando **Create**, **Attach**ou **Alter** .  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Anexar e desanexar bancos de dados do Analysis Services](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  
