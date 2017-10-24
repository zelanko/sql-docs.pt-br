---
title: Ao lado de valor (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/19/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NEXT_VALUE_TSQL
- NEXT
- NEXT VALUE
- NEXT VALUE FOR
- NEXT_TSQL
- NEXT_VALUE_FOR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NEXT VALUE FOR function
- sequence number object, NEXT VALUE FOR function
ms.assetid: 92632ed5-9f32-48eb-be28-a5e477ef9076
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aab8020fa04b978d7ec1b657fe0a1084123dfb48
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="next-value-for-transact-sql"></a>NEXT VALUE FOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Gera um número de sequência do objeto de sequência especificado.  
  
 Para obter uma discussão completa de criação e o uso de sequências, consulte [números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md). Use [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) para gerar reservar um intervalo de números de sequência.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
NEXT VALUE FOR [ database_name . ] [ schema_name . ]  sequence_name  
   [ OVER (<over_order_by_clause>) ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 O nome do banco de dados que contém o objeto de sequência.  
  
 *schema_name*  
 O nome do esquema que contém o objeto de sequência.  
  
 *sequence_name*  
 O nome do objeto de sequência que gera o número.  
  
 *over_order_by_clause*  
 Determina a ordem na qual o valor da sequência é atribuído às linhas de uma partição. Para obter mais informações, consulte [a cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna um número usando o tipo da sequência.  
  
## <a name="remarks"></a>Comentários  
 O **NEXT VALUE FOR** função pode ser usada em procedimentos armazenados e gatilhos.  
  
 Quando o **NEXT VALUE FOR** função é usada em uma consulta ou restrição padrão, se o mesmo objeto de sequência é usado mais de uma vez, ou se o mesmo objeto de sequência é usado na instrução que fornece os valores e em uma restrição padrão está sendo executado, será retornado o mesmo valor para todas as colunas que referenciam a mesma sequência em uma linha no conjunto de resultados.  
  
 O **NEXT VALUE FOR** função é não determinística e só é permitida em contextos em que o número de valores de sequência gerados é bem definido. Abaixo está a definição de quantos valores serão usados para cada objeto de sequência referenciado em uma determinada instrução:  
  
-   **Selecione** -para cada objeto de sequência referenciado, um novo valor é gerado uma vez por linha no resultado da instrução.  
  
-   **INSERIR** ... **VALORES** -para cada objeto de sequência referenciado, um novo valor é gerado uma vez para cada linha inserida na instrução.  
  
-   **ATUALIZAÇÃO** -para cada objeto de sequência referenciado, um novo valor é gerado para cada linha que está sendo atualizada pela instrução.  
  
-   Instruções de procedimentos (como **DECLARE**, **definir**, etc.)-para cada objeto de sequência referenciado, um novo valor é gerado para cada instrução.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 O **NEXT VALUE FOR** função não pode ser usada nas seguintes situações:  
  
-   Quando um banco de dados está em modo somente leitura.  
  
-   Como um argumento para uma função com valor de tabela.  
  
-   Como um argumento para uma função de agregação.  
  
-   Em subconsultas inclusive expressões de tabela comuns e tabelas derivadas.  
  
-   Em exibições, em funções definidas pelo usuário, ou em colunas computadas.  
  
-   Em uma instrução usando o **DISTINCT**, **união**, **UNION ALL**, **EXCEPT** ou **INTERSECT** operador.  
  
-   Em uma instrução usando o **ORDER BY** cláusula, a menos que **NEXT VALUE FOR** ... **SOBRE** (**ORDER BY** ...) é usado.  
  
-   Nas seguintes cláusulas: **BUSCAR**, **sobre**, **saída**, **ON**, **PIVOT**,  **UNPIVOT**, **Agrupar por**, **HAVING**, **de computação**, **COMPUTE BY**, ou **deFORXML**.  
  
-   Em expressões condicionais usando **caso**, **escolha**, **COALESCE**, **IIF**, **ISNULL**, ou  **NULLIF**.  
  
-   Em um **valores** cláusula não é parte de um **inserir** instrução.  
  
-   Na definição de uma restrição de verificação.  
  
-   Na definição de uma regra ou objeto padrão. (Pode ser usado em uma restrição padrão.)  
  
-   Como padrão em um tipo de tabela definido pelo usuário.  
  
-   Em uma instrução que usa **superior**, **deslocamento**, ou quando o **ROWCOUNT** opção é definida.  
  
-   No **onde** cláusula de uma instrução.  
  
-   Em um **mesclar** instrução. (Exceto quando o **NEXT VALUE FOR** função é usada em uma restrição padrão na tabela de destino e o padrão é usado no **criar** instrução o **mesclar** instrução.)  
  
## <a name="using-a-sequence-object-in-a-default-constraint"></a>Usando um objeto de sequência em uma restrição padrão  
 Ao usar o **NEXT VALUE FOR** função em uma restrição padrão, as seguintes regras se aplicam:  
  
-   Um único objeto de sequência pode ser referenciado de restrições padrão em várias tabelas.  
  
-   A tabela e o objeto de sequência devem residir no mesmo banco de dados.  
  
-   O usuário que adiciona a restrição padrão deve ter permissão de REFERENCES no objeto de sequência.  
  
-   Um objeto de sequência que é referenciado de uma restrição padrão não pode ser removido antes da restrição padrão ser removida.  
  
-   A mesma sequência de número é retornada para todas as colunas em uma linha se diversas restrições padrão usam o mesmo objeto de sequência, ou se o mesmo objeto de sequência for usado na instrução que fornece os valores, e em uma restrição padrão que é executada.  
  
-   Referências a **NEXT VALUE FOR** função em uma restrição padrão não é possível especificar o **sobre** cláusula.  
  
-   Um objeto de sequência referenciado em uma restrição padrão pode ser alterado.  
  
-   No caso de um `INSERT … SELECT` ou `INSERT … EXEC` instrução onde os dados inseridos vêm de uma consulta usando um **ORDER BY** cláusula, os valores retornados pelo **NEXT VALUE FOR** função será gerados na ordem especificada pelo **ORDER BY** cláusula.  
  
## <a name="using-a-sequence-object-with-an-over-order-by-clause"></a>Usando um objeto de sequência com uma cláusula OVER ORDER BY  
 O **NEXT VALUE FOR** function dá suporte à geração de valores de sequência classificados aplicando a **sobre** cláusula para o **NEXT VALUE FOR** chamar. Usando o **sobre** cláusula, um usuário garante que os valores retornados são gerados na ordem do **sobre** da cláusula **ordem B**Subcláusula Y. As seguintes regras adicionais se aplicam ao usar o **NEXT VALUE FOR** funcionar com o **sobre** cláusula:  
  
-   Diversas chamadas para o **NEXT VALUE FOR** de função para o mesmo gerador de sequência em uma única instrução deve usar o mesmo **sobre** definição de cláusula.  
  
-   Diversas chamadas para o **NEXT VALUE FOR** função que referência geradores de sequência diferentes em uma única instrução podem ter diferentes **sobre** definições de cláusula.  
  
-   Um **sobre** cláusula aplicada para o **NEXT VALUE FOR** função não oferece suporte a **PARTITION BY** Subcláusula.  
  
-   Se todas as chamadas para o **NEXT VALUE FOR** funcionar em um **selecione** instrução Especifica o **sobre** cláusula, um **ORDER BY** cláusula pode ser usada em o **selecione** instrução.  
  
-   O **sobre** cláusula é permitida com o **NEXT VALUE FOR** funcionam quando usados em um **selecione** instrução ou `INSERT … SELECT …` instrução. Usar o **sobre** cláusula com o **NEXT VALUE FOR** função não é permitida em **atualização** ou **mesclar** instruções.  
  
-   Se outro processo estiver acessando o objeto de sequência ao mesmo tempo, os números retornados poderão ter intervalos.  
  
## <a name="metadata"></a>Metadados  
 Para obter informações sobre sequências, consulte o [sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md) exibição do catálogo.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer **atualização** permissão no objeto de sequência ou o esquema da sequência. Para obter um exemplo de concessão de permissão, consulte o exemplo F posteriormente neste tópico.  
  
### <a name="ownership-chaining"></a>Encadeamento de propriedade  
 Objetos de sequência oferecem suporte a encadeamento de propriedade. Se o objeto de sequência tiver o mesmo proprietário que o procedimento armazenado de chamada, gatilho ou tabela (tendo um objeto de sequência como uma restrição padrão), nenhuma verificação de permissão será exigida no objeto de sequência. Se o objeto de sequência não tiver o mesmo proprietário que o procedimento armazenado de chamada, gatilho ou tabela, uma verificação de permissão será exigida no objeto de sequência.  
  
 Quando o **NEXT VALUE FOR** função é usada como um valor padrão em uma tabela, os usuários precisam **inserir** permissão na tabela, e **atualização** permissão no objeto de sequência , para inserir dados usando o padrão.  
  
-   Se a restrição padrão tiver o mesmo proprietário que o objeto de sequência, nenhuma permissão será exigida no objeto de sequência quando a restrição padrão for chamada.  
  
-   Se a restrição padrão e o objeto de sequência não tiverem o mesmo proprietário, as permissões serão exigidas no objeto de sequência mesmo que seja chamada através de uma restrição padrão.  
  
### <a name="audit"></a>Auditoria  
 Para auditar o **NEXT VALUE FOR** funcionar, monitore o SCHEMA_OBJECT_ACCESS_GROUP.  
  
## <a name="examples"></a>Exemplos  
 Para obter exemplos de como criar sequências e usando o **NEXT VALUE FOR** função para gerar números de sequência, consulte [números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 Os exemplos a seguir usam uma sequência chamada `CountBy1` em um esquema chamado `Test`. Execute a seguinte instrução para criar a sequência `Test.CountBy1`. Os exemplos C e E usam o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], portanto, a sequência `CountBy1` é criada naquele banco de dados.  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE SCHEMA Test;  
GO  
  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="a-using-a-sequence-in-a-select-statement"></a>A. Usando uma sequência em uma instrução select  
 O exemplo a seguir cria uma sequência chamada `CountBy1`, que aumenta em incrementos de um cada vez que é utilizada.  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1 AS FirstUse;  
SELECT NEXT VALUE FOR Test.CountBy1 AS SecondUse;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FirstUse  
1  
  
SecondUse  
2
```  
  
### <a name="b-setting-a-variable-to-the-next-sequence-value"></a>B. Definindo uma variável como o próximo valor de sequência  
 O exemplo a seguir demonstra três modos de definir uma variável como o próximo valor de um número de sequência.  
  
```  
DECLARE @myvar1 bigint = NEXT VALUE FOR Test.CountBy1  
DECLARE @myvar2 bigint ;  
DECLARE @myvar3 bigint ;  
SET @myvar2 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar3 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar1 AS myvar1, @myvar2 AS myvar2, @myvar3 AS myvar3 ;  
GO  
```  
  
### <a name="c-using-a-sequence-with-a-ranking-window-function"></a>C. Usando uma sequência com uma função de janela de classificação  
  
```  
USE AdventureWorks2012 ;  
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 OVER (ORDER BY LastName) AS ListNumber,  
    FirstName, LastName  
FROM Person.Contact ;  
GO  
```  
  
### <a name="d-using-the-next-value-for-function-in-the-definition-of-a-default-constraint"></a>D. Usando a função NEXT VALUE FOR na definição de uma restrição padrão  
 Usando o **NEXT VALUE FOR** oferece suporte a função na definição de uma restrição padrão. Para obter um exemplo do uso de **NEXT VALUE FOR** em uma **CREATE TABLE** instrução, consulte o exemplo C[números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md). O exemplo a seguir usa `ALTER TABLE` para adicionar uma sequência como um padrão em uma tabela atual.  
  
```  
CREATE TABLE Test.MyTable  
(  
    IDColumn nvarchar(25) PRIMARY KEY,  
    name varchar(25) NOT NULL  
) ;  
GO  
  
CREATE SEQUENCE Test.CounterSeq  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
ALTER TABLE Test.MyTable  
    ADD   
        DEFAULT N'AdvWorks_' +   
        CAST(NEXT VALUE FOR Test.CounterSeq AS NVARCHAR(20))   
        FOR IDColumn;  
GO  
  
INSERT Test.MyTable (name)  
VALUES ('Larry') ;  
GO  
  
SELECT * FROM Test.MyTable;  
GO  
```  
  
### <a name="e-using-the-next-value-for-function-in-an-insert-statement"></a>E. Usando uma função NEXT VALUE FOR em uma instrução INSERT  
 O exemplo a seguir cria uma tabela chamada `TestTable` e usa a função `NEXT VALUE FOR` para inserir uma linha.  
  
```  
CREATE TABLE Test.TestTable  
     (CounterColumn int PRIMARY KEY,  
    Name nvarchar(25) NOT NULL) ;   
GO  
  
INSERT Test.TestTable (CounterColumn,Name)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Syed') ;  
GO  
  
SELECT * FROM Test.TestTable;   
GO  
  
```  
  
### <a name="e-using-the-next-value-for-function-with-select--into"></a>E. Usando a função NEXT VALUE FOR com SELECT … INTO  
 O exemplo a seguir usa o `SELECT … INTO` instrução para criar uma tabela chamada `Production.NewLocation` e usa o `NEXT VALUE FOR` função para numerar cada linha.  
  
```  
USE AdventureWorks2012 ;   
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 AS LocNumber, Name   
    INTO Production.NewLocation  
    FROM Production.Location ;  
GO  
  
SELECT * FROM Production.NewLocation ;  
GO  
```  
  
### <a name="f-granting-permission-to-execute-next-value-for"></a>F. Concedendo permissão para executar NEXT VALUE FOR  
 O exemplo a seguir concede **atualização** permissão a um usuário chamado `AdventureWorks\Larry` permissão para executar `NEXT VALUE FOR` usando o `Test.CounterSeq` sequência.  
  
```  
GRANT UPDATE ON OBJECT::Test.CounterSeq TO [AdventureWorks\Larry] ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criar SEQUÊNCIA de &#40; Transact-SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [Números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  

