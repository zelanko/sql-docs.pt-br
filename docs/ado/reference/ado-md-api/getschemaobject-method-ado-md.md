---
description: Método GetSchemaObject (ADO MD)
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
ms.openlocfilehash: b0a54b02cf748d8ff1144e50e3531295dbfe8c55
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778115"
---
# <a name="getschemaobject-method-ado-md"></a>Método GetSchemaObject (ADO MD)
Recupera um objeto de esquema ADO MD ([dimensão](./dimension-object-ado-md.md), [hierarquia](./hierarchy-object-ado-md.md), [nível](./level-object-ado-md.md)ou [membro](./member-object-ado-md.md)) por seu [UniqueName](./uniquename-property-ado-md.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set object = CubeDef.GetSchemaObject (ObjType, UniqueName)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ObjType*  
 Um valor [SchemaObjectTypeEnum](./schemaobjecttypeenum.md) que especifica o tipo de objeto de esquema (dimensão, hierarquia, nível ou membro) a ser recuperado.  
  
 *UniqueName*  
 Uma **cadeia de caracteres** que especifica o valor da propriedade **UniqueName** do objeto a ser recuperado.  
  
## <a name="remarks"></a>Comentários  
 **GetSchemaObject** recupera objetos usando seus nomes exclusivos, conforme especificado pela propriedade **UniqueName** . Os nomes dos objetos pai não precisam ser conhecidos e as coleções pai não precisam ser preenchidas para recuperar um objeto de esquema.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto CubeDef (ADO MD)](./cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto CubeDef (ADO MD)](./cubedef-object-ado-md.md)