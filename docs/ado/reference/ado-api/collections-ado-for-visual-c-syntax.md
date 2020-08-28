---
description: Coleções (Sintaxe do ADO para Visual C++)
title: Coleções (ADO para sintaxe de Visual C++) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b4bc59facd753bf6d36c3a79d06a4efe29e7c235
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975377"
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
  
-   [Método Append (ADO)](./append-method-ado.md)  
  
-   [Método Delete (Coleção de parâmetros ADO)](./delete-method-ado-parameters-collection.md)  
  
-   [Método Refresh (ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>Propriedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, _ADOParameter **ppvObject);  
```  
  
 Para obter mais informações, consulte  
  
-   [Propriedade Count (ADO)](./count-property-ado.md)  
  
-   [Propriedade Item (ADO)](./item-property-ado.md)  
  
## <a name="fields"></a>Campos  
  
### <a name="methods"></a>Métodos  
  
```  
Append(BSTR bstrName, DataTypeEnum Type, long DefinedSize, FieldAttributeEnum Attrib);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 Para obter mais informações, consulte  
  
-   [Método Append (ADO)](./append-method-ado.md)  
  
-   [Método Delete (Coleção de parâmetros ADO)](./delete-method-ado-parameters-collection.md)  
  
-   [Método Refresh (ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>Propriedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOField **ppvObject);  
```  
  
 Para obter mais informações, consulte  
  
-   [Propriedade Count (ADO)](./count-property-ado.md)  
  
-   [Propriedade Item (ADO)](./item-property-ado.md)  
  
## <a name="errors"></a>Errors  
  
### <a name="methods"></a>Métodos  
  
```  
Clear(void);  
Refresh(void);  
```  
  
 Para obter mais informações, consulte  
  
-   [Método Clear (ADO)](./clear-method-ado.md)  
  
-   [Método Refresh (ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>Propriedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOError **ppvObject);  
```  
  
 Para obter mais informações, consulte  
  
-   [Propriedade Count (ADO)](./count-property-ado.md)  
  
-   [Propriedade Item (ADO)](./item-property-ado.md)  
  
## <a name="properties"></a>Propriedades  
  
### <a name="methods"></a>Métodos  
  
```  
Refresh(void);  
```  
  
 Para obter mais informações, consulte  
  
-   [Método Refresh (ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>Propriedades  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOProperty **ppvObject);  
```  
  
 Para obter mais informações, consulte  
  
-   [Propriedade Count (ADO)](./count-property-ado.md)  
  
-   [Propriedade Item (ADO)](./item-property-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Coleta de erros (ADO)](./errors-collection-ado.md)   
 [Coleção Fields (ADO)](./fields-collection-ado.md)   
 [Coleção Parameters (ADO)](./parameters-collection-ado.md)   
 [Coleção Properties (ADO)](./properties-collection-ado.md)