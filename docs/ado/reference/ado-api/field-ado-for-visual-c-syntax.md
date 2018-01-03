---
title: Campo (ADO para obter a sintaxe do Visual C++) | Microsoft Docs
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
dev_langs: C++
helpviewer_keywords: Field collection [ADO], ADO for Visual C++ syntax
ms.assetid: 04631b08-3937-440b-ac09-cd166f239908
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f842d5e89ca0c5ce323cbc8973716e491fb733b9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
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
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)
