---
title: Método (Java) executeUpdate | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 91ecb1cd-001d-4ac9-9ae8-5db05c3c2959
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a48df94bb417825aba64699443de6e43fced0d12
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="executeupdate-method-javalangstring"></a>Método executeUpdate (java.lang.String)

Executa a instrução SQL fornecida, que pode ser INSERT, UPDATE, MERGE ou DELETE; ou uma instrução SQL que não retorne nada, como uma instrução SQL DDL.

## <a name="syntax"></a>Sintaxe

```
public final int executeUpdate(java.lang.String sql)
```

#### <a name="parameters"></a>Parâmetros
*sql*

Um **cadeia de caracteres** que contém a instrução SQL.

## <a name="return-value"></a>Valor de retorno
Um **int** que indica o número de linhas afetadas ou 0 se usando uma instrução DDL.

## <a name="exceptions"></a>Exceções
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Remarks
Esse método executeUpdate é especificado pelo método na interface PreparedStatement executeUpdate.

Chamar esse método resultará em uma exceção, uma vez que a instrução SQL para o objeto SQLServerPreparedStatement é especificada quando o objeto é criado.

## <a name="see-also"></a>Consulte também

[Método executeUpdate &#40;SQLServerPreparedStatement&#41;](./executeupdate-method-sqlserverpreparedstatement.md)

[Membros de SQLServerPreparedStatement](./sqlserverpreparedstatement-members.md)

[Classe SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md)
