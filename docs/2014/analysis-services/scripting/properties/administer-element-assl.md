---
title: Elemento Administer (ASSL) | Microsoft Docs
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
- Administer Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Administer
helpviewer_keywords:
- Administer element
ms.assetid: 52924cd6-6176-47c8-ab17-4ee0e0ce42b1
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 099e5b9283acf8da6268e8b5abaaad73049ca076
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009839"
---
# <a name="administer-element-assl"></a>Elemento Administer (ASSL)
  Indica se a permissão associada inclui o direito de administrar um [banco de dados](../objects/database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DatabasePermission>  
      ...  
      <Administer>...</Administer>  
   ...  
</DatabasePermission>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Booliano|  
|Valor padrão|Falso|  
|Cardinalidade|0-1: elemento opcional que pode ocorrer apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[DatabasePermission](../objects/databasepermission-element-assl.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O elemento `Administer` indica se um usuário só pode executar funções administrativas no banco de dados especificado. A função de administrador de servidor pode executar funções administrativas em todos os bancos de dados contidos pela instância.  
  
 O elemento que corresponde ao pai do `Administer` no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DatabasePermission>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo de dados Permission &#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [Elemento Role &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [Propriedades &#40;ASSL&#41;](properties-assl.md)  
  
  