---
title: Método executeUpdate (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 91ecb1cd-001d-4ac9-9ae8-5db05c3c2959
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04b3bdcd2b495513500d07583fadc910fe9c13a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954680"
---
# <a name="executeupdate-method-javalangstring"></a>Método executeUpdate (java.lang.String)

Executa a instrução SQL fornecida, que pode ser INSERT, UPDATE, MERGE ou DELETE; ou uma instrução SQL que não retorne nada, como uma instrução SQL DDL.

## <a name="syntax"></a>Sintaxe

```
public final int executeUpdate(java.lang.String sql)
```

#### <a name="parameters"></a>Parâmetros
*sql*

Uma **String** que contém a instrução SQL.

## <a name="return-value"></a>Valor retornado
Um **int** que indica o número de linhas afetadas ou 0 se uma instrução DDL estiver sendo usada.

## <a name="exceptions"></a>Exceções
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Remarks
Esse método executeUpdate é especificado pelo método executeUpdate na interface java.sql.PreparedStatement.

Chamar esse método resultará em uma exceção, uma vez que a instrução SQL para o objeto SQLServerPreparedStatement é especificada quando o objeto é criado.

## <a name="see-also"></a>Consulte Também

[Método executeUpdate &#40;SQLServerPreparedStatement&#41;](./executeupdate-method-sqlserverpreparedstatement.md)

[Membros de SQLServerPreparedStatement](./sqlserverpreparedstatement-members.md)

[Classe SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md)
