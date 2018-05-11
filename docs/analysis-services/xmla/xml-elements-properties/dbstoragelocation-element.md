---
title: Elemento DbStorageLocation | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dfd4e547c6a32b5ff3d96ca7640c32567e18988c
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="dbstoragelocation-element"></a>Elemento DbStorageLocation
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
## <a name="remarks"></a>Remarks  
 A propriedade **DbStorageLocation** do banco de dados deve ser definida como um caminho de pasta UNC existente ou uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia é a pasta de dados do servidor padrão. Se a pasta não existir, ocorrerá um erro ao executar um comando **Create**, **Attach**ou **Alter** .  
  
 Além disso, a propriedade do banco de dados **DbStorageLocation** não pode ser definida para apontar para a pasta de dados do servidor nem qualquer uma de suas subpastas. Se o local apontar para a pasta de dados do servidor ou qualquer uma de suas subpastas, ocorrerá um erro ao executar um comando **Create**, **Attach**ou **Alter** .  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices.Database.DbStorageLocation%2A>   
 [Anexar e desanexar bancos de dados do Analysis Services](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  
