---
description: Propriedade NativeError (ADO)
title: Propriedade NativeError (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetNativeError
- Error::get_NativeError
- Error::NativeError
helpviewer_keywords:
- NativeError property [ADO]
ms.assetid: b9b47e57-18a4-4186-aef5-5bd18d7b1d74
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c22667a9cd5855e4715b8aa37774a9137ab3cc4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774054"
---
# <a name="nativeerror-property-ado"></a>Propriedade NativeError (ADO)
Indica o código de erro específico do provedor para um determinado objeto de [erro](./error-object.md) .  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor **longo** que indica o código de erro.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **NativeError** para recuperar as informações de erro específicas do banco de dados para um objeto de **erro** específico. Por exemplo, ao usar o provedor ODBC da Microsoft para OLE DB com um banco de dados Microsoft SQL Server, códigos de erro nativos originados de SQL Server passam pelo ODBC e o provedor ODBC para a propriedade **NativeError** do ADO.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Error](./error-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VB)](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VC + +)](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)