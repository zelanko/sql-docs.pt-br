---
title: "Índices para tabelas com otimização de memória | Microsoft Docs"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 06/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eecc5821-152b-4ed5-888f-7c0e6beffed9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b468f44444a9c6cc031ea892f44849db401e0ab7
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="indexes-for-memory-optimized-tables"></a>Índices para tabelas com otimização de memória
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
Este artigo descreve os tipos de índices que estão disponíveis para uma tabela com otimização de memória. O artigo:  
  
- Fornece exemplos de códigos curtos para demonstrar a sintaxe Transact-SQL.  
- Descreve como os índices com otimização de memória diferem dos índices tradicionais com base em disco.  
- Explica as circunstâncias em que cada tipo de índice com otimização de memória é melhor.  
  
  
Os índices de*hash* são abordados mais detalhadamente em um [artigo estreitamente relacionado](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md).  
  
  
Índices*columnstore* são abordados em [outro artigo](~/relational-databases/indexes/columnstore-indexes-overview.md).  
  
  
## <a name="a-syntax-for-memory-optimized-indexes"></a>A. Sintaxe para índices com otimização de memória  
  
Cada instrução CREATE TABLE para uma tabela com otimização de memória deve incluir entre uma e oito cláusulas para declarar índices. O índice deve ser um dos seguintes:  
  
- Índice de hash.  
- Índice não clusterizado (ou seja, a estrutura interna padrão de uma árvore B).  
  
  
Para ser declarada com DURABILITY = SCHEMA_AND_DATA padrão, a tabela com otimização de memória precisa ter uma chave primária. A cláusula PRIMARY KEY NONCLUSTERED na seguinte instrução CREATE TABLE atende a dois requisitos:  
  
- Fornece um índice para atender ao requisito mínimo de um índice na instrução CREATE TABLE.  
- Fornece a chave primária necessária para a cláusula SCHEMA_AND_DATA.  
  
  
  
    CREATE TABLE SupportEvent  
    (  
        SupportEventId   int NOT NULL  
            PRIMARY KEY NONCLUSTERED,  
        ...  
    )  
        WITH (  
            MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_AND_DATA);  
  
  
  
### <a name="a1-code-sample-for-syntax"></a>A.1 Exemplo de código de sintaxe  
  
Esta subseção contém um bloco de códigos Transact-SQL que demonstra a sintaxe para criar vários índices em uma tabela com otimização de memória. O código demonstra o seguinte:  
  
  
1. Crie uma tabela com otimização de memória.  
2. Use as instruções ALTER TABLE para adicionar dois índices.  
3. Insira algumas linhas de dados.  
  
  
  
    DROP TABLE IF EXISTS SupportEvent;  
    go  
  
    CREATE TABLE SupportEvent  
    (  
      SupportEventId   int               not null   identity(1,1)  
        PRIMARY KEY NONCLUSTERED,  
  
      StartDateTime        datetime2     not null,  
      CustomerName         nvarchar(16)  not null,  
      SupportEngineerName  nvarchar(16)      null,  
      Priority             int               null,  
      Description          nvarchar(64)      null  
    )  
      WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA_AND_DATA);  
    go  
      
        --------------------  
      
    ALTER TABLE SupportEvent  
      ADD CONSTRAINT constraintUnique_SDT_CN  
        UNIQUE NONCLUSTERED (StartDateTime DESC, CustomerName);  
    go  
  
    ALTER TABLE SupportEvent  
      ADD INDEX idx_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 64);  -- Nonunique.  
    go  
      
        --------------------  
      
    INSERT INTO SupportEvent  
        (StartDateTime, CustomerName, SupportEngineerName, Priority, Description)  
      VALUES  
        ('2016-02-25 13:40:41:123', 'Abby', 'Zeke', 2, 'Display problem.'     ),  
        ('2016-02-25 13:40:41:323', 'Ben' , null  , 1, 'Cannot find help.'    ),  
        ('2016-02-25 13:40:41:523', 'Carl', 'Liz' , 2, 'Button is gray.'      ),  
        ('2016-02-25 13:40:41:723', 'Dave', 'Zeke', 2, 'Cannot unhide column.');  
    go  
  
  
  
## <a name="b-nature-of-memory-optimized-indexes"></a>B. Natureza de índices com otimização de memória  
  
Em uma tabela com otimização de memória, cada índice também tem otimização de memória. Existem várias diferenças entre um índice em um índice com otimização de memória e um índice tradicional em uma tabela baseada em disco.  
  
Cada índice com otimização de memória existe apenas na memória ativa. O índice não tem representação no disco.  
  
- Os índices com otimização de memória são recriados quando o banco de dados fica online novamente.  
  
  
Quando uma instrução SQL UPDATE modifica dados em uma tabela com otimização de memória, as alterações correspondentes em seus índices não são gravadas no log.  
  
  
As entradas em um índice com otimização de memória contém um endereço de memória direto para a linha na tabela.  
  
- Ao contrário, as entradas em um índice de árvore B tradicional em disco contêm um valor de chave que o sistema precisa usar primeiramente para localizar o endereço de memória da linha da tabela associada.  
  
  
Os índices com otimização de memória não têm páginas fixas como os índices com base em disco.  
  
- Eles não acumulam o tipo tradicional de fragmentação em uma página e, portanto, não têm nenhum fator de preenchimento.  
  
## <a name="c-duplicate-index-key-values"></a>C. Valores de chave de índice duplicados

