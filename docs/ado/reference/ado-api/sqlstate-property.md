---
title: Propriedade SQLState | Microsoft Docs
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
f1_keywords:
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13ca3fb822dc6ea79f835a3d50cac847b345c29b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="sqlstate-property"></a>Propriedade SQLState
Indica o estado do SQL para um determinado [erro](../../../ado/reference/ado-api/error-object.md) objeto.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna os cinco caracteres **cadeia de caracteres** valor que segue o padrão SQL ANSI e indica o código de erro.  
  
## <a name="remarks"></a>Remarks  
 Use o **SQLState** propriedade para ler o código de erro de cinco caracteres que o provedor retorna quando ocorre um erro durante o processamento de uma instrução SQL. Por exemplo, ao usar o Microsoft OLE DB Provider para ODBC com um banco de dados do Microsoft SQL Server, os códigos de erro de estado SQL se originar de ODBC, com base em erros de ODBC específicos ou sobre os erros que se originam do Microsoft SQL Server e, em seguida, são mapeados para ODBC erros. Esses códigos de erro estão documentados no padrão ANSI SQL, mas podem ser implementados de maneira distinta por fontes de dados diferentes.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Consulte também  
 [Descrição, HelpContext, HelpFile, NativeError, número, fonte e exemplo de propriedades de SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descrição, HelpContext, HelpFile, NativeError, número, fonte e exemplo de propriedades de SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
