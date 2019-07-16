---
title: Coleções (sintaxe do ADO para Visual C++) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- ADO for Visual C++ syntax [ADO]
- syntax indexes [ADO], ADO for Visual C++ syntax
- collections [ADO], ADO for Visual C++ syntax
ms.assetid: 6a0109a0-f2d9-4f7c-8e1e-42763f9acaea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f18884c7a1aabe138408cca7eb529f4f21120330
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919918"
---
# <a name="collections-ado-for-visual-c-syntax"></a>Coleções (Sintaxe do ADO para Visual C++)
## <a name="parameters"></a>Parâmetros  
  
### <a name="methods"></a>Métodos  
  
```  
Append(IDispatch *Object);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 Para saber mais, veja  
  
-   [Método Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Método Delete (Coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Propriedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, _ADOParameter **ppvObject);  
```  
  
 Para saber mais, veja  
  
-   [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Propriedade Item (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="fields"></a>Campos  
  
### <a name="methods"></a>Métodos  
  
```  
Append(BSTR bstrName, DataTypeEnum Type, long DefinedSize, FieldAttributeEnum Attrib);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 Para saber mais, veja  
  
-   [Método Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Método Delete (Coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Propriedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOField **ppvObject);  
```  
  
 Para saber mais, veja  
  
-   [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Propriedade Item (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="errors"></a>Erros  
  
### <a name="methods"></a>Métodos  
  
```  
Clear(void);  
Refresh(void);  
```  
  
 Para saber mais, veja  
  
-   [Método Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)  
  
-   [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Propriedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOError **ppvObject);  
```  
  
 Para saber mais, veja  
  
-   [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Propriedade Item (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="properties"></a>Propriedades  
  
### <a name="methods"></a>Métodos  
  
```  
Refresh(void);  
```  
  
 Para saber mais, veja  
  
-   [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Propriedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOProperty **ppvObject);  
```  
  
 Para saber mais, veja  
  
-   [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Propriedade Item (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Coleção Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
