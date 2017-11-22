---
title: "Método Execute (Java, int[]) | Microsoft Docs"
ms.custom: 
ms.date: 02/07/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerStatement.execute (javal.lang.String.int[])
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: dc73d1c3-e756-43af-b1fc-ac438cbd0965
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3fa9cc8796aeb415a58b8c4d65c2f346f57febb0
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="execute-method-javalangstring-int"></a>Método execute (java.lang.String, int[])

  Executa a instrução SQL fornecida, que pode retornar vários resultados e sinaliza [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion-md.md)] que as chaves geradas automaticamente indicadas na matriz fornecida devem ser disponibilizadas para recuperação.

## <a name="syntax"></a>Sintaxe

```Java
public final boolean execute(
    java.lang.String sql,
    int[] columnIndexes)
```

#### <a name="parameters"></a>Parâmetros
*SQL*

Um **cadeia de caracteres** que contém uma instrução SQL.

*columnIndexes*

Uma matriz de **int**s que indica os índices de coluna das chaves geradas automaticamente que devem ser disponibilizados.

## <a name="return-value"></a>Valor de retorno
**True** se o primeiro resultado é um conjunto de resultados. Caso contrário, **false**.
  
## <a name="exceptions"></a>Exceções
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Comentários
Esse método execute é especificado pelo método execute na interface Java.SQL. Statement.

## <a name="see-also"></a>Consulte também

[Executar método &#40; SQLServerStatement &#41;](./execute-method-sqlserverstatement.md)

[Membros SQLServerStatement](./sqlserverstatement-members.md)

[Classe SQLServerStatement](./sqlserverstatement-class.md)
