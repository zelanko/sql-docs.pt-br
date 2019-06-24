---
title: Método Execute (lang. String, int[]) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d4ae744a27156a59c926f2181ca9aec1146e8cd7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801663"
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

## <a name="return-value"></a>Valor retornado
**True** se o primeiro resultado é um conjunto de resultados. Caso contrário, **false**.
  
## <a name="exceptions"></a>Exceções
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Remarks
Esse método execute é especificado pelo método execute na interface java.sql.PreparedStatement.

## <a name="see-also"></a>Consulte Também

[executar o método &#40;SQLServerStatement&#41;](./execute-method-sqlserverstatement.md)

[Membros SQLServerStatement](./sqlserverstatement-members.md)

[Classe SQLServerStatement](./sqlserverstatement-class.md)
