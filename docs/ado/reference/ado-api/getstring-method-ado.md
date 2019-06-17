---
title: Método GetString (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_GetString
- Recordset20::GetString
helpviewer_keywords:
- GetString method [ADO]
ms.assetid: 92452940-b2a7-456e-94fc-3780c71da33c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 14bb7fd2e4a6dd8e6eb8f369342923ce1a9728c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697619"
---
# <a name="getstring-method-ado"></a>Método GetString (ADO)
Retorna o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) como uma cadeia de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Variant = recordset.GetString(StringFormat, NumRows, ColumnDelimiter, RowDelimiter, NullExpr)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna o **conjunto de registros** como um valor de cadeia de caracteres **Variant** (BSTR).  
  
#### <a name="parameters"></a>Parâmetros  
 *StringFormat*  
 Um [StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md) valor que especifica como o **Recordset** devem ser convertidas em uma cadeia de caracteres. O *RowDelimiter*, *ColumnDelimiter*, e *NullExpr* parâmetros são usados somente com um *StringFormat* de  **adClipString**.  
  
 *NumRows*  
 Opcional. O número de linhas a ser convertido na **conjunto de registros**. Se *NumRows* não for especificado, ou se ele for maior que o número total de linhas na **conjunto de registros**, em seguida, todas as linhas a **Recordset** são convertidos.  
  
 *ColumnDelimiter*  
 Opcional. Um delimitador usado entre colunas, se especificado, caso contrário, o caractere de tabulação.  
  
 *RowDelimiter*  
 Opcional. Um delimitador usado entre linhas, se especificado, caso contrário, o caractere de retorno de CARRO.  
  
 *NullExpr*  
 Opcional. Uma expressão usada no lugar de um valor nulo, se especificado, caso contrário, a cadeia de caracteres vazia.  
  
## <a name="remarks"></a>Comentários  
 Dados de linha, mas nenhum dado de esquema, é salvo na cadeia de caracteres. Portanto, uma **Recordset** não pode ser reaberto usando essa cadeia de caracteres.  
  
 Esse método é equivalente ao RDO **GetClipString** método.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método GetString (VB)](../../../ado/reference/ado-api/getstring-method-example-vb.md)
