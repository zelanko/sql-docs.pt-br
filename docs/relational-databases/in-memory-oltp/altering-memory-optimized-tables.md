---
title: Alterando tabelas com otimização de memória | Microsoft Docs
description: Saiba como a instrução ALTER TABLE executa alterações de esquema e de índice em tabelas com otimização de memória. Combine as operações ADD, DROP e ALTER em uma só instrução.
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 690b70b7-5be1-4014-af97-54e531997839
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: db339d9063378b29f6902f7e52e3006ac57295b7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85776071"
---
# <a name="altering-memory-optimized-tables"></a>Alterando tabelas com otimização de memória

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Alterações de esquema e de índice em tabelas com otimização de memória podem ser executadas usando a instrução ALTER TABLE. No SQL Server 2016 e no Banco de Dados SQL do Azure as operações ALTER TABLE em tabelas com otimização de memória são OFFLINE, o que significa que a tabela não está disponível para consulta enquanto a operação está em andamento. O aplicativo de banco de dados pode continuar em execução e qualquer operação que acessa a tabela será bloqueada até que o processo de alteração seja concluído. É possível combinar várias operações ADD, DROP ou ALTER em uma única instrução ALTER TABLE.

> [!IMPORTANT]
> A Instância Gerenciada do Banco de Dados SQL do Azure não oferece suporte a tabelas com otimização de memória na camada de serviço de Uso Geral.
  
## <a name="alter-table"></a>ALTER TABLE  

A sintaxe ALTER TABLE é usada para fazer alterações no esquema de tabela, bem como para adicionar, excluir e recompilar índices. Índices são considerados parte da definição de tabela:  
  
- A sintaxe ALTER TABLE... ADD/DROP/ALTER INDEX só tem suporte para tabelas com otimização de memória.  
  
- Sem o uso de uma instrução ALTER TABLE, não há suporte para as instruções [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) e [PAD_INDEX](../../t-sql/statements/alter-table-index-option-transact-sql.md) para índices em tabelas com otimização de memória.  
  
Os tipos de alteração a seguir têm suporte:  
  
- Alterando o número de buckets  
  
- Adicionando e removendo um índice  
  
- Alterando, adicionando e removendo uma coluna  
  
- Adicionando e removendo uma restrição  
  
 Para obter mais informações sobre a funcionalidade ALTER TABLE e a sintaxe completa, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
## <a name="schema-bound-dependency"></a>Dependência associada a esquema

 Procedimentos armazenados compilados de modo nativo devem ser associados a esquema, o que significa que eles têm uma dependência associada a esquema nas tabelas com otimização de memória que eles acessam e nas colunas às quais eles fazem referência. A dependência associada a esquema é uma relação entre duas entidades que impede que a entidade referenciada seja cancelada ou modificada de modo incompatível enquanto existir a entidade mencionada.  
  
 Por exemplo, se um procedimento armazenado compilado de modo nativo associado a esquema fizer referência a uma coluna *c1* da tabela *mytable*, a coluna *c1* não poderá ser removida. Da mesma forma, se houver um procedimento desse tipo com uma instrução INSERT sem uma lista de colunas (por exemplo, `INSERT INTO dbo.mytable VALUES (...)`), nenhuma coluna da tabela poderá ser removida.  

## <a name="logging-of-alter-table-on-memory-optimized-tables"></a>Log de ALTER TABLE em tabelas com otimização de memória

Em uma tabela com otimização de memória, a maioria dos cenários de ALTER TABLE agora é executada em paralelo e resulta em uma otimização das gravações no log de transações. A otimização é obtida apenas registrando as alterações de metadados no log de transações. No entanto, as operações de ALTER TABLE a seguir são executadas em thread único e não têm otimização de log.

A operação single-threaded, nesse caso, registraria todo o conteúdo da tabela alterada no log de transações. A seguir, a lista das operações de thread único:

- Alterar ou adicionar uma coluna para usar um tipo de objeto grande (LOB): nvarchar(max), varchar(max) ou varbinary(max).

- Adicionar ou remover um índice COLUMNSTORE.

- Quase tudo o que afeta uma [coluna fora de linha](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md).

  - Fazer com que uma coluna na linha mova-se para fora de linha.
  - Fazer com que uma coluna fora de linha mova-se para dentro da linha.
  - Crie uma nova coluna fora de linha.
  - *Exceção:* o aumento de uma coluna já fora de linha é registrado de forma otimizada.
  
## <a name="examples"></a>Exemplos

O exemplo a seguir altera o número de buckets de um índice de hash existente. Isso recompila o índice de hash com o novo número de buckets, enquanto outras propriedades do índice de hash permanecem as mesmas.  

```sql
ALTER TABLE Sales.SalesOrderDetail_inmem
       ALTER INDEX imPK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID  
              REBUILD WITH (BUCKET_COUNT=67108864);  
GO
```

O exemplo a seguir adiciona uma coluna com uma restrição NOT NULL e com uma definição DEFAULT, e usa WITH VALUES para fornecer valores para cada linha existente na tabela. Se WITH VALUES não for usado, cada linha terá o valor NULL na nova coluna.  

```sql
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD Comment NVARCHAR(100) NOT NULL DEFAULT N'' WITH VALUES;  
GO
```

O exemplo a seguir adiciona uma restrição de chave primária a uma coluna existente.  

```sql
CREATE TABLE dbo.UserSession (
   SessionId int not null,
   UserId int not null,
   CreatedDate datetime2 not null,
   ShoppingCartId int,
   index ix_UserId nonclustered hash (UserId) with (bucket_count=400000)
)
WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_ONLY) ;  
GO  
  
ALTER TABLE dbo.UserSession  
       ADD CONSTRAINT PK_UserSession PRIMARY KEY NONCLUSTERED (SessionId);  
GO
```

O exemplo a seguir remove um índice.  

```sql
ALTER TABLE Sales.SalesOrderDetail_inmem  
       DROP INDEX ix_ModifiedDate;  
GO
```  

O exemplo a seguir adiciona um índice.  

```sql  
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD INDEX ix_ModifiedDate (ModifiedDate);  
GO  
```  

O exemplo a seguir adiciona várias colunas, com um índice e restrições.  

```sql
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD    CustomerID int NOT NULL DEFAULT -1 WITH VALUES,  
              ShipMethodID int NOT NULL DEFAULT -1 WITH VALUES,  
              INDEX ix_Customer (CustomerID);  
GO  
```

<a name="logging-of-alter-table-on-memory-optimized-tables-124"></a>

## <a name="see-also"></a>Consulte Também  

[Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
