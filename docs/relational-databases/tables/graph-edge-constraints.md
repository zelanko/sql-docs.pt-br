---
title: Restrições de borda de grafo | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current||=azuresqldb-current'
ms.openlocfilehash: 9a02f34464c19bd51af0e68a1385b223e1c9d669
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920112"
---
# <a name="edge-constraints"></a>Restrições do Microsoft Edge

[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]

É possível usar restrições de borda para impor a integridade dos dados e uma semântica específica às tabelas de borda no banco de dados de gráfico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="edge-constraints"></a><a name="Connection"></a> Restrições de borda

Na primeira versão dos recursos de gráfico, as tabelas de borda não impunham nada aos pontos de extremidade da borda. Ou seja, uma borda em um banco de dados de gráfico podia conectar qualquer nó a qualquer outro nó, independentemente do tipo.

Esta versão introduz restrições de borda, que permitem aos usuários adicionar restrições a suas tabelas de borda, imponto assim uma semântica específica e mantendo a integridade dos dados. Quando uma nova borda é adicionada a uma tabela de borda com restrições de borda, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] impõe que os nós que a borda está tentando conectar existem nas tabelas de nó adequadas. Também é garantido que um nó não possa ser removido se ele ainda for referenciado por uma borda.

### <a name="edge-constraint-clauses"></a>Cláusulas de restrição de borda

Cada restrição de borda é composta por uma ou mais cláusulas de restrição de borda. Uma cláusula de restrição de borda é o par de nós DE e PARA que a borda em questão poderia conectar.

Considere que você tem os nós `Product` e `Customer` em seu gráfico e você usa a borda `Bought` para conectar a esses nós. A cláusula de restrição de borda especifica o par de nós DE e PARA e a direção da borda. Nesse caso, a cláusula de restrição de borda será `Customer` PARA `Product`. Ou seja, será permitido inserir um `Bought` que vai de um `Customer` para `Product`. Tentativas de inserir uma borda que vai de `Product` para `Customer` falham.

- Uma cláusula de restrição de borda contém um par de tabelas de nós DE e PARA a que a restrição de borda é imposta.
- Os usuários podem especificar várias cláusulas de restrição de borda por restrição de borda, que serão aplicadas como uma disjunção.
- Se várias restrições de borda forem criadas em uma única tabela de borda, as bordas deverão atender a TODAS as restrições para serem permitidas.

### <a name="indexes-on-edge-constraints"></a>Índices em restrições de borda

Criar uma restrição de borda não cria automaticamente um índice correspondente nas colunas `$from_id` e `$to_id` da tabela de borda. Criar manualmente um índice em um par `$from_id`, `$to_id` é recomendado se você tem consultas de pesquisa de ponto ou carga de trabalho de OLTP.

### <a name="on-delete-referential-actions-on-edge-constraints"></a>Ações referenciais ON DELETE em restrições de borda
As ações em cascata em uma restrição de borda permitem que os usuários definam as ações que o mecanismo de banco de dados usa quando um usuário exclui os nós que a borda especificada conecta. As ações referenciais a seguir podem ser definidas:  
*NO ACTION*   
O mecanismo de banco de dados gera um erro quando você tenta excluir um nó que tem bordas de conexão.  

*CASCADE*   
Quando um nó é excluído do banco de dados, as bordas de conexão são excluídas.  

## <a name="working-with-edge-constraints"></a>Trabalhando com restrições de borda

É possível definir uma restrição de borda no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]. É possível definir uma restrição de borda apenas em uma tabela de borda do gráfico. Para criar, excluir ou modificar uma restrição de borda, você deve ter a permissão **ALTER** para a tabela.

### <a name="create-edge-constraints"></a>Criar restrições de borda

Os exemplos a seguir mostram como criar restrições de borda em tabelas novas ou existentes

#### <a name="to-create-an-edge-constraint-on-a-new-edge-table"></a>Para criar uma restrição de borda em uma nova tabela de borda

O exemplo a seguir cria uma restrição de borda na tabela de borda **bought**.

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      ,CustomerName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      ,ProductName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
         ,CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product) ON DELETE NO ACTION
   )
   AS EDGE;
   ```

#### <a name="defining-referential-actions-on-a-new-edge-table"></a>Definir ações referenciais em uma nova tabela de borda 

O exemplo a seguir cria uma restrição de borda na tabela de borda **bought** e define a ação referencial ON DELETE CASCADE. 

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      ,CustomerName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      ,ProductName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
         ,CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product) ON DELETE CASCADE
   )
   AS EDGE;
   ```

#### <a name="to-add-edge-constraint-to-an-existing-edge-table"></a>Para adicionar uma restrição de borda a uma tabela de borda existente

O exemplo a seguir usa ALTER TABLE para adicionar uma restrição de borda à tabela de borda **bought**.

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY,
      , CustomerName VARCHAR(100)
   )
   AS NODE;
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
   )
   AS EDGE;
