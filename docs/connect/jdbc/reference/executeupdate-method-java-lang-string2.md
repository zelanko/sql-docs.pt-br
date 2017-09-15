---
title: "Método (Java) executeUpdate | Microsoft Docs"
ms.custom: 
ms.date: 02/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerPreparedStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 91ecb1cd-001d-4ac9-9ae8-5db05c3c2959
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 264ccb901e544eb0990f39ed53d112c7f8e9220f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="executeupdate-method-javalangstring"></a>Método executeUpdate (java.lang.String)

Executa a instrução SQL fornecida, que pode ser INSERT, UPDATE, MERGE ou DELETE; ou uma instrução SQL que não retorne nada, como uma instrução SQL DDL.

## <a name="syntax"></a>Sintaxe

```
public final int executeUpdate(java.lang.String sql)
```

#### <a name="parameters"></a>Parâmetros
*SQL*

Um **cadeia de caracteres** que contém a instrução SQL.

## <a name="return-value"></a>Valor de retorno
Um **int** que indica o número de linhas afetadas ou 0 se usando uma instrução DDL.

## <a name="exceptions"></a>Exceções
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Comentários
Esse método executeUpdate é especificado pelo método na interface PreparedStatement executeUpdate.

Chamar esse método resultará em uma exceção porque a instrução SQL para o objeto SQLServerPreparedStatement for especificada quando o objeto é criado.

## <a name="see-also"></a>Consulte também

[Método executeUpdate &#40; SQLServerPreparedStatement &#41;](./executeupdate-method-sqlserverpreparedstatement.md)

[Membros de SQLServerPreparedStatement](./sqlserverpreparedstatement-members.md)

[Classe SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md)

