---
title: Tipo de dados Permission (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Permission Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Permission
helpviewer_keywords:
- Permission data type
ms.assetid: 5f309544-59f8-4432-b1eb-b7c1a049f8df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8d12fb71a8ed19ca083e8ec506fba6338f6b58a7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101936"
---
# <a name="permission-data-type-assl"></a>Tipo de dados Permission (ASSL)
  Define um tipo de dados primitivo abstrato que representa as informações sobre uma permissão individual.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Permission>  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreateTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <RoleID>...</RoleID>  
   <Description>...</Description>  
   <Process>...</Process>  
   <ReadDefinition>...</ReadDefinition>  
   <Read>...</Read>  
   <Write>...</Write>  
   <Annotations>...</Annotations>  
</Permission>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipos de dados base|None|  
|Tipos de dados derivados|[CubePermission](../objects/cubepermission-element-assl.md), [DatabasePermission](../objects/databasepermission-element-assl.md), [DimensionPermission](permission-data-type-assl.md), [MiningModelPermission](../objects/miningmodelpermission-element-assl.md), [MiningStructurePermission](../objects/miningstructurepermission-element-assl.md)|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|None|  
|Elementos filho|[Anotações](../collections/annotations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [descrição](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [nome](../properties/name-element-assl.md), [Processo](../properties/process-element-assl.md), [leitura](../properties/read-element-assl.md), [ReadDefinition](../properties/readdefinition-element-assl.md), [RoleID](../properties/roleid-element-assl.md), [de gravação](../properties/write-element-assl.md)|  
|Elementos derivados|None|  
  
## <a name="remarks"></a>Comentários  
 `Permission` serve como o tipo base abstrato para diversos tipos de permissões derivadas usadas em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Este tipo de dados tem as validações a seguir no valor 2 de DeploymentMode (modo de servidor de tabela).  
  
-   *Processo* valor padrão do atributo é definido como `False`, exceto quando o usuário tem a **atualizar** permissão. Para usuários com o **Refresh** permissão a *processo* valor de atributo é definido como `True`.  
  
-   *ReadDefinition* valor de atributo é definido como `None`; qualquer outro valor gera um erro.  
  
-   *Leia* valor de atributo é definido como `Allowed` para usuários com o **usuário** permissão e, ao `None` quando os usuários são atribuídos ao **atualizar** permissão; se um usuário tiver as **Usuário** e **atualize** permissões e, em seguida, o atributo é definido como `Allowed`. Para usuários com privilégios administrativos, o valor do atributo é definido como `Allowed`.  
  
-   *Gravar* valor de atributo é definido como `None`; qualquer outro valor gera um erro.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.Permission>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de função &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [Tipos de dados XML de linguagem script do Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
