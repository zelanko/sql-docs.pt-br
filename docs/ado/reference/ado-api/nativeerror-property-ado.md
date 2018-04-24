---
title: Propriedade NativeError (ADO) | Microsoft Docs
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
- Error::GetNativeError
- Error::get_NativeError
- Error::NativeError
helpviewer_keywords:
- NativeError property [ADO]
ms.assetid: b9b47e57-18a4-4186-aef5-5bd18d7b1d74
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 31b3a22526262543926012b66eb92d12487e7f2a
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="nativeerror-property-ado"></a>Propriedade NativeError (ADO)
Indica o código de erro específico do provedor para um determinado [erro](../../../ado/reference/ado-api/error-object.md) objeto.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **longo** valor que indica o código de erro.  
  
## <a name="remarks"></a>Remarks  
 Use o **NativeError** propriedade para recuperar as informações de erro específico de banco de dados para um determinado **erro** objeto. Por exemplo, ao usar o provedor do Microsoft ODBC para OLE DB com um banco de dados do Microsoft SQL Server, os códigos de erro nativo que se originam do SQL Server passam pelo ODBC e o provedor ODBC ao ADO **NativeError** propriedade.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Descrição, HelpContext, HelpFile, NativeError, número, fonte e exemplo de propriedades de SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descrição, HelpContext, HelpFile, NativeError, número, fonte e exemplo de propriedades de SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
