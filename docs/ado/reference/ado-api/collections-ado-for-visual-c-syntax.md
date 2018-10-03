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
manager: craigg
ms.openlocfilehash: d94570a337f564588b2709fd292eab5ed5396dc4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47679874"
---
# <a name="collections-ado-for-visual-c-syntax"></a>Coleções (Sintaxe do ADO para Visual C++)
## <a name="parameters"></a>Parâmetros  
  
### <a name="methods"></a>Métodos  
  
```  
Append(IDispatch *Object);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 Para obter mais informações, consulte  
  
-   [Método Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Método Delete (Coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Propriedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, _ADOParameter **ppvObject);  
```  
  
 Para obter mais informações, consulte  
  
-   [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Propriedade Item (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="fields"></a>Campos  
  
### <a name="methods"></a>Métodos  
  
```  
Append(BSTR bstrName, DataTypeEnum Type, long DefinedSize, FieldAttributeEnum Attrib);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 Para obter mais informações, consulte  
  
-   [Método Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Método Delete (Coleção de parâmetros ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Propriedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOField **ppvObject);  
```  
  
 Para obter mais informações, consulte  
  
-   [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Propriedade Item (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="errors"></a>Erros  
  
### <a name="methods"></a>Métodos  
  
```  
Clear(void);  
Refresh(void);  
```  
  
 Para obter mais informações, consulte  
  
-   [Método Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)  
  
-   [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Propriedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOError **ppvObject);  
```  
  
 Para obter mais informações, consulte  
  
-   [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Propriedade Item (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="properties"></a>Propriedades  
  
### <a name="methods"></a>Métodos  
  
```  
Refresh(void);  
```  
  
 Para obter mais informações, consulte  
  
-   [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>Propriedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOProperty **ppvObject);  
```  
  
 Para obter mais informações, consulte  
  
-   [Propriedade Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Propriedade Item (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Coleção Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
