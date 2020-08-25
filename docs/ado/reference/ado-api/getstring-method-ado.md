---
description: Método GetString (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a972edd11c419c1990c78635d42c44d8c06db2c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774905"
---
# <a name="getstring-method-ado"></a>Método GetString (ADO)
Retorna o [conjunto de registros](./recordset-object-ado.md) como uma cadeia de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Variant = recordset.GetString(StringFormat, NumRows, ColumnDelimiter, RowDelimiter, NullExpr)  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna o **conjunto de registros** como uma **variante** com valor de cadeia de caracteres (BSTR).  
  
#### <a name="parameters"></a>Parâmetros  
 *StringFormat*  
 Um valor [StringFormatEnum](./stringformatenum.md) que especifica como o **conjunto de registros** deve ser convertido em uma cadeia de caracteres. Os parâmetros *madelimiter*, *ColumnDelimiter*e *NullExpr* são usados apenas com um *StringFormat* de **adClipString**.  
  
 *NumRows*  
 Opcional. O número de linhas a serem convertidas no **conjunto de registros**. Se *numrows* não for especificado, ou se for maior que o número total de linhas no conjunto de **registros**, todas as linhas no conjunto de **registros** serão convertidas.  
  
 *ColumnDelimiter*  
 Opcional. Um delimitador usado entre colunas, se especificado, caso contrário, o caractere de TABULAção.  
  
 *RowDelimiter*  
 Opcional. Um delimitador usado entre linhas, se especificado, caso contrário, o caractere de retorno de carro.  
  
 *NullExpr*  
 Opcional. Uma expressão usada no lugar de um valor nulo, se especificado, caso contrário, a cadeia de caracteres vazia.  
  
## <a name="remarks"></a>Comentários  
 Dados de linha, mas sem dados de esquema, são salvos na cadeia de caracteres. Portanto, um **conjunto de registros** não pode ser reaberto usando essa cadeia de caracteres.  
  
 Esse método é equivalente ao método de **Hiperclipstring** RDO.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método GetString (VB)](./getstring-method-example-vb.md)