---
title: "Coleções (ADO - sintaxe WFC) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- syntax indexes [ADO], ADO/WFC
- collections [ADO], ADO/WFC syntax
- ADO/WFC syntax index [ADO]
ms.assetid: 073f9a0e-c755-42dd-9f71-4647d68e331a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 81a6c1f1c7ad0827b605e8e63c85a16efc1b51b5
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="collections-ado---wfc-syntax"></a>Coleções (ADO - WFC sintaxe)
**package com.ms.wfc.data**  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="methods"></a>Métodos  
  
```  
public void append(com.ms.wfc.data.Parameter param)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public Parameter getItem(int n)  
public Parameter getItem(String s)  
```  
  
### <a name="properties"></a>Propriedades  
  
```  
public int getCount()  
```  
  
## <a name="fields"></a>Campos  
  
### <a name="methods"></a>Métodos  
  
```  
public void append(String name, int type)  
public void append(String name, int type, int definedSize)  
public void append(String name, int type, int definedSize, int attrib)  
public void delete(int n)  
public void delete(String s)  
public void refresh()  
public com.ms.wfc.data.Field getItem(int n)  
public com.ms.wfc.data.Field getItem(String s)  
```  
  
### <a name="properties"></a>Propriedades  
  
```  
public int getCount()  
```  
  
## <a name="errors"></a>Erros  
  
### <a name="methods"></a>Métodos  
  
```  
public void clear()  
public void refresh()  
public com.ms.wfc.data.Error getItem(int n)  
public com.ms.wfc.data.Error getItem(String s)  
```  
  
### <a name="properties"></a>Propriedades  
  
```  
public int getCount()  
```  
  
## <a name="see-also"></a>Consulte também  
 [Coleção de erros (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Coleção de campos (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
