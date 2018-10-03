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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe681a0f93dd88ad7f4752daf213817c21b054ad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798274"
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
 Um **cadeia de caracteres** especificando as **UniqueName** valor da propriedade de objeto a ser recuperado.  
  
## <a name="remarks"></a>Comentários  
 **GetSchemaObject** recupera objetos usando seus nomes exclusivos, conforme especificado pelo **UniqueName** propriedade. Os nomes dos objetos pai não precisam ser conhecidos e pai coleções não precisam ser preenchidos para recuperar um objeto de esquema.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)
