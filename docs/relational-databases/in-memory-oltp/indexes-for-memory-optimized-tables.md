---
title: Índices para tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.component: in-memory-oltp
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eecc5821-152b-4ed5-888f-7c0e6beffed9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2b2ce7ce7e891e0750f80637c3ebc42176167834
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="indexes-on-memory-optimized-tables"></a>Índices em tabelas com otimização de memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Todas as tabelas com otimização de memória devem ter, pelo menos, um índice, porque são os índices que conectam as linhas. Em uma tabela com otimização de memória, cada índice também tem otimização de memória. Existem várias diferenças entre um índice em um índice com otimização de memória e um índice tradicional em uma tabela baseada em disco:  

- As linhas de dados não são armazenadas em páginas e, portanto, não há nenhuma coleção de páginas ou extensões, nenhuma partição ou unidade de alocação que pode ser referenciada para obter todas as páginas de uma tabela. Há o conceito de páginas de índice para um dos tipos de índices disponíveis, mas elas são armazenadas de modo diferente dos índices para tabelas baseadas em disco. Eles não acumulam o tipo tradicional de fragmentação em uma página e, portanto, não têm nenhum fator de preenchimento.
- As alterações feitas nos índices em tabelas com otimização de memória durante a manipulação de dados nunca são gravadas em disco. Apenas as linhas de dados e as alterações nos dados são gravadas no log de transações. 
- Os índices com otimização de memória são recriados quando o banco de dados fica online novamente. 

Todos os índices em tabelas com otimização de memória são criados com base nas definições de índice durante a recuperação do banco de dados.

O índice deve ser um dos seguintes:  
  
- Índice de hash  
- Índice não clusterizado com otimização de memória (ou seja, a estrutura interna padrão de uma árvore B) 
  
Os índices de *hash* são abordados mais detalhadamente em [Índices de hash para tabelas com otimização de memória](../../relational-databases/sql-server-index-design-guide.md#hash_index).
Os índices *não clusterizados* são abordados mais detalhadamente em [Índice não clusterizado para tabelas com otimização de memória](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index).  
Índices*columnstore* são abordados em [outro artigo](../../relational-databases/indexes/columnstore-indexes-overview.md).  

## <a name="syntax-for-memory-optimized-indexes"></a>Sintaxe para índices com otimização de memória  
  
Cada instrução CREATE TABLE para uma tabela com otimização de memória deve incluir um índice, seja explicitamente por meio de um INDEX ou implicitamente por meio de uma restrição PRIMARY KEY ou UNIQUE.
  
Para ser declarada com a DURABILITY = SCHEMA\_AND_DATA padrão, a tabela com otimização de memória deve ter uma chave primária. A cláusula PRIMARY KEY NONCLUSTERED na seguinte instrução CREATE TABLE atende a dois requisitos:  
  
- Fornece um índice para atender ao requisito mínimo de um índice na instrução CREATE TABLE.  
- Fornece a chave primária necessária para a cláusula SCHEMA\_AND_DATA.  

    ```sql
    CREATE TABLE SupportEvent  
    (  
        SupportEventId   int NOT NULL  
            PRIMARY KEY NONCLUSTERED,  
        ...  
    )  
        WITH (  
            MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA\_AND_DATA);  
    ```
> [!NOTE]  
> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] têm um limite de 8 índices por tabela com otimização de memória ou tipo de tabela. A partir do [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], não há mais um limite no número de índices específicos para as tabelas com otimização de memória e os tipos de tabela.
  
### <a name="code-sample-for-syntax"></a>Exemplo de código de sintaxe  
  
Esta subseção contém um bloco de códigos Transact-SQL que demonstra a sintaxe para criar vários índices em uma tabela com otimização de memória. O código demonstra o seguinte:  
  
