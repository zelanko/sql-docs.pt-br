---
title: Fluxo de propriedade | Microsoft Docs
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
f1_keywords:
- ADOStreamConstruction::GetStream
- ADOStreamConstruction::PutStream
- ADOStreamConstruction::put_Stream
- ADOStreamConstruction::Stream
- ADOStreamConstruction::get_Stream
helpviewer_keywords:
- Stream property
ms.assetid: 4a44f9f6-0265-4c00-8def-d85b6af923b1
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd848306588cba57a25e0a8e7e8a45ab5c563766
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="stream-property"></a>Propriedade de fluxo
Obtém ou define um banco de dados OLE **fluxo** objeto de/em uma **ADOStreamConstruction** objeto.  
  
 Leitura/gravação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *ppStream*  
 Ponteiro para um banco de dados OLE **fluxo** objeto.  
  
 *pStream*  
 OLE DB **fluxo** objeto.  
  
## <a name="return-values"></a>Valores de retorno  
 Esse método de propriedade retorna os valores HRESULT padrão. Isso inclui S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Aplica-se a  
 [ADOStreamConstruction Interface](../../../ado/reference/ado-api/adostreamconstruction-interface.md)
