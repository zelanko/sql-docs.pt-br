---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9e4804b5cbdec4008e1c967b81620ea96eead924
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711319"
---
# <a name="sqlstate-property"></a>Propriedade SQLState
Indica o estado do SQL para um determinado [erro](../../../ado/reference/ado-api/error-object.md) objeto.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um caractere de cinco **cadeia de caracteres** valor que segue o padrão ANSI SQL e indica o código de erro.  
  
## <a name="remarks"></a>Comentários  
 Use o **SQLState** propriedade para ler o código de erro de cinco caracteres que o provedor retorna quando ocorre um erro durante o processamento de uma instrução SQL. Por exemplo, ao usar o Microsoft OLE DB Provider para ODBC com um banco de dados do Microsoft SQL Server, os códigos de erro de estado SQL se originam do ODBC, com base no erros específicos de ODBC ou em erros que se originam do Microsoft SQL Server e, em seguida, são mapeados para ODBC erros. Esses códigos de erro estão documentados no padrão ANSI SQL, mas podem ser implementados de forma diferente por diferentes fontes de dados.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Descrição, HelpContext, HelpFile, NativeError, número, código-fonte e exemplo de propriedades de SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descrição, HelpContext, HelpFile, NativeError, número, código-fonte e SQLState exemplo das propriedades (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
