---
title: Comando (sintaxe do ADO para Visual C++) | Microsoft Docs
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
- Command collection [ADO], ADO for Visual C++ syntax
ms.assetid: cf12cbd1-25f7-4bb5-aa94-0fe823b3b6d6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 49a82682e619bb2a33e5c04e049b40ac4733f427
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919878"
---
# <a name="command-ado-for-visual-c-syntax"></a>Comando (Sintaxe do ADO para Visual C++)
## <a name="methods"></a>Métodos  
  
```  
Cancel(void)  
CreateParameter(BSTR Name, DataTypeEnum Type, ParameterDirectionEnum Direction, long Size, VARIANT Value, _ADOParameter **ppiprm)  
Execute(VARIANT *RecordsAffected, VARIANT *Parameters, long Options, _ADORecordset **ppirs)  
```  
  
## <a name="properties"></a>Propriedades  
  
```  
get_ActiveConnection(_ADOConnection **ppvObject)  
put_ActiveConnection(VARIANT vConn)  
putref_ActiveConnection(_ADOConnection *pCon)  
get_CommandText(BSTR *pbstr)  
put_CommandText(BSTR bstr)  
get_CommandTimeout(LONG *pl)  
put_CommandTimeout(LONG Timeout)  
get_CommandType(CommandTypeEnum *plCmdType)  
put_CommandType(CommandTypeEnum lCmdType)  
get_Name(BSTR *pbstrName)  
put_Name(BSTR bstrName)  
get_Prepared(VARIANT_BOOL *pfPrepared)  
put_Prepared(VARIANT_BOOL fPrepared)  
get_State(LONG *plObjState)  
get_Parameters(ADOParameters **ppvObject)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
