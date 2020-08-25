---
description: Propriedade SQLState
title: Propriedade SQLState | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
author: rothja
ms.author: jroth
ms.openlocfilehash: 65d72fed54723f525f4e1426ed04886e9d474985
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777365"
---
# <a name="sqlstate-property"></a>Propriedade SQLState
Indica o estado SQL de um determinado objeto de [erro](./error-object.md) .  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor de **cadeia de caracteres** de cinco caracteres que segue o padrão ANSI SQL e indica o código de erro.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **SQLSTATE** para ler o código de erro de cinco caracteres que o provedor retorna quando ocorre um erro durante o processamento de uma instrução SQL. Por exemplo, ao usar o provedor do Microsoft OLE DB para ODBC com um banco de dados Microsoft SQL Server, os códigos de erro de estado do SQL se originam do ODBC, com base em erros específicos do ODBC ou em erros originados de Microsoft SQL Server e, em seguida, são mapeados para erros ODBC. Esses códigos de erro são documentados no padrão ANSI SQL, mas podem ser implementados de forma diferente por diferentes fontes de dados.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Error](./error-object.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VB)](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VC + +)](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)