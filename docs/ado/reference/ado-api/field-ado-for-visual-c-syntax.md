---
title: Campo (ADO para obter a sintaxe do Visual C++) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- Field collection [ADO], ADO for Visual C++ syntax
ms.assetid: 04631b08-3937-440b-ac09-cd166f239908
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1f089eead8435a81c48b002eccfe1b2b8b78775
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="field-ado-for-visual-c-syntax"></a>Campo (ADO para obter a sintaxe do Visual C++)
## <a name="methods"></a>Métodos  
  
```  
AppendChunk(VARIANT Data)  
GetChunk(long Length, VARIANT *pvar)  
```  
  
## <a name="properties"></a>Propriedades  
  
```  
get_ActualSize(long *pl)  
get_Attributes(long *pl)  
put_Attributes(long lAttributes)  
get_DataFormat(IUnknown **ppiDF)  
put_DataFormat(IUnknown *piDF)  
get_DefinedSize(long *pl)  
put_DefinedSize(long lSize)  
get_Name(BSTR *pbstr)  
get_NumericScale(BYTE *pbNumericScale)  
put_NumericScale(BYTE bScale)  
get_OriginalValue(VARIANT *pvar)  
get_Precision(BYTE *pbPrecision)  
put_Precision(BYTE bPrecision)  
get_Type(DataTypeEnum *pDataType)  
put_Type(DataTypeEnum DataType)  
get_UnderlyingValue(VARIANT *pvar)  
get_Value(VARIANT *pvar)  
put_Value(VARIANT Val)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)