1. Crie uma tabela com otimização de memória.  
2. Use as instruções ALTER TABLE para adicionar dois índices.  
3. Insira algumas linhas de dados.  
   
    ```sql
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
        DURABILITY = SCHEMA\_AND_DATA);  
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
        ('2016-02-23 13:40:41:123', 'Abby', 'Zeke', 2, 'Display problem.'     ),  
        ('2016-02-24 13:40:41:323', 'Ben' , null  , 1, 'Cannot find help.'    ),  
        ('2016-02-25 13:40:41:523', 'Carl', 'Liz' , 2, 'Button is gray.'      ),  
        ('2016-02-26 13:40:41:723', 'Dave', 'Zeke', 2, 'Cannot unhide column.');  
    go 
    ``` 
  
## <a name="duplicate-index-key-values"></a>Valores de chave de índice duplicados

Valores de chave de índice duplicados podem afetar o desempenho de operações em tabelas com otimização de memória. Grandes números de duplicatas (por exemplo, mais de 100) tornam ineficiente o trabalho de manutenção de um índice, pois as cadeias duplicadas devem ser percorridas na maioria das operações de índice. O impacto pode ser visto nas operações `INSERT`, `UPDATE` e `DELETE` em tabelas com otimização de memória. 

Esse problema é mais visível no caso de índices de hash, devido ao menor custo por operação de índices de hash e à interferência de cadeias grandes duplicadas com a cadeia de colisão de hash. Para reduzir a duplicação em um índice, use um índice não clusterizado e adicione outras colunas (por exemplo, da chave primária) ao final da chave de índice para reduzir o número de duplicatas. Para obter mais informações sobre colisões de hash, consulte [Índices de hash para tabelas com otimização de memória](../../relational-databases/sql-server-index-design-guide.md#hash_index).

Por exemplo, considere uma tabela `Customers` com uma chave primária em `CustomerId` e um índice na coluna `CustomerCategoryID`. Normalmente, haverá muitos clientes em uma determinada categoria e, portanto, muitos valores duplicados para uma determinada chave no índice em CustomerCategoryID. Nesse cenário, a melhor prática é usar um índice não clusterizado em `(CustomerCategoryID, CustomerId)`. Esse índice pode ser usado para consultas que usam um predicado que envolve `CustomerCategoryID` e não há duplicação e, portanto, não causam ineficiência na manutenção do índice.

A consulta a seguir mostra o número médio de valores de chave de índice duplicado para o índice em `CustomerCategoryID` na tabela `Sales.Customers`, no banco de dados de exemplo [WideWorldImporters](../../sample/world-wide-importers/wide-world-importers-documentation.md).

```sql
SELECT AVG(row_count) FROM
    (SELECT COUNT(*) AS row_count 
        FROM Sales.Customers
        GROUP BY CustomerCategoryID) a
```

Para avaliar o número médio de duplicatas de chave de índice para sua própria tabela e índice, substitua `Sales.Customers` pelo nome da tabela e substitua `CustomerCategoryID` pela lista de colunas de chave de índice.

## <a name="comparing-when-to-use-each-index-type"></a>Comparando quando usar cada tipo de índice  
  
A natureza de cada consulta específica determina que tipo de índice é a melhor opção.  

Ao implementar tabelas com otimização de memória em um aplicativo existente, a recomendação geral é iniciar com índices não clusterizados, já que as funcionalidades se assemelham mais às funcionalidades de índices clusterizados e não clusterizados tradicionais em tabelas baseadas em disco. 
  
### <a name="recommendations-for-nonclustered-index-use"></a>Recomendações para o uso do índice não clusterizado  
  
Um índice não clusterizado é preferível em vez de um índice de hash quando:  
  
- As consultas têm uma cláusula `ORDER BY` na coluna indexada.  
- Consultas nas quais apenas as colunas à esquerda de um índice de várias colunas são testadas.  
- As consultas testam a coluna indexada usando uma cláusula `WHERE` com:  
  - Uma desigualdade: `WHERE StatusCode != 'Done'`  
  - Uma verificação do intervalo de valores: `WHERE Quantity >= 100`  
  
Em todos os SELECTs a seguir, um índice não clusterizado é preferível em vez de um índice de hash:  

```sql
SELECT CustomerName, Priority, Description 
FROM SupportEvent  
WHERE StartDateTime > DateAdd(day, -7, GetUtcDate());  
    
SELECT CustomerName, Priority, Description 
FROM SupportEvent  
WHERE CustomerName != 'Ben';  
    
SELECT StartDateTime, CustomerName  
FROM SupportEvent  
ORDER BY StartDateTime;  
    
SELECT CustomerName  
FROM SupportEvent  
WHERE StartDateTime = '2016-02-26';  
```
  
### <a name="recommendations-for-hash-index-use"></a>Recomendações para o uso do índice de hash   
  
[Índices de hash](../../relational-databases/sql-server-index-design-guide.md#hash_index) são usados principalmente para pesquisas de ponto e não para verificações de intervalo.

Um índice de hash é preferível a um índice não clusterizado quando as consultas usam predicados de igualdade e a cláusula `WHERE` é mapeada para todas as colunas de chave de índice, como no seguinte exemplo:  
  
```sql
SELECT CustomerName 
FROM SupportEvent  
WHERE SupportEngineerName = 'Liz';
```  

### <a name="multi-column-index"></a>Índice de várias colunas  
  
O índice de várias colunas pode ser um índice não clusterizado ou um índice de hash. Suponha que as colunas de índice sejam col1 e col2. Considerando a seguinte instrução `SELECT`, apenas o índice não clusterizado será útil para o otimizador de consulta:  
  
```sql
SELECT col1, col3  
FROM MyTable_memop  
WHERE col1 = 'dn';  
```

O índice de hash precisa da cláusula `WHERE` para especificar um teste de igualdade para cada uma das colunas em sua chave. Caso contrário, o índice de hash não será útil para o otimizador de consulta.  
  
Nenhum tipo de índice é útil se a cláusula `WHERE` especifica somente a segunda coluna na chave de índice.  

### <a name="summary-table-to-compare-index-use-scenarios"></a>Tabela de resumo de comparação dos cenários de uso de índices  
  
A tabela a seguir lista todas as operações com suporte dos diferentes tipos de índice. *Sim* significa que o índice pode atender à solicitação com eficiência e *Não* significa que o índice não pode atender à solicitação com eficiência. 
  
| Operação | Com otimização de memória, <br/> hash | Com otimização de memória, <br/> não clusterizado | Com base em disco, <br/> (não) clusterizado |  
| :-------- | :--------------------------- | :----------------------------------- | :------------------------------------ |  
| Verificação de índice, recuperar todas as linhas da tabela. | Sim | Sim | Sim |  
| Busca de índice em predicados de igualdade (=). | Sim <br/> (A chave completa é necessária.) | Sim  | Sim |  
| Busca de índice em predicados de desigualdade e intervalo <br/> (>, <, <=, >=, `BETWEEN`). | não <br/> (Resulta em uma verificação de índice.) | Sim <sup>1</sup> | Sim |  
| Recuperar linhas em uma ordem de classificação que corresponda à definição do índice. | não | Sim | Sim |  
| Recuperar linhas em uma ordem de classificação que corresponda ao inverso da definição do índice. | não | não | Sim |  

<sup>1</sup> Para um índice não clusterizado com otimização de memória, a chave completa não é necessária para a execução de uma busca de índice.  

## <a name="automatic-index-and-statistics-management"></a>Índice automático e gerenciamento de estatísticas

Aproveite soluções como a [Desfragmentação de índice adaptável](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) para gerenciar automaticamente a desfragmentação de índice e as atualizações de estatísticas em um ou mais bancos de dados. Este procedimento escolhe automaticamente se deve recompilar ou reorganizar um índice de acordo com seu nível de fragmentação, entre outros parâmetros, e atualizar as estatísticas com um limite linear.

## <a name="Additional_Reading"></a> Consulte também   
 [Guia de criação de índice do SQL Server](../../relational-databases/sql-server-index-design-guide.md)   
 [Índices de hash para tabelas com otimização de memória](../../relational-databases/sql-server-index-design-guide.md#hash_index)   
 [Índices não clusterizados para tabelas com otimização de memória](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)    
 [Desfragmentação de índice adaptável](http://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)  
