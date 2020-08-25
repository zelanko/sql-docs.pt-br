---
description: Modificando dados em uma tabela temporal com controle da versão do sistema
title: Modificando dados em uma tabela temporal com controle de versão do sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 5f398470-c531-47b5-84d5-7c67c27df6e5
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 79ae1efd305215d0e64287e6c0a7ad7aa9a70a36
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646434"
---
# <a name="modifying-data-in-a-system-versioned-temporal-table"></a>Como modificar dados em uma tabela temporal com controle da versão do sistema


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]


Os dados em uma tabela temporal com controle da versão do sistema são modificados usando as instruções DML regulares com uma diferença importante: os dados de coluna do período não podem ser modificados diretamente. Quando os dados são atualizados, eles recebem a versão anterior de cada linha atualizada inserida na tabela de histórico. Quando dados são excluídos, a exclusão é lógica, com a linha movida para a tabela de histórico da tabela atual - ele não será excluído permanentemente.

## <a name="inserting-data"></a>Inserindo dados

Quando você insere novos dados, precisa levar em conta as colunas **PERIOD** se não forem **HIDDEN**. Você também pode usar alternância de partição com tabelas temporais com controle da versão do sistema.

### <a name="insert-new-data-with-visible-period-columns"></a>Inserir novos dados com colunas de período visíveis

Você pode construir sua instrução **INSERT** quando tiver colunas visíveis **PERIOD** da seguinte maneira para considerar as novas colunas **PERIOD** :

- Se você especificar a lista de colunas em sua instrução **INSERT** , poderá omitir as colunas **PERIOD** porque o sistema irá gerar valores automaticamente para essas colunas.

  ```sql
  -- Insert with column list and without period columns
  INSERT INTO [dbo].[Department]
    (  [DeptID]
          , [DeptName]
          , [ManagerID]
          ,[ParentDeptID]
    )
       VALUES
         (  10
         , 'Marketing'
         , 101
         , 1
         ) ;
   ```

- Se você especificar as colunas **PERIOD** na lista de colunas na sua instrução **INSERT**, precisará especificar **DEFAULT** como seu valor.

  ```sql
  INSERT INTO [dbo].[Department]
    (  [DeptID]
          , [DeptName]
          , [ManagerID]
          , [ParentDeptID]
          , SysStartTime
          , SysEndTime
    )
       VALUES
         (  11
          , 'Sales'
          , 101
          , 1
          , default
          , default) ;
   ```

- Se você não especificar a lista de colunas em sua instrução **INSERT** , especifique **DEFAULT** para colunas **PERIOD** .

  ```sql
    -- Insert without column list and DEFAULT values for period columns
    INSERT INTO [dbo].[Department]
    VALUES(12, 'Production', 101, 1, default, default);

  ```

### <a name="insert-data-into-a-table-with-hidden-period-columns"></a>Inserir dados em uma tabela com colunas de período HIDDEN

Se as colunas **PERIOD** forem especificadas como HIDDEN, você só precisará especificar os valores para as colunas visíveis quando usar INSERT sem especificar a lista de colunas. Não é necessário levar em conta a nova coluna **PERIOD** em sua instrução **INSERT** . Esse comportamento garante que seus aplicativos herdados continuem a funcionar quando você habilita o controle de versão do sistema em tabelas que se beneficiam disso.

```sql
CREATE TABLE [dbo].[CompanyLocation]
(
     [LocID] [int] IDENTITY(1,1) NOT NULL PRIMARY KEY
   , [LocName] [varchar](50) NOT NULL
   , [City] [varchar](50) NOT NULL
   , [SysStartTime] [datetime2] GENERATED ALWAYS AS ROW START HIDDEN NOT NULL
   , [SysEndTime] [datetime2] GENERATED ALWAYS AS ROW END HIDDEN NOT NULL
   , PERIOD FOR SYSTEM_TIME ([SysStartTime], [SysEndTime])
)
WITH ( SYSTEM_VERSIONING = ON );
GO
INSERT INTO [dbo].[CompanyLocation]
VALUES ('Headquarters', 'New York');

```

### <a name="inserting-data-using-partition-switch"></a>Inserindo dados usando PARTITION SWITCH

Se a tabela atual estiver particionada, você poderá usar a alternância de partição como um mecanismo eficiente para carregar dados em uma partição vazia ou em várias partições em paralelo.

A tabela de preparo é usada na instrução **PARTITION SWITCH IN** com uma tabela temporal com controle da versão do sistema deve ter **SYSTEM_TIME PERIOD** definido, mas não precisa ser uma tabela temporal com controle da versão do sistema.
Isso garante que as verificações de consistência temporais são executadas durante a inserção de dados em uma tabela de preparo ou quando o período SYSTEM_TIME é adicionado a uma tabela de preparo preenchida previamente.

