---
title: Criando uma tabela temporal com controle da versão do sistema | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 21e6d74f-711f-40e6-a8b7-85f832c5d4b3
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eae7dfb2a198cf7cb3b1563f8f5b35c5fbb0b4eb
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52409613"
---
# <a name="creating-a-system-versioned-temporal-table"></a>Como criar uma tabela temporal com controle da versão do sistema
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Há três maneiras de criar uma tabela temporal com controle da versão do sistema relacionadas ao modo como a tabela de histórico é especificada:  
  
-   Tabela temporal com uma tabela de histórico anônimo: especifique o esquema da tabela atual e deixe o sistema criar a tabela de histórico correspondente com o nome gerado automaticamente.  
  
-   Tabela temporal com uma tabela de histórico padrão: especifique o nome do esquema de tabela de histórico e o nome da tabela e deixe o sistema criar tabela de histórico nesse esquema.  
  
-   Tabela temporal com uma tabela de histórico definida pelo usuário criada antecipadamente: crie a tabela de histórico que melhor atenda às suas necessidades e faça referência a essa tabela durante a criação da tabela temporal.  
  
## <a name="creating-a-temporal-table-with-an-anonymous-history-table"></a>Criação de uma tabela temporal com uma tabela de histórico anônimo  
 Criar uma tabela temporal com uma tabela de histórico "anônimo" é uma opção conveniente para a criação rápida de objeto, especialmente em ambientes de teste e de protótipos. Também é a maneira mais simples de criar uma tabela temporal, já que não exige qualquer parâmetro na cláusula **SYSTEM_VERSIONING**. No exemplo a seguir, uma nova tabela é criada com o controle de versão do sistema habilitado, sem definir o nome da tabela de histórico.  
  
```  
CREATE TABLE Department   
(    
     DeptID int NOT NULL PRIMARY KEY CLUSTERED  
   , DeptName varchar(50) NOT NULL  
   , ManagerID INT  NULL  
   , ParentDeptID int NULL  
   , SysStartTime datetime2 GENERATED ALWAYS AS ROW START NOT NULL  
   , SysEndTime datetime2 GENERATED ALWAYS AS ROW END NOT NULL  
   , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)    
WITH (SYSTEM_VERSIONING = ON)   
;  
```  
  
### <a name="important-remarks"></a>Observações importantes  
  
-   Uma tabela temporal com controle da versão do sistema deve ter uma chave primária definida e ter exatamente um **PERIOD FOR SYSTEM_TIME** definido com duas colunas datetime2, declaradas como **GENERATED ALWAYS AS ROW START / END**  
  
-   Supõe-se que as colunas **PERIOD** sempre são não anuláveis, mesmo se a nulidade não for especificada. Se as colunas  **PERIOD** forem definidas explicitamente como anuláveis, a instrução **CREATE TABLE** falhará.  
  
-   A tabela de histórico deve sempre ser alinhada ao esquema com a tabela atual ou temporal, em termos de número de colunas, nomes de coluna, ordenação e tipos de dados.  
  
-   Uma tabela de histórico anônimo é criada automaticamente no mesmo esquema que a tabela temporal ou atual.  
  
-   O nome da tabela de histórico anônimo tem o seguinte formato: *MSSQL_TemporalHistoryFor_<current_temporal_table_object_id>_[suffix]*. O sufixo é opcional e será adicionado somente se a primeira parte do nome da tabela não for exclusivo.  
  
-   A tabela de histórico é criada como uma tabela rowstore. Se possível, a compactação de PÁGINA será aplicada, caso contrário, a tabela de histórico será descompactada. Por exemplo, algumas configurações de tabela, como as colunas ESPARSAS, não permitem a compactação.  
  
-   Um índice clusterizado padrão é criado para a tabela de histórico com um nome gerado automaticamente no formato *IX_<history_table_name>*. O índice clusterizado contém as colunas **PERIOD** (início, fim).  
  
-   Para criar a tabela atual como uma tabela com otimização de memória, consulte [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md).  
  
## <a name="creating-a-temporal-table-with-a-default-history-table"></a>Criação de uma tabela temporal com uma tabela de histórico padrão  
 A criação de uma tabela temporal com uma tabela de histórico padrão é uma opção conveniente quando você deseja controlar a nomenclatura e ainda depende do sistema para criar a tabela de histórico com a configuração padrão. No exemplo a seguir, uma nova tabela é criada com o controle de versão do sistema habilitado, com o nome da tabela de histórico definido explicitamente.  
  
