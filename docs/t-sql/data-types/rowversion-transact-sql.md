---
title: rowversion (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 57
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 47bcf3007657c1cf8f77c364aa21839cdd27d1ba
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="rowversion-transact-sql"></a>rowversion (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

É um tipo de dados que expõe números binários exclusivos, gerados automaticamente, em um banco de dados. **rowversion** geralmente é usado como um mecanismo para linhas de tabela de carimbo de versão. O tamanho de armazenamento é de 8 bytes. O **rowversion** tipo de dados é apenas um número incrementado e não preserva uma data ou hora. Para registrar uma data ou hora, use um **datetime2** tipo de dados.
  
## <a name="remarks"></a>Comentários  
Cada banco de dados tem um contador é incrementado para cada inserção ou uma operação de atualização é executada em uma tabela que contém um **rowversion** coluna no banco de dados. Esse contador é a rowversion do banco de dados. Isso controla uma hora relativa em um banco de dados, não uma hora real que pode ser associada a um relógio. Uma tabela pode ter apenas um **rowversion** coluna. Sempre que uma linha com um **rowversion** coluna é modificada ou inserida, o valor de rowversion do banco de dados incrementado é inserido no **rowversion** coluna. Essa propriedade torna uma **rowversion** coluna uma pobre candidata a chaves, especialmente as chaves primárias. Qualquer atualização feita na linha altera o valor de rowversion e, portanto, altera o valor de chave. Se a coluna estiver em uma chave primária, o valor da chave antiga não será mais válido e as chaves estrangeiras que fazem menção ao valor antigo não serão mais válidas. Se a tabela for mencionada em um cursor dinâmico, todas as atualizações alterarão a posição das linhas no cursor. Se a coluna for uma chave de índice, todas as atualizações na linha de dados também gerarão atualizações do índice.  O **rowversion** valor é incrementado com qualquer instrução update, mesmo se nenhum valor de linha é alterados. (Por exemplo, se um valor de coluna é 5 e uma instrução update define o valor para 5, essa ação é considerada uma atualização, embora não exista nenhuma alteração e o **rowversion** é incrementada.)
  
**carimbo de hora** é o sinônimo para o **rowversion** tipo de dados e está sujeito ao comportamento de dados sinônimos de tipo. Em instruções DDL, use **rowversion** em vez de **timestamp** sempre que possível. Para obter mais informações, consulte [sinônimos de tipos de dados &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
O [!INCLUDE[tsql](../../includes/tsql-md.md)] **timestamp** tipo de dados é diferente de **timestamp** tipo de dados definido no padrão ISO.
  
> [!NOTE]  
>  O **timestamp** sintaxe foi preterida. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
Em uma instrução CREATE TABLE ou ALTER TABLE, você não precisa especificar um nome de coluna para o **timestamp** tipo de dados, por exemplo:
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, timestamp);  
```  
  
Se você não especificar um nome de coluna, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] gera o **timestamp** nome de coluna; no entanto, o **rowversion** sinônimo não segue esse comportamento. Quando você usa **rowversion**, você deve especificar um nome de coluna, por exemplo:
  
```sql
CREATE TABLE ExampleTable2 (PriKey int PRIMARY KEY, VerCol rowversion) ;  
```  
  
> [!NOTE]  
>  Duplicar **rowversion** valores podem ser gerados usando a instrução SELECT INTO na qual um **rowversion** coluna está na lista de seleção. Não é recomendável usar **rowversion** dessa maneira.  
  
Um nulo **rowversion** coluna é semanticamente equivalente a um **binary (8)** coluna. Um valor nulo **rowversion** coluna é semanticamente equivalente a um **varbinary (8)** coluna.
  
Você pode usar o **rowversion** coluna de uma linha para determinar facilmente se a linha teve uma instrução update é executado em relação a ela desde a última vez que foi lido. Se uma instrução update é executada em relação a linha, o valor de rowversion será atualizado. Se nenhuma atualização instruções são executou em linha, o valor de rowversion é igual a quando ele foi lido anteriormente. Para retornar o valor de rowversion atual para um banco de dados, use [@@DBTS](../../t-sql/functions/dbts-transact-sql.md).
  
Você pode adicionar uma **rowversion** coluna a uma tabela para ajudar a manter a integridade do banco de dados quando vários usuários estão atualizando linhas ao mesmo tempo. Você também pode querer saber quantas e quais linhas foram atualizadas sem consultar novamente a tabela.
  
Por exemplo, vamos suporte que você crie uma tabela chamada `MyTest`. Você popula alguns dados na tabela, executando o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções.
  
```sql
CREATE TABLE MyTest (myKey int PRIMARY KEY  
    ,myValue int, RV rowversion);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (2, 0);  
GO  
```  
  
Em seguida, você pode usar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] de amostra para implementar o controle de simultaneidade otimista na tabela `MyTest` durante a atualização.
  
```sql
DECLARE @t TABLE (myKey int);  
UPDATE MyTest  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND RV = myValue;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
`myValue`é o **rowversion** valor de coluna para a linha que indica a última vez que você leia a linha. Esse valor deve ser substituído por real **rowversion** valor. Um exemplo de real **rowversion** valor é 0x00000000000007D3.
  
Você também pode colocar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] de amostra em uma transação. Consultando a variável `@t` no escopo da transação, você pode recuperar a coluna `myKey` atualizada da tabela, sem consultar a tabela `MyTes`t.
  
Este é o mesmo exemplo usando o **timestamp** sintaxe:
  
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
    AND TS = myValue;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
## <a name="see-also"></a>Consulte também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)  
[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40; Transact-SQL &#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)
  
  

