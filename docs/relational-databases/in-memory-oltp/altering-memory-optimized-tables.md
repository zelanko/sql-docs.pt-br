---
title: "Alterando tabelas com otimização de memória | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 690b70b7-5be1-4014-af97-54e531997839
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e4a8b3f4dabec4d46813c570e1a04fd469075a66
ms.lasthandoff: 04/11/2017

---
# <a name="altering-memory-optimized-tables"></a>Alterando tabelas com otimização de memória
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Alterações de esquema e de índice em tabelas com otimização de memória podem ser executadas usando a instrução ALTER TABLE. O aplicativo de banco de dados pode continuar em execução e qualquer operação que acessa a tabela será bloqueada até que o processo de alteração seja concluído.  
  
## <a name="alter-table"></a>ALTER TABLE  
 
A sintaxe ALTER TABLE é usada para fazer alterações no esquema de tabela, bem como para adicionar, excluir e recompilar índices. Índices são considerados parte da definição de tabela:  
  
-   A sintaxe ALTER TABLE... ADD/DROP/ALTER INDEX só tem suporte para tabelas com otimização de memória.  
  
-   Sem o uso de uma instrução ALTER TABLE, as instruções CREATE INDEX, DROP INDEX e ALTER INDEX *não* têm suporte para índices em tabelas com otimização de memória.  
  
 A seguir, a sintaxe para as cláusulas ADD, DROP e ALTER INDEX na instrução ALTER TABLE.  
  
```
| ADD   
     {   
        <column_definition>  
      | <table_constraint>  
      | <table_index>    
     } [ ,...n ]  
  
| DROP   
     {  
         [ CONSTRAINT ]   
         {   
              constraint_name   
         } [ ,...n ]  
         | COLUMN   
         {  
              column_name   
         } [ ,...n ]  
         | INDEX   
         {  
              index_name   
         } [ ,...n ]  
     } [ ,...n ]  
  
| ALTER INDEX index_name  
     {   
         REBUILD WITH ( <rebuild_index_option> )     
     }  
}  
```  
  
 Os tipos de alteração a seguir têm suporte.  
  
-   Alterando o número de buckets  
  
-   Adicionando e removendo um índice  
  
-   Alterando, adicionando e removendo uma coluna  
  
-   Adicionando e removendo uma restrição  
  
 Para obter mais informações sobre a funcionalidade ALTER TABLE e a sintaxe completa, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
## <a name="schema-bound-dependency"></a>Dependência associada a esquema  
 Procedimentos armazenados compilados de modo nativo devem ser associados a esquema, o que significa que eles têm uma dependência associada a esquema nas tabelas com otimização de memória que eles acessam e nas colunas às quais eles fazem referência. A dependência associada a esquema é uma relação entre duas entidades que impede que a entidade referenciada seja cancelada ou modificada de modo incompatível enquanto existir a entidade mencionada.  
  
 Por exemplo, se um procedimento armazenado compilado de modo nativo associado a esquema fizer referência a uma coluna *c1* da tabela *mytable*, a coluna *c1* não poderá ser removida. Da mesma forma, se houver um procedimento desse tipo com uma instrução INSERT sem uma lista de colunas (por exemplo, `INSERT INTO dbo.mytable VALUES (...)`), nenhuma coluna da tabela poderá ser removida.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o número de buckets de um índice de hash existente. Isso recompila o índice de hash com o novo número de buckets, enquanto outras propriedades do índice de hash permanecem as mesmas.  
  
```tsql
ALTER TABLE Sales.SalesOrderDetail_inmem   
       ALTER INDEX imPK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID  
              REBUILD WITH (BUCKET_COUNT=67108864);  
GO
```
  
 O exemplo a seguir adiciona uma coluna com uma restrição NOT NULL e com uma definição DEFAULT, e usa WITH VALUES para fornecer valores para cada linha existente na tabela. Se WITH VALUES não for usado, cada linha terá o valor NULL na nova coluna.  
  
```tsql  
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD Comment NVARCHAR(100) NOT NULL DEFAULT N'' WITH VALUES;  
GO
```  
  
 O exemplo a seguir adiciona uma restrição de chave primária a uma coluna existente.  
  
```tsql
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
  
```tsql
ALTER TABLE Sales.SalesOrderDetail_inmem  
       DROP INDEX ix_ModifiedDate;  
GO
```  
  
 O exemplo a seguir adiciona um índice.  
  
```tsql  
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD INDEX ix_ModifiedDate (ModifiedDate);  
GO  
```  
  
 O exemplo a seguir adiciona várias colunas, com um índice e restrições.  
  
```tsql
ALTER TABLE Sales.SalesOrderDetail_inmem  
       ADD    CustomerID int NOT NULL DEFAULT -1 WITH VALUES,  
              ShipMethodID int NOT NULL DEFAULT -1 WITH VALUES,  
              INDEX ix_Customer (CustomerID);  
GO  
```


<a name="logging-of-alter-table-on-memory-optimized-tables-124"></a>

## <a name="logging-of-alter-table-on-memory-optimized-tables"></a>Log de ALTER TABLE em tabelas com otimização de memória


Em uma tabela com otimização de memória, a maioria dos cenários de ALTER TABLE agora é executada em paralelo e resulta em uma otimização das gravações no log de transações. A otimização é que apenas as alterações de metadados são gravadas no log de transações. No entanto, as operações de ALTER TABLE a seguir são executadas em thread único e não têm otimização de log.

As operações de thread único requerem que todo o conteúdo da tabela alterada seja gravado no log. A seguir, a lista das operações de thread único:

- Alterar ou adicionar uma coluna para usar um tipo de objeto grande (LOB): nvarchar(max), varchar(max) ou varbinary(max).

- Adicionar ou remover um índice COLUMNSTORE.

- Quase tudo o que afeta uma [coluna fora de linha](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md).

    - Fazer com que uma coluna na linha mova-se para fora de linha.

    - Fazer com que uma coluna fora de linha mova-se para dentro da linha.

    - Crie uma nova coluna fora de linha.

    - *Exceção:* o aumento de uma coluna já fora de linha é registrado de forma otimizada.


## <a name="see-also"></a>Consulte também  

[Tabelas com otimização de memória](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  


