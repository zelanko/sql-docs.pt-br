---
description: Propriedade Rowset (ADO)
title: Propriedade Rowset (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3341def2ce9f9f8e68f2135dc2b38cc3f947366f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989367"
---
# <a name="rowset-property-ado"></a>Propriedade Rowset (ADO)
Obtém ou define um OLE DB objeto de **conjunto de linhas** de/em um objeto **ADORecordsetConstruction** . Quando você usa put_Rowset, o conjunto de linhas é transformado em um objeto **RECORDSET** ADO.  
  
 Leitura/gravação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT get_Rowset([out, retval] IUnknown** ppRowset);  
HRESULT put_Rowset([in] IUnknown* pRowset);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *ppRowset*  
 Ponteiro para um objeto de **conjunto de linhas** OLE DB.  
  
 *PRowset*  
 Um objeto de **conjunto de linhas** OLE DB.  
  
## <a name="return-values"></a>Valores de retorno  
 Esse método de propriedade retorna os valores de HRESULT padrão, incluindo S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Interface ADORecordsetConstruction](./adorecordsetconstruction-interface.md)