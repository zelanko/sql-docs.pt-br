---
title: Elemento DatabasePermission (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DatabasePermission Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DatabasePermission
helpviewer_keywords:
- DatabasePermission element
ms.assetid: 6dcb9136-a40d-42e3-ad3b-b8ce8c7ca78c
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f1fb55349384d99d3b7e6f8647abfd2c7468e87b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="databasepermission-element-assl"></a>Elemento DatabasePermission (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define as permissões padrão em uma [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento para um determinado [função](../../../analysis-services/scripting/objects/role-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DatabasePermissions>  
      <DatabasePermission xsi:type="Permission">  
      <!-- The following elements extend Permission -->  
      <Administer>...</Administer>  
...</DatabasePermission>  
</DatabasePermissions>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[Permissão](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|Valor padrão|False|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DatabasePermissions](../../../analysis-services/scripting/collections/databasepermissions-element-assl.md)|  
|Elementos filho|[Administrar](../../../analysis-services/scripting/properties/administer-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Os objetos**DatabasePermission** podem existir somente para as funções possuídas pelo banco de dados e somente um objeto **DatabasePermission** pode existir para qualquer função.  
  
 Este elemento tem as validações a seguir no valor 2 DeploymentMode (modelos tabulares).  
  
-   O valor padrão do atributo*Administer* é definido como **False**, menos quando o usuário tem privilégios administrativos. Para usuários com privilégios administrativos, o valor do atributo é definido como **True**.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DatabasePermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Role & #40; ASSL & #41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
