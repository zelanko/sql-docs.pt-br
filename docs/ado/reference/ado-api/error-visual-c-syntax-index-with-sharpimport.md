---
title: 'Erro (Visual C++ índice de sintaxe com #import) | Microsoft Docs'
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
- 'Error collection [ADO], Visual C++ syntax index with #import'
ms.assetid: 1ee59754-59c8-48e2-a4fb-242fa788c1f9
author: rothja
ms.author: jroth
ms.openlocfilehash: c118bcc524aefb03f1f34f66cd595a83e21f72d9
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758782"
---
# <a name="error-visual-c-syntax-index-with-import"></a>Erro (Visual C++ índice de sintaxe com #import)
## <a name="properties"></a>Propriedades  
  
```  
_bstr_t GetDescription( );  
__declspec(property(get=GetDescription)) _bstr_t Description;  
  
long GetHelpContext( );  
__declspec(property(get=GetHelpContext)) long HelpContext;  
  
_bstr_t GetHelpFile( );  
__declspec(property(get=GetHelpFile)) _bstr_t HelpFile;  
  
long GetNativeError( );  
__declspec(property(get=GetNativeError)) long NativeError;  
  
long GetNumber( );  
__declspec(property(get=GetNumber)) long Number;  
  
_bstr_t GetSource( );  
__declspec(property(get=GetSource)) _bstr_t Source;  
  
_bstr_t GetSQLState( );  
__declspec(property(get=GetSQLState)) _bstr_t SQLState;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de erro](../../../ado/reference/ado-api/error-object.md)
