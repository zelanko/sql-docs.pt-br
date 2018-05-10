---
title: Alterando o esquema de uma tabela temporal com versão do sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9dbe5a21-9335-4f8b-85fd-9da83df79946
caps.latest.revision: 13
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e370e98dbe0ce5c5f38cf4cac880abcb6500da5d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="changing-the-schema-of-a-system-versioned-temporal-table"></a>Alterando o esquema de uma tabela temporal com versão do sistema
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Use a instrução **ALTER TABLE** para adicionar, alterar ou remover uma coluna.  
  
## <a name="examples"></a>Exemplos  
 Aqui estão alguns exemplos que alteram o esquema de tabela temporal.  
  
```  
ALTER TABLE dbo.Department   
   ALTER COLUMN  DeptName varchar(100);   
  
ALTER TABLE dbo.Department   
   ADD WebAddress nvarchar(255) NOT NULL    
   CONSTRAINT DF_WebAddress DEFAULT 'www.mycompany.com';   
  
ALTER TABLE dbo.Department   
   ADD TempColumn INT;   
  
GO   
  
ALTER TABLE dbo.Department   
   DROP COLUMN TempColumn;  
  
/* Setting IsHidden property for period columns.   
Use ALTER COLUMN <period_column> DROP HIDDEN to clear IsHidden flag */  
  
ALTER TABLE dbo.Department   
   ALTER COLUMN SysStartTime ADD HIDDEN;   
  
ALTER TABLE dbo.Department   
   ALTER COLUMN SysEndTime ADD HIDDEN;  
  
```  
  
### <a name="important-remarks"></a>Observações importantes  
  
-   Permissão**CONTROL** nas tabelas atual e de histórico é necessária para alterar o esquema da tabela temporal.  
  
-   Durante uma operação de **ALTER TABLE** , o sistema mantém um bloqueio de esquema em ambas as tabelas.  
  
-   A alteração de esquema especificada é propagada para a tabela de histórico de forma apropriada (dependendo do tipo de alteração)  
  
-   Se você adicionar uma coluna não anulável ou alterar a coluna existente para se tornar não anulável, deve especificar o valor padrão para as linhas existentes. O sistema gerará um padrão adicional com o mesmo valor e o aplicará à tabela de histórico. A adição de **DEFAULT** a uma tabela não vazia é um tamanho da operação de dados em todas as edições diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition (no qual ela é uma operação de metadados).  
  
-   A adição de colunas varchar(max), nvarchar(max), varbinary(max) ou XML, será uma operação de atualização de dados em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Se o tamanho da linha após a adição da coluna exceder o limite de tamanho de linha, não será possível adicionar novas colunas online.  
  
-   Quando você estender uma tabela com uma nova coluna NOT NULL, considere descartar a restrição padrão na tabela de histórico, já que todas as colunas dessa tabela são preenchidas automaticamente pelo sistema.  
  
-   A opção online (**WITH (ONLINE = ON**) não tem nenhum efeito em **ALTER TABLE ALTER COLUMN** no caso da tabela temporal com controle de versão do sistema. A coluna ALTER não é executada online, independentemente de qual valor tenha sido especificado para a opção ONLINE.  
  
-   Você pode usar **ALTER COLUMN** para alterar a propriedade **IsHidden** das colunas de período.  
  
-   Não é possível usar **ALTER** direto para as alterações de esquema a seguir. Para esses tipos de alterações, defina **SYSTEM_VERSIONING = OFF**.  
  
    -   Adicionando uma coluna computada  
  
    -   Adicionando uma coluna **IDENTITY**  
  
    -   Adicionando uma coluna **SPARSE** ou alterando a coluna existente para **SPARSE**quando a tabela de histórico é definida como **DATA_COMPRESSION = PAGE** ou **DATA_COMPRESSION = ROW**, que é o padrão para a tabela de histórico.  
  
    -   Adicionando um **COLUMN_SET**  
  
    -   Adicionando uma coluna **ROWGUIDCOL** ou alterando a coluna existente para **ROWGUIDCOL**  
  
         O exemplo a seguir demonstra como alterar o esquema no qual a configuração **SYSTEM_VERSIONING = OFF** ainda é necessária (adicionando a coluna **IDENTITY** ).   
        Observe que este exemplo desabilita a verificação de consistência de dados. Essa verificação é desnecessária quando a alteração de esquema é feita dentro de uma transação, uma vez que nenhuma alteração de dados simultânea pode ocorrer.  
  
        ```  
        BEGIN TRAN   
        ALTER TABLE [dbo].[CompanyLocation] SET (SYSTEM_VERSIONING = OFF);   
        ALTER TABLE [CompanyLocation] ADD Cntr INT IDENTITY (1,1);   
        ALTER TABLE [dbo].[CompanyLocationHistory] ADD Cntr INT NOT NULL DEFAULT 0;   
        ALTER TABLE [dbo].[CompanyLocation]    
        SET    
        (   
        SYSTEM_VERSIONING = ON (HISTORY_TABLE = [dbo].[CompanyLocationHistory])   
        );   
        COMMIT ;  
  
        ```  
  
 
## <a name="see-also"></a>Consulte Também  
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [Introdução a Tabelas Temporais com Controle da Versão do Sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [Como criar uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [Modificando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [Consultando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [Interrompendo o controle de versão do sistema em uma tabela temporal com controle de versão do sistema](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  