```  
CREATE TABLE Department   
(    
     DeptID int NOT NULL PRIMARY KEY CLUSTERED  
   , DeptName varchar(50) NOT NULL  
   , ManagerID INT  NULL  
   , ParentDeptID int NULL  
   , SysStartTime datetime2 GENERATED ALWAYS AS ROW START NOT NULL  
   , SysEndTime datetime2 GENERATED ALWAYS AS ROW END NOT NULL  
   , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)     
)   
WITH    
   (   
      SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory)   
   )   
;  
```  
  
### <a name="important-remarks"></a>Observações importantes  
 A tabela de histórico é criada usando as mesmas regras que se aplicam à criação de uma tabela de histórico "anônimo", com as seguintes regras se aplicam especificamente à tabela de histórico nomeada.  
  
-   O nome do esquema é obrigatório para o parâmetro **HISTORY_TABLE** .  
  
-   Se o esquema especificado não existir, a instrução **CREATE TABLE** falhará.  
  
-   Se a tabela especificada pelo parâmetro **HISTORY_TABLE** já existir, ela será validada em relação à tabela temporal recém-criada em termos de [consistência do esquema e consistência dos dados temporais](https://msdn.microsoft.com/library/dn935015.aspx). Se você especificar uma tabela de histórico inválido, a instrução **CREATE TABLE** falhará.  
  
## <a name="creating-a-temporal-table-with-a-user-defined-history-table"></a>Criação de uma tabela temporal com uma tabela de histórico definido pelo usuário  
 A criação de uma tabela temporal com tabela de histórico definido pelo usuário é uma opção conveniente quando o usuário deseja especificar a tabela de histórico com opções de armazenamento específicas e índices adicionais. No exemplo a seguir, uma tabela de histórico definido pelo usuário é criada com um esquema alinhado à tabela temporal que será criada. Um índice columnstore clusterizado e um índice rowstore não clusterizado adicional (árvore B) são criado para essa tabela de histórico definido pelo usuário com a função de pesquisas de ponto. Após a criação dessa tabela de histórico definido pelo usuário, a tabela temporal com controle da versão do sistema é criada especificando a tabela de histórico definido pelo usuário como a tabela de histórico padrão.  
  
```  
CREATE TABLE DepartmentHistory   
(    
     DeptID int NOT NULL  
   , DeptName varchar(50) NOT NULL  
   , ManagerID INT  NULL  
   , ParentDeptID int NULL  
   , SysStartTime datetime2 NOT NULL  
   , SysEndTime datetime2 NOT NULL   
);   
GO   
CREATE CLUSTERED COLUMNSTORE INDEX IX_DepartmentHistory   
   ON DepartmentHistory;   
CREATE NONCLUSTERED INDEX IX_DepartmentHistory_ID_PERIOD_COLUMNS   
   ON DepartmentHistory (SysEndTime, SysStartTime, DeptID);   
GO   
CREATE TABLE Department   
(    
    DeptID int NOT NULL PRIMARY KEY CLUSTERED  
   , DeptName varchar(50) NOT NULL  
   , ManagerID INT  NULL  
   , ParentDeptID int NULL  
   , SysStartTime datetime2 GENERATED ALWAYS AS ROW START NOT NULL  
   , SysEndTime datetime2 GENERATED ALWAYS AS ROW END NOT NULL     
   , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)      
)    
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory))   
;  
```  
  
### <a name="important-remarks"></a>Observações importantes  
  
-   Se você planeja executar consultas analíticas em dados históricos que empregam agregações ou funções de janelamento, a criação de uma columnstore clusterizada como um índice primário é altamente recomendável para o desempenho da consulta e compactação.  
  
-   Se o caso de uso principal for a auditoria de dados (ou seja, pesquisa por alterações históricas de uma única linha da tabela atual), uma boa opção é criar uma tabela de histórico de rowstore com um índice clusterizado  
  
-   A tabela de histórico não pode ter chave primária, chaves estrangeiras, índices exclusivos, restrições de tabela ou gatilhos. Ela não pode ser configurada para alterar a captura de dados, o controle de alterações ou replicação de mesclagem ou transacional.  
  
## <a name="alter-non-temporal-table-to-be-system-versioned-temporal-table"></a>Alteração de tabela não temporal para tabela temporal com controle da versão do sistema  
 Quando você precisa habilitar o controle da versão do sistema usando uma tabela existente, por exemplo, quando você deseja migrar uma solução personalizada temporal para o suporte interno.   
Por exemplo, você pode ter um conjunto de tabelas nas quais o controle de versão é implementado com gatilhos. O uso do controle da versão do sistema temporal é menos complexo e fornece outros benefícios que incluem:  
  
-   histórico imutável  
  
-   nova sintaxe para consultas entre períodos de tempo  
  
-   melhor desempenho de DML  
  
-   custos de manutenção mínima  
  
 Ao converter uma tabela existente, considere o uso da cláusula **HIDDEN** para ocultar as novas colunas **PERIOD** , a fim de evitar o impacto em aplicativos existentes que não foram projetados para lidar com novas colunas.  
  
### <a name="adding-versioning-to-non-temporal-tables"></a>Adição do controle de versão a tabelas não temporais  
 Se você quiser começar a controlar as alterações de uma tabela não temporal que contém os dados, é necessário adicionar a definição **PERIOD** e, opcionalmente, fornecer um nome para a tabela de histórico vazio que o SQL Server criará para você:  
  
```  
CREATE SCHEMA History;   
GO   
ALTER TABLE InsurancePolicy   
   ADD   
      SysStartTime datetime2(0) GENERATED ALWAYS AS ROW START HIDDEN    
           CONSTRAINT DF_SysStart DEFAULT SYSUTCDATETIME()  
      , SysEndTime datetime2(0) GENERATED ALWAYS AS ROW END HIDDEN    
           CONSTRAINT DF_SysEnd DEFAULT CONVERT(datetime2 (0), '9999-12-31 23:59:59'),   
      PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);   
GO   
ALTER TABLE InsurancePolicy   
   SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.InsurancePolicy))   
;  
```  
  
#### <a name="important-remarks"></a>Observações importantes  
  
-   A adição de colunas não nulas com padrões à tabela com dados existente é uma operação de tamanho de dados (size of data operation) em todas as edições com exceção do SQL Server Enterprise Edition (em que é uma operação de metadados). Com uma tabela de histórico grande e com dados existente no SQL Server Standard Edition, a adição de uma coluna não nula pode ser uma operação dispendiosa.  
  
-   As restrições para colunas com período de início e período de término devem ser escolhidas com cuidado:  
  
    -   O padrão para a coluna inicial especifica a partir de qual ponto no tempo você considera as linhas existentes válidas. Isso não pode ser especificado como um ponto de data/hora no futuro.  
  
    -   A hora de término deve ser especificada como o valor máximo para uma determinada precisão de datetime2  
  
-   A adição de um período executará a verificação de consistência dos dados na tabela atual a fim de se certificar de que os padrões para colunas do período são válidos.  
  
-   Quando uma tabela de histórico existente é especificada ao habilitar **SYSTEM_VERSIONING**, uma verificação de consistência de dados temporais é executada na tabela atual e de histórico. Ela poderá ser ignorada se você especificar **DATA_CONSISTENCY_CHECK = OFF** como um parâmetro adicional.  
  
### <a name="migrate-existing-tables-to-built-in-support"></a>Migrar as tabelas existentes para o suporte interno  
 Este exemplo mostra como migrar uma solução existente, com base em gatilhos, para o suporte temporal interno. Para este exemplo, vamos supor que a solução personalizada atual divide os dados atuais e históricos em duas tabelas de usuário separadas (**ProjectTaskCurrent** e **ProjectTaskHistory**). Se a solução existente usa uma única tabela para armazenar as linhas reais e históricas, divida os dados entre duas tabelas antes das etapas de migração mostradas neste exemplo:  
  
```  
/*Drop trigger on future temporal table*/   
DROP TRIGGER ProjectCurrent_OnUpdateDelete;   
/*Make sure that future period columns are non-nullable*/   
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidFrom] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidTo] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidFrom] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidTo] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskCurrent   
   ADD PERIOD FOR SYSTEM_TIME ([ValidFrom], [ValidTo])   
ALTER TABLE ProjectTaskCurrent   
   SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProjectTaskHistory, DATA_CONSISTENCY_CHECK = ON))   
;  
```  
  
#### <a name="important-remarks"></a>Observações importantes  
  
-   A referência a colunas existentes na definição **PERIOD** altera implicitamente generated_always_type para **AS_ROW_START** e **AS_ROW_END** para essas colunas.  
  
-   A adição de **PERIOD** executará a verificação de consistência dos dados na tabela atual a fim de se certificar de que os valores existentes para colunas do período sejam válidos  
  
-   É altamente recomendável definir **SYSTEM_VERSIONING** com **DATA_CONSISTENCY_CHECK = ON** para impor as verificações de consistência de dados nos dados existentes.  
  
 
## <a name="see-also"></a>Consulte Também  
 [Tabelas temporais](../../relational-databases/tables/temporal-tables.md)   
 [Introdução a Tabelas Temporais com Controle da Versão do Sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Modificando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [Consultando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [Alterando o esquema de uma tabela temporal com versão do sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)   
 [Parando o controle de versão do sistema de uma tabela temporal com versão do sistema](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  
