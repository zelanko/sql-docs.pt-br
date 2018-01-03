---
title: "Método GetSchemaObject (ADO MD) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords: GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 425596babe4dab4147375f569e1cee2c7b790fa7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="getschemaobject-method-ado-md"></a>Método GetSchemaObject (ADO MD)
Recupera um objeto de esquema do ADO MD ([dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md), ou [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md)) por seus [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ObjType*  
 Um [SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md) valor que especifica o tipo de objeto de esquema (dimensão, hierarquia, nível ou membro) para recuperar.  
  
 *UniqueName*  
 Um **cadeia de caracteres** especificando o **UniqueName** valor da propriedade do objeto a ser recuperada.  
  
## <a name="remarks"></a>Remarks  
 **GetSchemaObject** recupera objetos usando seus nomes exclusivos, conforme especificado pelo **UniqueName** propriedade. Os nomes de objetos pai não precisam ser conhecidos e coleções pai não precisam ser preenchidos para recuperar um objeto de esquema.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
