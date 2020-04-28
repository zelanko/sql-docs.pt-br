---
title: SEQUÊNCIAs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/30/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SEQUENCES
- SEQUENCES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SEQUENCES view
- INFORMATION_SCHEMA.SEQUENCES view
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8ff8490824c6a0ccb45b383535e830cabff83407
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "77479344"
---
# <a name="sequences-transact-sql"></a>SEQUÊNCIAs (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna uma linha para cada sequência que pode ser acessada pelo usuário atual no banco de dados atual.

Para recuperar informações dessas exibições, especifique o nome totalmente qualificado de **INFORMATION_SCHEMA**_. view_name_.

|Nome da coluna|Tipo de dados|Descrição|
|-----------------|---------------|-----------------|
|**SEQUENCE_CATALOG**|**nvarchar(128)**|Qualificador de sequência|
|**SEQUENCE_SCHEMA**|**nvarchar (** 128) * *|Nome do esquema que contém a sequência|
|**SEQUENCE_NAME**|**nvarchar(128)**|Nome da sequência|
|**DATA_TYPE**|**nvarchar (** 128 **)**|O tipo de dados Sequence|
|**NUMERIC_PRECISION**|**tinyint**|A precisão da sequência|
|**NUMERIC_PRECISION_RADIX**|**smallint**|Base de precisão de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|
|**NUMERIC_SCALE**|**int**|Escala de dados numéricos aproximados, dados numéricos exatos, dados de inteiro ou dados monetários. Caso contrário, será retornado NULL.|
|**START_VALUE**|**int**|O primeiro valor que será retornado pelo objeto de sequência.|
|**MINIMUM_VALUE**|**int**|Os limites para o objeto de sequência. O valor mínimo padrão de um novo objeto de sequência é o valor mínimo do tipo de dados do objeto de sequência. É zero para o tipo de dados tinyint e um número negativo para todos os outros tipos de dados.|
|**MAXIMUM_VALUE**|**int**|Os limites para o objeto de sequência. O valor máximo padrão para um novo objeto de sequência é o valor máximo do tipo de dados do objeto de sequência.|
|**PROGRESSIV**|**int**|O valor usado para incrementar (ou decrementar, se negativo) o valor do objeto de sequência para cada chamada da função NEXT VALUE FOR. Se o incremento for um valor negativo, o objeto de sequência será decrescente, caso contrário, será crescente. O incremento não pode ser 0. O incremento padrão para um novo objeto de sequência é 1.
|**CYCLE_OPTION**|**int**|Propriedade que especifica se o objeto de sequência deve reiniciar do valor mínimo (ou máximo para objetos de sequência decrescente) ou deve lançar uma exceção quando seu valor mínimo ou máximo é excedido. A opção de ciclo padrão para novos objetos de sequência é NO CYCLE.
|**DECLARED_DATA_TYPE**|**int**|O tipo de dados para o tipo de dados definido pelo usuário.|
|**DECLARED_DATA_PRECISION**|**int**|A precisão do tipo de dados definido pelo usuário.|
|**DECLARED_NUJMERIC_SCALE**|**int**|A escala numérica para o tipo de dados definido pelo usuário.|

**Exemplo** O exemplo a seguir retorna informações sobre os esquemas no banco de dados de teste:

```sql
SELECT * FROM test.INFORMATION_SCHEMA.SEQUENCES;
```

## <a name="see-also"></a>Consulte Também

- [Exibições do esquema de informações &#40;&#41;Transact-SQL](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)
- [sys.sequences &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)
