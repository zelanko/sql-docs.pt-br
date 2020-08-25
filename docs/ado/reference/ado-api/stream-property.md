---
description: Propriedade Stream
title: Propriedade de fluxo | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 97f378e1be87be95682bf2eeb05e112abfb96f9d
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777205"
---
# <a name="stream-property"></a>Propriedade Stream
Obtém ou define um objeto de **fluxo** de OLE DB de/em um objeto **ADOStreamConstruction** .  
  
 Leitura/gravação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>Parâmetros  
 *ppStream*  
 Ponteiro para um objeto de **fluxo** de OLE DB.  
  
 *pStream*  
 Um objeto de **fluxo** OLE DB.  
  
## <a name="return-values"></a>Valores de retorno  
 Esse método de propriedade retorna os valores de HRESULT padrão. Isso inclui S_OK e E_FAIL.  
  
## <a name="applies-to"></a>Aplica-se A  
 [ADOStreamConstruction Interface](./adostreamconstruction-interface.md)