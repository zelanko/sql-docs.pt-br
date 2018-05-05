---
title: Propriedade de conjunto de linhas (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::PutRowset
- ADORecordsetConstruction::GetRowset
- ADORecordsetConstruction::Rowset
- ADORecordsetConstruction::put_Rowset
- ADORecordsetConstruction::get_Rowset
helpviewer_keywords:
- Rowset property [ADO]
ms.assetid: 7d359294-4ff2-47e0-8111-0c221b24d80e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9e5310f52345537b5062e8bb497589ceb61da9e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="rowset-property-ado"></a>Propriedade de conjunto de linhas (ADO)
Obtém ou define um banco de dados OLE **linhas** objeto de/em uma **ADORecordsetConstruction** objeto. Quando você usa put_Rowset, o conjunto de linhas é transformado em ADO **registros** objeto.  
  
 Leitura/gravação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT get_Rowset([out, retval] IUnknown** ppRowset);  
HRESULT put_Rowset([in] IUnknown* pRowset);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *ppRowset*  
 Ponteiro para um banco de dados OLE **linhas** objeto.  
  
 *PRowset*  
 OLE DB **linhas** objeto.  
  
## <a name="return-values"></a>Valores de retorno  
 Esse método de propriedade retorna os valores HRESULT padrão, incluindo S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Interface ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
