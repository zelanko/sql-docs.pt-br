---
description: Método GetSchemaObject (ADO MD)
title: Método GetSchemaObject (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 4031b9dbe100df7e73c64354888ffa97cf38c30c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986687"
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