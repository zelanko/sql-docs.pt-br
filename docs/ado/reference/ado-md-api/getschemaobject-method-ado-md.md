---
title: Método GetSchemaObject (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- GetSchemaObject
- Cellset::GetSchemaObject
helpviewer_keywords:
- GetSchemaObject method [ADO MD]
ms.assetid: 36b754b4-6b17-4dd1-a925-bca46938b7c4
author: rothja
ms.author: jroth
ms.openlocfilehash: a8853e967a75a67aadccc7e48d684ab92819a71d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764207"
---
# <a name="getschemaobject-method-ado-md"></a>Método GetSchemaObject (ADO MD)
Recupera um objeto de esquema ADO MD ([dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md)ou [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md)) por seu [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ObjType*  
 Um valor [SchemaObjectTypeEnum](../../../ado/reference/ado-md-api/schemaobjecttypeenum.md) que especifica o tipo de objeto de esquema (dimensão, hierarquia, nível ou membro) a ser recuperado.  
  
 *UniqueName*  
 Uma **cadeia de caracteres** que especifica o valor da propriedade **UniqueName** do objeto a ser recuperado.  
  
## <a name="remarks"></a>Comentários  
 **GetSchemaObject** recupera objetos usando seus nomes exclusivos, conforme especificado pela propriedade **UniqueName** . Os nomes dos objetos pai não precisam ser conhecidos e as coleções pai não precisam ser preenchidas para recuperar um objeto de esquema.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
