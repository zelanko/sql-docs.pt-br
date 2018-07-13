---
title: Elemento DatabasePermission (ASSL) | Microsoft Docs
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
- DatabasePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DatabasePermission
helpviewer_keywords:
- DatabasePermission element
ms.assetid: 6dcb9136-a40d-42e3-ad3b-b8ce8c7ca78c
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0fbfd9544e5305169e0d25b1b0157197d39cc002
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37259522"
---
# <a name="databasepermission-element-assl"></a>Elemento DatabasePermission (ASSL)
  Define as permissões padrão em uma [banco de dados](database-element-assl.md) elemento para um determinado [função](role-element-assl.md) elemento.  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|[Permissão](../data-type/permission-data-type-assl.md)|  
|Valor padrão|Falso|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DatabasePermissions](../collections/databasepermissions-element-assl.md)|  
|Elementos filho|[Administrar](../properties/administer-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 Os objetos `DatabasePermission` podem existir somente para as funções possuídas pelo banco de dados e somente um objeto `DatabasePermission` pode existir para qualquer função.  
  
 Este elemento tem as validações a seguir no valor 2 DeploymentMode (modelos tabulares).  
  
-   *Administrar* valor padrão do atributo é definido como `False`, exceto quando o usuário tem privilégios administrativos. Para usuários com privilégios administrativos, o valor do atributo é definido como `True`.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.DatabasePermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento de função &#40;ASSL&#41;](role-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