Valores de chave de índice duplicados podem afetar o desempenho de operações em tabelas com otimização de memória. Grandes números de duplicatas (por exemplo, mais de 100) tornam ineficiente o trabalho de manutenção de um índice, pois as cadeias duplicadas devem ser percorridas na maioria das operações de índice. O impacto pode ser visto em operações INSERT, UPDATE e DELETE em tabelas com otimização de memória. Esse problema é mais visível no caso de índices de hash, devido ao menor custo por operação de índices de hash e à interferência de grandes cadeias duplicadas com a cadeia de colisão de hash. Para reduzir a duplicação em um índice, use um índice não clusterizado e adicione outras colunas (por exemplo, da chave primária) ao final da chave de índice para reduzir o número de duplicatas.

Considere, por exemplo, uma tabela Customers com uma chave primária em CustomerId e um índice na coluna CustomerCategoryID. Normalmente, haverá muitos clientes em uma determinada categoria e, portanto, muitos valores duplicados para uma determinada chave no índice em CustomerCategoryID. Nesse cenário, a prática recomendada é usar um índice não clusterizado em (CustomerCategoryID, CustomerId). Esse índice pode ser usado para consultas que usam um predicado que envolvem CustomerCategoryID e não há duplicação e, portanto, não causam ineficiência na manutenção do índice.

A consulta a seguir mostra o número médio de valores de chave de índice duplicado para o índice em `CustomerCategoryID` na tabela `Sales.Customers`, no banco de dados de exemplo [WideWorldImporters](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx).

```Transact-SQL
    SELECT AVG(row_count) FROM
       (SELECT COUNT(*) AS row_count 
        FROM Sales.Customers
        GROUP BY CustomerCategoryID) a
```

Para avaliar o número médio de duplicatas de chave de índice para sua própria tabela e índice, substitua `Sales.Customers` pelo nome da tabela e substitua `CustomerCategoryID` pela lista de colunas de chave de índice.

## <a name="d-comparing-when-to-use-each-index-type"></a>D. Comparando quando usar cada tipo de índice  
  
  
A natureza de cada consulta específica determina que tipo de índice é a melhor opção.  

Ao implementar tabelas com otimização de memória em um aplicativo existente, a recomendação geral é iniciar com índices não clusterizados, já que as funcionalidades se assemelham mais às funcionalidades de índices clusterizados e não clusterizados tradicionais em tabelas baseadas em disco. 
  
  
### <a name="d1-strengths-of-nonclustered-indexes"></a>D.1 Pontos fortes dos índices não clusterizados  
  
  
Um índice não clusterizado é preferível em vez de um índice de hash quando:  
  
- As consultas têm uma cláusula ORDER BY na coluna indexada.  
- Consultas nas quais apenas as colunas à esquerda de um índice de várias colunas são testadas.  
- As consultas testam a coluna indexada usando uma cláusula WHERE com:  
  - Uma desigualdade: *WHERE StatusCode != 'Done'*  
  - Um intervalo de valores: *WHERE Quantity >= 100*  
  
  
Em todos os SELECTs a seguir, um índice não clusterizado é preferível em vez de um índice de hash:  
  
  
  
    SELECT col2 FROM TableA  
        WHERE StartDate > DateAdd(day, -7, GetUtcDate());  
      
    SELECT col3 FROM TableB  
        WHERE ActivityCode != 5;  
      
    SELECT StartDate, LastName  
        FROM TableC  
        ORDER BY StartDate;  
      
    SELECT IndexKeyColumn2  
        FROM TableD  
        WHERE IndexKeyColumn1 = 42;  
  
  
  
### <a name="d2-strengths-of-hash-indexes"></a>D.2 Pontos fortes dos índices de hash  
  
  
Um [índice de hash](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) é preferível em vez de um índice não clusterizado quando:  
  
- As consultas testam as colunas indexadas pelo uso de uma cláusula WHERE com uma igualdade exata em todas as colunas de chave de índice, como mostrado a seguir:  
  
  
  
    SELECT col9 FROM TableZ  
        WHERE Z_Id = 2174;  
  
  
  
### <a name="d3-summary-table-to-compare-index-strengths"></a>D.3 Tabela de resumo para comparar os pontos fortes dos índices  
  
  
A tabela a seguir lista todas as operações com suporte dos diferentes tipos de índice.  
  
  
| Operação | Com otimização de memória, <br/> hash | Com otimização de memória, <br/> não clusterizado | Com base em disco, <br/> (não) clusterizado |  
| :-------- | :--------------------------- | :----------------------------------- | :------------------------------------ |  
| Verificação de índice, recuperar todas as linhas da tabela. | Sim | Sim | Sim |  
| Busca de índice em predicados de igualdade (=). | Sim <br/> (A chave completa é necessária.) | Sim  | Sim |  
| Busca de índice em predicados de desigualdade e intervalo <br/> (>, <, <=, >=, entre). | Não <br/> (Resulta em uma verificação de índice.) | Sim | Sim |  
| Recuperar linhas em uma ordem de classificação que corresponda à definição do índice. | Não | Sim | Sim |  
| Recuperar linhas em uma ordem de classificação que corresponda ao inverso da definição do índice. | Não | Não | Sim |  
  
  
Na tabela, Sim significa que o índice pode atender à solicitação com eficiência e Não significa que o índice não pode satisfazer a solicitação com eficiência.  

