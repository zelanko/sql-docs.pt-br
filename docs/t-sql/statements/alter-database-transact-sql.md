---
title: ALTER DATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/20/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_TSQL
- ALTER DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- databases [SQL Server], modifying
- ALTER DATABASE statement
- databases [SQL Server], renaming
- renaming databases
- database modifications [SQL Server]
- ALTER DATABASE statement, syntax described
- database names [SQL Server], ALTER DATABASE
- modifying databases
- collations [SQL Server], modifying
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 15f8affd-8f39-4021-b092-0379fc6983da
caps.latest.revision: 282
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5e0e79fb6a74373268e6077971662b323623cc54
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33065763"
---
# <a name="alter-database-transact-sql"></a>ALTER DATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica um banco de dados ou os arquivos e grupos de arquivos associados ao banco de dados. Adiciona ou remove arquivos e grupos de arquivos de um banco de dados, altera os atributos de um banco de dados ou seus arquivos e grupos de arquivos, altera o agrupamento de banco de dados e define opções de banco de dados. Instantâneos de banco de dados não podem ser modificados. Para modificar opções de banco de dados associadas à replicação, use [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md).  
   
 Devido a sua extensão, a sintaxe ALTER DATABASE está dividida nos seguintes tópicos:  
  
 ALTER DATABASE  
 O tópico atual fornece a sintaxe para alterar o nome e o agrupamento de um banco de dados.  
  
 [Opções de arquivo e grupo de arquivos de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
 Fornece a sintaxe para adicionar e remover arquivos e grupos de arquivos de um banco de dados e para alterar os atributos dos arquivos e grupos de arquivos.  
  
 [Opções de ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
 Fornece a sintaxe para alterar os atributos de um banco de dados usando as opções SET de ALTER DATABASE.  
  
 [Espelhamento de banco de dados de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)  
 Fornece a sintaxe para as opções SET de ALTER DATABASE relacionadas a espelhamento de banco de dados.  
  
 [ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)  
 Fornece a sintaxe para as opções [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] de ALTER DATABASE para configurar um banco de dados secundário em uma réplica secundária de um Grupo de Disponibilidade AlwaysOn.  
  
 [Nível de compatibilidade de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
 Fornece a sintaxe para as opções SET de ALTER DATABASE relacionadas aos níveis de compatibilidade do banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
Para o banco de dados SQL do Azure, veja [ALTER DATABASE &#40;Banco de Dados SQL do Azure&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
Para o SQL Data Warehouse do Azure, veja [ALTER DATABASE &#40;SQL Data Warehouse do Azure&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).  
Para Parallel Data Warehouse, veja [ALTER DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- SQL Server Syntax  
ALTER DATABASE { database_name  | CURRENT }  
{  
    MODIFY NAME = new_database_name   
  | COLLATE collation_name  
  | <file_and_filegroup_options>  
  | <set_database_options>  
}  
[;]  
  
<file_and_filegroup_options >::=  
  <add_or_modify_files>::=  
  <filespec>::=   
  <add_or_modify_filegroups>::=  
  <filegroup_updatability_option>::=  
  
<set_database_options>::=  
  <optionspec>::=   
  <auto_option> ::=   
  <change_tracking_option> ::=  
  <cursor_option> ::=   
  <database_mirroring_option> ::=   
  <date_correlation_optimization_option> ::=  
  <db_encryption_option> ::=  
  <db_state_option> ::=  
  <db_update_option> ::=  
  <db_user_access_option> ::=  <delayed_durability_option> ::=  <external_access_option> ::=  
  <FILESTREAM_options> ::=  
  <HADR_options> ::=    
  <parameterization_option> ::=  
  <query_store_options> ::=  
  <recovery_option> ::=   
  <service_broker_option> ::=  
  <snapshot_option> ::=  
  <sql_option> ::=   
  <termination> ::=  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 É o nome do banco de dados a ser modificado.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 CURRENT  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Designa que o banco de dados em uso deve ser alterado.  
  
 MODIFY NAME **=***new_database_name*  
 Renomeia o banco de dados com o nome especificado como *novo_nome_do_banco_de_dados*.  
  
 COLLATE *collation_name*  
 Especifica o agrupamento do banco de dados. *collation_name* pode ser um nome de agrupamento do Windows ou um nome de agrupamento SQL. Se não especificado, o banco de dados será atribuído ao agrupamento da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Durante a criação de bancos de dados com itens diferentes do agrupamento padrão, os dados no banco de dados sempre respeitam o agrupamento especificado. Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ao criar um banco de dados independente, as informações do catálogo interno serão mantidas por meio do agrupamento padrão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **Latin1_General_100_CI_AS_WS_KS_SC**.  
  
 Para obter mais informações sobre os nomes de agrupamento do Windows e do SQL, veja [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md).  
  
 **\<delayed_durability_option> ::=**  
 **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para obter mais informações, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) e [Controlar a durabilidade da transação](../../relational-databases/logs/control-transaction-durability.md).  
  
 **\<file_and_filegroup_options>::=**  
 Para obter mais informações, consulte [Opções de arquivo e grupo de arquivos de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  
  
## <a name="remarks"></a>Remarks  
 Para remover um banco de dados, use [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).  
  
 Para diminuir o tamanho de um banco de dados, use [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
 A instrução ALTER DATABASE deve ser executada em modo de confirmação automática (o modo padrão de administração de transações) e não deve ser permitida em uma transação explícita ou implícita.  
  
 O estado de um arquivo de banco de dados (por exemplo, online ou offline) é mantido independentemente do estado do banco de dados. Para obter mais informações, consulte [Estados de arquivo](../../relational-databases/databases/file-states.md). O estado dos arquivos dentro de um grupo de arquivos determina a disponibilidade de todo o grupo. Para que um grupo de arquivos fique disponível, todos os seus arquivos devem estar online. Se um grupo de arquivos estiver offline, qualquer tentativa de acessá-lo por meio de uma instrução SQL falhará com erro. Quando você cria planos de consulta para instruções SELECT, o otimizador de consultas evita índices não clusterizados e exibições indexadas que residam em grupos de arquivos offline. Isso permite que essas instruções tenham êxito. Porém, se o grupo de arquivos offline contiver o heap ou índice clusterizado da tabela de destino, as instruções SELECT falharão. Além disso, qualquer instrução INSERT, UPDATE ou DELETE que modifique uma tabela contendo um índice em um grupo de arquivos offline falhará.  
  
 Quando um banco de dados estiver em estado RESTORING, a maioria das instruções ALTER DATABASE falhará. A exceção está definindo opções de espelhamento de banco de dados. Um banco de dados pode estar no estado RESTORING durante uma operação de restauração ativa ou quando uma operação de restauração de um banco de dados ou arquivo de log falhar devido a um arquivo de backup corrompido.  
  
 O cache do plano para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é limpo pela configuração de uma das seguintes opções.  
  
|||  
|-|-|  
|OFFLINE|READ_WRITE|  
|ONLINE|MODIFY FILEGROUP DEFAULT|  
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|  
|COLLATE|MODIFY FILEGROUP READ_ONLY|  
|READ_ONLY|PAGE_VERIFY|  
  
 A limpeza do cache de planos gera uma recompilação de todos os planos de execução subsequentes e pode provocar uma redução repentina e temporária do desempenho de consultas. Para cada armazenamento em cache limpo no cache de planos, o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém a seguinte mensagem informativa: "O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontrou %d ocorrência(s) de liberação de armazenamento em cache '% s' (parte do cache de planos) devido à manutenção do banco de dados ou operações de reconfiguração". Essa mensagem é registrada a cada cinco minutos, contanto que o cache seja liberado dentro desse intervalo de tempo.  
  
 O cache de procedimento também é liberado nos seguintes cenários:  
  
-   Um banco de dados tem a opção de banco de dados AUTO_CLOSE definida como ON. Quando nenhuma conexão de usuário fizer referência ou usar o banco de dados, a tarefa de banco de dados tentará fechar e encerrar o banco de dados automaticamente.  
  
-   Execute diversas consultas em um banco de dados que tem opções padrão. O banco de dados é removido.  
  
-   Um instantâneo de banco de dados para um banco de dados de origem é removido.  
  
-   Você recria com sucesso o log de transação para um banco de dados.  
  
-   Você restaura um backup de banco de dados.  
  
-   Você desanexa um banco de dados.  
  
## <a name="changing-the-database-collation"></a>Alterando o agrupamento de banco de dados  
 Antes de aplicar um agrupamento diferente a um banco de dados, certifique-se de que existam as seguintes condições:  
  
-   Você é o único usuário que está utilizando o banco de dados no momento.  
  
-   Nenhum objeto associado ao esquema depende do agrupamento do banco de dados.  
  
     Se os objetos a seguir, que dependem do agrupamento de banco de dados, existirem no banco de dados, a instrução ALTER DATABASE*database_name*COLLATE falhará. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará uma mensagem de erro para cada objeto que bloqueia a ação de ALTER:  
  
    -   Funções definidas pelo usuário e exibições criadas com SCHEMABINDING.  
  
    -   Colunas computadas.  
  
    -   Restrições CHECK.  
  
    -   Funções com valor de tabela que retornam tabelas com colunas de caracteres com agrupamentos herdados do agrupamento de banco de dados padrão.  
  
     Informações de dependência de entidades não associadas a esquema são automaticamente atualizadas quando o agrupamento de banco de dados é alterado.  
  
 Alterar o agrupamento de banco de dados não cria duplicatas entre nenhum nome de sistema para os objetos de banco de dados. Se nomes duplicados resultarem do agrupamento alterados, os namespaces a seguir poderão provocar falha de alteração de agrupamento de banco de dados:  
  
-   Nomes de objeto, como procedimentos, tabelas, gatilhos ou exibições.  
  
-   Nomes de esquema.  
  
-   Entidades, como grupos, funções ou usuários.  
  
-   Nomes escalares, como tipos de sistema e tipos definidos pelo usuário.  
  
-   Nomes de catálogo de texto completo.  
  
-   Nomes de coluna ou parâmetro dentro de um objeto.  
  
-   Nomes de índice dentro de uma tabela.  
  
Nomes duplicados resultantes do novo agrupamento provocarão falha na ação de alteração e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará uma mensagem de erro especificando o namespace onde a duplicata foi encontrada.  
  
## <a name="viewing-database-information"></a>Exibindo informações do banco de dados  
 É possível usar exibições do catálogo, funções do sistema e procedimentos armazenados do sistema para retornar informações sobre bancos de dados, arquivos e grupos de arquivos.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-name-of-a-database"></a>A. Alterando o nome de um banco de dados  
 O exemplo a seguir altera o nome do banco de dados `AdventureWorks2012` para `Northwind`.  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
### <a name="b-changing-the-collation-of-a-database"></a>B. Alterando o agrupamento de um banco de dados  
 O exemplo a seguir cria um banco de dados denominado `testdb` com o agrupamento `SQL_Latin1_General_CP1_CI_A`S e, em seguida, altera o agrupamento do banco de dados `testdb` para `COLLATE French_CI_AI`.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE master;  
GO  
  
CREATE DATABASE testdb  
COLLATE SQL_Latin1_General_CP1_CI_AS ;  
GO  
  
ALTER DATABASE testDB  
COLLATE French_CI_AI ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
- [ALTER DATABASE &#40;Banco de Dados SQL do Azure&#41;](alter-database-azure-sql-database.md)  
- [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
- [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
- [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
- [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
- [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
- [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
- [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
- [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
- [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
- [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
- [sys.data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
- [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
- [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
- [Bancos de dados do sistema](../../relational-databases/databases/system-databases.md)  
  
