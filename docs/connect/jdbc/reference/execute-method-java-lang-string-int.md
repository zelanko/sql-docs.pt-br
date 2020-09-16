---
description: Método execute (java.lang.String, int[])
title: Método execute (java.lang.String, int[]) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.execute (javal.lang.String.int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc73d1c3-e756-43af-b1fc-ac438cbd0965
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 95c18d95e6014afc78fc53b8a37f3cd4d3509fd3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437768"
---
# <a name="execute-method-javalangstring-int"></a>Método execute (java.lang.String, int[])

  Executa a instrução SQL fornecida, que pode retornar diversos resultados, e sinaliza ao [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] que as chaves geradas automaticamente indicadas na matriz fornecida devem ser disponibilizadas para recuperação.

## <a name="syntax"></a>Sintaxe

```Java
public final boolean execute(
    java.lang.String sql,
    int[] columnIndexes)
```

#### <a name="parameters"></a>Parâmetros
*sql*

Uma **String** que contém uma instrução SQL.

*columnIndexes*

Uma matriz de **int**s que indica os índices de coluna das chaves geradas automaticamente que devem ser disponibilizados.

## <a name="return-value"></a>Valor de retorno
**true** se o primeiro resultado for um conjunto de resultados. Caso contrário, **false**.
  
## <a name="exceptions"></a>Exceções
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Comentários
Esse método execute é especificado pelo método execute na interface java.sql.PreparedStatement.

## <a name="see-also"></a>Consulte Também

[Método execute &#40;SQLServerStatement&#41;](./execute-method-sqlserverstatement.md)

[Membros SQLServerStatement](./sqlserverstatement-members.md)

[Classe SQLServerStatement](./sqlserverstatement-class.md)