GO
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product);
```  

#### <a name="create-a-new-edge-constraint-on-existing-edge-table-with-additional-edge-constraint-clauses"></a>Criar uma nova restrição de borda na tabela de borda existente com cláusulas adicionais de restrição de borda

O exemplo a seguir usa o comando `ALTER TABLE` para adicionar uma nova restrição de borda com cláusulas de restrição de borda adicionais na tabela de borda **bought**.
  
```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Supplier
   (
      ID INTEGER PRIMARY KEY
      , SupplierName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
      , CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
   )
   AS EDGE;
-- Drop the existing edge constraint first and then create a new one.
ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT;
GO
-- User ALTER TABLE to create a new edge constraint.
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product, Supplier TO Product);
```  

No exemplo anterior, há duas cláusulas de restrição de borda na restrição *EC_BOUGHT1*, uma que conecta **Customer** a **Product** e a outra que conecta **Supplier** a **Product**. Essas duas cláusulas são aplicadas em disjunção. Ou seja, uma determinada borda precisa satisfazer uma dessas duas cláusulas para ser permitida na tabela de borda.

#### <a name="creating-a-new-edge-constraint-on-existing-edge-table-with-new-edge-constraint-clause"></a>Criando uma nova restrição de borda na tabela de borda existente com uma nova cláusula de restrição de borda

O exemplo a seguir usa o comando `ALTER TABLE` para adicionar uma nova restrição de borda com uma nova cláusula de restrição de borda na tabela de borda **bought**.
  
 ```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Supplier
   (
      ID INTEGER PRIMARY KEY
      , SupplierName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT,
         CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
   )
   AS EDGE;
GO
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Supplier TO Product);
 ```  

No exemplo anterior, criamos duas restrições de borda separadas na tabela de borda **bought**, *EC_BOUGHT* e *EC_BOUGHT1*. Essas duas restrições de borda têm cláusulas de restrição de borda diferentes. Se uma tabela de borda tiver mais de uma restrição de borda, uma determinada borda precisará satisfazer **TODAS** as restrições para ser permitida na tabela de borda. Como nenhuma borda será capaz de satisfazer *EC_BOUGHT* e *EC_BOUGHT1* neste caso, a tabela de borda **bought** deverá permanecer vazia.

Para que inserções tenham êxito nessa tabela de borda, uma das restrições de borda deverá ser removida, ou ambas deverão ser removidas e uma nova restrição de borda com as duas cláusulas de restrição deverá ser criada.

```sql
-- Drop the existing edge constraint first and then create a new one.
ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT;
GO
ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT1;
GO
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT_NEW CONNECTION (Customer TO Product, Supplier TO Product);
GO
```  

Para que uma determinada borda seja permitida na borda **bought**, ela precisará atender a qualquer uma das cláusulas de restrição de borda na restrição *EC_BOUGHT_NEW*. Portanto, qualquer borda que estiver tentando conectar nós **Customer** a **Product** ou **Supplier** a **Product** válidos, serão permitidos.

### <a name="delete-edge-constraints"></a>Excluir restrições de borda

O exemplo a seguir primeiro identifica o nome da restrição de borda e depois exclui a restrição.  
  
```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   ) AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
      , CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
    AS EDGE;
GO
-- Return the name of edge constraint.
SELECT name  
   FROM sys.edge_constraints  
   WHERE type = 'EC' AND parent_object_id = OBJECT_ID('bought');  
GO  
-- Delete the primary key constraint.  
ALTER TABLE bought
DROP CONSTRAINT EC_BOUGHT;
```  

### <a name="modify-edge-constraints"></a>Modificar restrições de borda

Para modificar uma restrição de borda usando o Transact-SQL, exclua primeiramente a restrição de borda existente e, em seguida, recrie-a com a nova definição.


### <a name="view-edge-constraints"></a>Exibir restrições de borda

[!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).

O exemplo retorna todas as restrições de borda e suas propriedades para a tabela de borda `bought` no banco de dados tempdb.  

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Supplier
   (
      ID INTEGER PRIMARY KEY
      , SupplierName VARCHAR(100)
   )
   AS NODE;
   GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;

-- CREATE edge table with edge constraints.
CREATE TABLE bought
   (
      PurchaseCount INT
      , CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product, Supplier TO Product)
   )
   AS EDGE;

-- Query sys.edge_constraints and sys.edge_constraint_clauses to view
-- edge constraint properties.
SELECT
   EC.name AS edge_constraint_name
   , OBJECT_NAME(EC.parent_object_id) AS edge_table_name
   , OBJECT_NAME(ECC.from_object_id) AS from_node_table_name
   , OBJECT_NAME(ECC.to_object_id) AS to_node_table_name
   , is_disabled
   , is_not_trusted
FROM sys.edge_constraints EC
   INNER JOIN sys.edge_constraint_clauses ECC
   ON EC.object_id = ECC.object_id
WHERE EC.parent_object_id = object_id('bought');
```  

## <a name="related-tasks"></a>Tarefas relacionadas

[CREATE TABLE (Grafo do SQL)](../../t-sql/statements/create-table-sql-graph.md)  
[ALTER TABLE table_constraint](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)  

Para saber mais sobre a tecnologia de grafo no SQL Server, confira [Processamento de grafo com o SQL Server e Banco de Dados SQL do Azure](../graphs/sql-graph-overview.md?view=sql-server-2017).