```sql
/*Create staging table with period definition for SWITCH IN temporal table*/
CREATE TABLE [dbo].[Staging_Department_Partition2]
(
     [DeptID] [int] NOT NULL
   , [DeptName] [varchar](50) NOT NULL
   , [ManagerID] [int] NULL
   , [ParentDeptID] [int] NULL
   , [SysStartTime] [datetime2] GENERATED ALWAYS AS ROW START NOT NULL
   , [SysEndTime] [datetime2] GENERATED ALWAYS AS ROW END NOT NULL
   , PERIOD FOR SYSTEM_TIME ( [SysStartTime], [SysEndTime] )
) ON [PRIMARY]

/*Create aligned primary key*/
ALTER TABLE [dbo].[Staging_Department_Partition2]
ADD CONSTRAINT [Staging_Department_Partition2_PK]
   PRIMARY KEY CLUSTERED
   ( [DeptID] ASC )
   ON [PRIMARY]
  
/*
Create and enforce constraints for partition boundaries.
Partition 2 contains rows with DeptID > 100 and DeptID <=200
*/
ALTER TABLE [dbo].[Staging_Department_Partition2]
   WITH CHECK ADD  CONSTRAINT [chk_staging_Department_partition_2]
   CHECK  ([DeptID]>N'100' AND [DeptID]<=N'200')
ALTER TABLE [dbo].[Staging_Department_Partition2]
   CHECK CONSTRAINT [chk_staging_Department_partition_2]

/*Load data into staging table*/
INSERT INTO [dbo].[staging_Department] ([DeptID],[DeptName],[ManagerID],[ParentDeptID])
VALUES (101,'D101',1,NULL)

/*Use PARTITION SWITCH IN to efficiently add data to current table */
ALTER TABLE [Staging_Department]
SWITCH TO [dbo].[Department] PARTITION 2;
```

Se você tentar realizar o PARTITION SWITCH de uma tabela sem definição de período, obterá uma mensagem de erro: `Msg 13577, Level 16, State 1, Line 25 ALTER TABLE SWITCH statement failed on table 'MyDB.dbo.Staging_Department_2015_09_26' because target table has SYSTEM_TIME PERIOD while source table does not have it.`

## <a name="updating-data"></a>Atualizar dados

Atualize os dados na tabela atual com uma instrução **UPDATE** regular. Você pode atualizar dados na tabela atual da tabela de histórico para o cenário de "oops". No entanto, não é possível atualizar as colunas **PERIOD** nem atualizar dados diretamente na tabela de histórico enquanto **SYSTEM_VERSIONING = ON**.

Defina **SYSTEM_VERSIONING = OFF** e atualize as linhas da tabela atual e de histórico, mas tenha em mente que, dessa maneira, o sistema não guardará o histórico de alterações.

### <a name="updating-the-current-table"></a>Atualizando a tabela atual

Neste exemplo, a coluna ManagerID é atualizada para cada linha onde DeptID = 10. As colunas **PERIOD** não são referenciadas de qualquer maneira.

```sql
UPDATE [dbo].[Department] SET [ManagerID] = 501 WHERE [DeptID] = 10
```

No entanto, você não pode atualizar uma coluna **PERIOD** e não pode atualizar a tabela de histórico. Neste exemplo, uma tentativa de atualizar uma coluna **PERIOD** gera um erro.

```sql
UPDATE [dbo].[Department]
SET SysStartTime = '2015-09-23 23:48:31.2990175'
WHERE DeptID = 10 ;

Msg 13537, Level 16, State 1, Line 3
Cannot update GENERATED ALWAYS columns in table 'TmpDev.dbo.Department'.
```

### <a name="updating-the-current-table-from-the-history-table"></a>Atualizando a tabela atual da tabela de histórico

Você pode usar **UPDATE** na tabela atual para reverter o estado real da linha para um estado válido em um ponto específico no passado (reversão para uma "última versão de linha boa conhecida"). O exemplo a seguir mostra a reversão para os valores na tabela de histórico em 25-04-2015 onde o DeptID = 10.

```sql
UPDATE Department
SET DeptName = History.DeptName
FROM Department
FOR SYSTEM_TIME AS OF '2015-04-25' AS History
WHERE History.DeptID = 10
AND Department.DeptID = 10 ;
```

## <a name="deleting-data"></a>Excluindo dados

Exclua os dados na tabela atual com uma instrução **DELETE** regular. A coluna do período final para linhas excluídas será preenchida com a hora de início da transação subjacente. Não é possível excluir linhas diretamente da tabela de histórico enquanto **SYSTEM_VERSIONING = ON**. Defina **SYSTEM_VERSIONING = OFF** e exclua as linhas da tabela atual e de histórico, mas tenha em mente que, dessa maneira, o sistema não guardará o histórico de alterações. Não há suporte para**TRUNCATE**, **SWITCH PARTITION OUT** da tabela atual nem para **SWITCH PARTITION IN** da tabela de histórico quando **SYSTEM_VERSIONING = ON**.

## <a name="using-merge-to-modify-data-in-temporal-table"></a>Usando MERGE para modificar dados em tabela temporal

A operação**MERGE** não tem suporte com as mesmas limitações que as instruções **INSERT** e **UPDATE** têm em relação a colunas **PERIOD** .

```sql
CREATE TABLE DepartmentStaging (DeptId INT, DeptName varchar(50));
GO
INSERT INTO DepartmentStaging VALUES (1, 'Company Management');
INSERT INTO DepartmentStaging VALUES (10, 'Science & Research');
INSERT INTO DepartmentStaging VALUES (15, 'Process Management');

MERGE dbo.Department AS target
USING (SELECT DeptId, DeptName FROM DepartmentStaging) AS source (DeptId, DeptName)
ON (target.DeptId = source.DeptId)
WHEN MATCHED THEN
    UPDATE
   SET DeptName = source.DeptName
WHEN NOT MATCHED THEN
   INSERT (DeptName)
   VALUES (source.DeptName);
```

## <a name="next-steps"></a>Próximas etapas

- [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)
- [Criando uma tabela temporal com controle de versão do sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [Consultando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [Alterando o esquema de uma tabela temporal com versão do sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
- [Interrompendo o controle de versão do sistema em uma tabela temporal com controle de versão do sistema](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)
