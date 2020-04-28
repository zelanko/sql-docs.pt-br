---
title: 'Propriedade (Visual C++ índice de sintaxe com #import) | Microsoft Docs'
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
- 'Property collection [ADO], Visual C++ syntax index with #import'
ms.assetid: 80988ca7-f514-438d-bf6f-9390dfe93fc3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2175b8b07fcea8dc61ab0c47a4d85fcdb94dd7d9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931573"
---
# <a name="property-visual-c-syntax-index-with-import"></a>Propriedade (Visual C++ índice de sintaxe com #import)
## <a name="properties"></a>Propriedades  
  
```  
long GetAttributes( );  
void PutAttributes( long plAttributes );  
__declspec(property(get=GetAttributes,put=PutAttributes)) long  
    Attributes;  
  
_bstr_t GetName( );  
__declspec(property(get=GetName)) _bstr_t Name;  
  
enum DataTypeEnum GetType( );  
__declspec(property(get=GetType)) enum DataTypeEnum Type;  
  
_variant_t GetValue( );  
void PutValue( const _variant_t & pval );  
__declspec(property(get=GetValue,put=PutValue)) _variant_t Value;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Property (ADO)](../../../ado/reference/ado-api/property-object-ado.md)
