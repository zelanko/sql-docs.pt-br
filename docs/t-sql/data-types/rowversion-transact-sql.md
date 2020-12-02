---
description: rowversion (Transact-SQL)
title: rowversion (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- timestamp_TSQL
- timestamp
dev_langs:
- TSQL
helpviewer_keywords:
- rowversion data type
- size [SQL Server], rowversion
- row version-stamping [SQL Server]
- rowversion columns
- version-stamping table rows
- unique rowversion numbers
- unique timestamp numbers
- timestamp data type
- timestamp columns
- size [SQL Server], timestamp
ms.assetid: 65c9cf0e-3e8a-45f8-87b3-3460d96afb0b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 087e3e1d67bce5d8f46f03cdb1cad05578b39b46
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88479871"
---
# <a name="rowversion-transact-sql"></a>rowversion (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

É um tipo de dados que expõe números binários exclusivos, gerados automaticamente, em um banco de dados. **rowversion** geralmente é usado como um mecanismo para linhas de tabela de registro de versão. O tamanho do armazenamento é de 8 bytes. O tipo de dados **rowversion** é apenas um número que aumenta e não preserva uma data nem hora. Para gravar uma data ou hora, use um tipo de dados **datetime2**.
  
## <a name="remarks"></a>Comentários  
Cada banco de dados tem um contador que é incrementado para cada operação de inserção ou atualização executada em uma tabela que contém uma coluna **rowversion** no banco de dados. Esse contador é a rowversion do banco de dados. Isso controla uma hora relativa em um banco de dados, não uma hora real que pode ser associada a um relógio. Uma tabela pode ter apenas uma coluna **rowversion**. Sempre que uma linha com uma coluna **rowversion** é modificada ou inserida, o valor de rowversion do banco de dados incrementado é inserido na coluna **rowversion**. Essa propriedade torna uma coluna **rowversion** uma pobre candidata a chaves, especialmente, chaves primárias. Qualquer atualização feita na linha altera o valor de rowversion e, portanto, altera o valor de chave. Se a coluna estiver em uma chave primária, o valor da chave antiga não será mais válido e as chaves estrangeiras que fazem menção ao valor antigo não serão mais válidas. Se a tabela for mencionada em um cursor dinâmico, todas as atualizações alterarão a posição das linhas no cursor. Se a coluna for uma chave de índice, todas as atualizações na linha de dados também gerarão atualizações do índice.  O valor de **rowversion** é incrementado com qualquer instrução de atualização, mesmo se nenhum valor de linha for alterado. (Por exemplo, se um valor de coluna é 5 e uma instrução de atualização define o valor como 5, essa ação é considerada uma atualização, embora não exista nenhuma alteração e a **rowversion** seja incrementada.)
  
**timestamp** é o sinônimo do tipo de dados **rowversion** e está sujeito ao comportamento de sinônimos de tipo de dados. Em instruções DDL, use **rowversion** em vez de **timestamp** sempre que possível. Para obter mais informações, consulte [Sinônimos de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
O tipo de dados [!INCLUDE[tsql](../../includes/tsql-md.md)] **timestamp** é diferente do tipo de dados **timestamp** definido no padrão ISO.
  
> [!NOTE]  
>  A sintaxe de **timestamp** foi preterida. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
Em uma instrução CREATE TABLE ou ALTER TABLE, você não precisará especificar um nome de coluna para o tipo de dados **timestamp**, por exemplo:
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, timestamp);  
```  
  
Se você não especificar um nome de coluna, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] gerará o nome da coluna **timestamp**; no entanto, o sinônimo de **rowversion** não segue este comportamento. Quando você usar **rowversion**, precisará especificar um nome de coluna, por exemplo:
  
```sql
CREATE TABLE ExampleTable2 (PriKey int PRIMARY KEY, VerCol rowversion) ;  
```  
  
> [!NOTE]  
>  Os valores duplicados de **rowversion** podem ser gerados com a instrução SELECT INTO na qual uma coluna **rowversion** está na lista SELECT. Não recomendamos o uso de **rowversion** desta maneira.  
  
Uma coluna **rowversion** que não permite valor nulo é semanticamente equivalente a uma coluna **binary(8)**. Uma coluna **rowversion** que permite valor nulo é semanticamente equivalente a uma coluna **varbinary(8)**.
  
Use a coluna **rowversion** de uma linha para determinar facilmente se uma declaração de atualização foi executada para a linha desde a última vez em que ela foi lida. Se uma declaração de atualização tiver sido executada na linha, o valor de rowversion será atualizado. Se nenhuma instrução de atualização for executada na linha, o valor de rowversion será igual a quando ele foi lido anteriormente. Para retornar o valor de rowversion atual para um banco de dados, use [@@DBTS](../../t-sql/functions/dbts-transact-sql.md).
  
Adicione uma coluna **rowversion** à uma tabela para ajudar a manter a integridade do banco de dados quando vários usuários estão atualizando as linhas ao mesmo tempo. Você também pode querer saber quantas e quais linhas foram atualizadas sem consultar novamente a tabela.
  
Por exemplo, vamos suporte que você crie uma tabela chamada `MyTest`. Popule alguns dados na tabela executando as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir.
  
```sql
CREATE TABLE MyTest (myKey int PRIMARY KEY  
    ,myValue int, RV rowversion);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (2, 0);  
GO  
```  
  
Em seguida, você pode usar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] de amostra para implementar o controle de simultaneidade otimista na tabela `MyTest` durante a atualização. O script usa `<myRv>` para representar o valor de **rowversion** da última leitura da linha. Substitua o valor pelo valor real de **rowversion**. Um exemplo de um valor real de **rowversion** é `0x00000000000007D3`.
  
```sql
DECLARE @t TABLE (myKey int);  
UPDATE MyTest  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND RV = <myRv>;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  


Você também pode colocar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] de amostra em uma transação. Consultando a variável `@t` no escopo da transação, você pode recuperar a coluna `myKey` atualizada da tabela sem consultar a tabela `MyTest`.

Veja a seguir o mesmo exemplo usando a sintaxe de **carimbo de data/hora**. Substitua `<myTS>` por um **carimbo de data/hora real**.

```sql
CREATE TABLE MyTest2 (myKey int PRIMARY KEY  
    ,myValue int, TS timestamp);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (2, 0);  
GO  
DECLARE @t TABLE (myKey int);  
UPDATE MyTest2  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND TS = <myTS>;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
## <a name="see-also"></a>Confira também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)  
[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40;Transact-SQL&#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)
  
  
