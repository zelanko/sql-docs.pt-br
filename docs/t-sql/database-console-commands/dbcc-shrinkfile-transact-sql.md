---
title: DBCC SHRINKFILE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SHRINKFILE
- DBCC_SHRINKFILE_TSQL
- DBCC SHRINKFILE
- SHRINKFILE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- TRUNCATEONLY option
- shrinking files
- NOTRUNCATE option
- shrinking databases
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
- DBCC SHRINKFILE statement
ms.assetid: e02b2318-bee9-4d84-a61f-2fddcf268c9f
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: ebb817cc2d9359a04e2661a17ab4ce99a55165ba
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955907"
---
# <a name="dbcc-shrinkfile-transact-sql"></a>DBCC SHRINKFILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Reduz o tamanho do arquivo de log ou dos dados especificados do banco de dados atual. Você pode usá-lo para mover os dados de um arquivo para outros no mesmo grupo de arquivos, o que esvazia o arquivo e permite a remoção do banco de dados dele. Você pode reduzir um arquivo a menos da metade do tamanho de criação dele, definindo um novo valor para o tamanho mínimo do arquivo.
  
![Ícone do link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone do link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
  
DBCC SHRINKFILE   
(  
    { file_name | file_id }   
    { [ , EMPTYFILE ]   
    | [ [ , target_size ] [ , { NOTRUNCATE | TRUNCATEONLY } ] ]  
    }  
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
*file_name*  
O nome lógico do arquivo que será reduzido.
  
*file_id*  
O número de identificação (ID) do arquivo que será reduzido. Para obter uma ID de arquivo, use a função do sistema [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) ou confira a exibição do catálogo [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) do banco de dados atual.
  
*target_size*  
Um inteiro – o novo tamanho em megabytes do arquivo. Se não for especificado, DBCC SHRINKFILE será reduzido ao tamanho de criação do arquivo.
  
> [!NOTE]  
>  Você pode reduzir o tamanho padrão de um arquivo vazio usando DBCC SHRINKFILE *target_size*. Por exemplo, se você cria um arquivo com 5 MB e depois o reduz para 3 MB enquanto o arquivo ainda está vazio, o tamanho do arquivo padrão é definido como 3 MB. Isso só se aplica a arquivos vazios que nunca contiveram dados.  
  
Essa opção não tem suporte em contêineres de grupo de arquivos FILESTREAM.  
Se for especificado, DBCC SHRINKFILE tentará reduzir o arquivo até *target_size*. As páginas usadas na área do arquivo a ser liberadas serão movidas para espaço livres nas áreas do arquivo que serão mantidas. Por exemplo, com um arquivo de dados de 10 MB, uma operação DBCC SHRINKFILE com 8 *target_size* move todas as páginas usadas nos últimos 2 MB do arquivo para qualquer página não alocada nos primeiros 8 MB do arquivo. A DBCC SHRINKFILE não reduzirá um arquivo além do tamanho necessário dos dados armazenados. Por exemplo, se 7 MB de um arquivo de dados de 10 MB forem usados, uma instrução DBCC SHRINKFILE com *target_size* igual a 6 reduzirá o arquivo somente para 7 MB, não para 6 MB.
  
EMPTYFILE  
Migra todos os dados do arquivo especificado para outros arquivos no **mesmo grupo de arquivos**. Em outras palavras, EMPTYFILE migrará os dados do arquivo especificado para outros arquivos no mesmo grupo de arquivos. ENPTYFILE garante que nenhum dado novo seja adicionado ao arquivo, apesar de ele não ser somente leitura. Você pode usar a instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) para remover um arquivo. Se você usar a instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) para alterar o tamanho do arquivo, o sinalizador somente leitura será redefinido e dados poderão ser adicionados.

Em contêineres de grupo de arquivos FILESTREAM, não é possível usar ALTER DATABASE para remover um arquivo até que o coletor de lixo FILESTREAM tenha sido executado e tenha excluído todos os arquivos do contêiner de grupo de arquivos desnecessários que EMPTYFILE copiou em outro contêiner. Para obter mais informações, consulte [sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
> [!NOTE]  
>  Para obter informações sobre como remover um contêiner FILESTREAM, consulte a seção correspondente em [Opções de arquivo e grupos de arquivos de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
  
NOTRUNCATE  
Move páginas alocadas do final de um arquivo de dados para páginas não alocadas no início de um arquivo com ou sem a especificação de *target_percent*. O espaço livre no final do arquivo não é retornado ao sistema operacional, e o tamanho físico do arquivo não é alterado. Portanto, se NOTRUNCATE for especificado, o arquivo parecerá não reduzir.
NOTRUNCATE aplica-se apenas a arquivos de dados. Os arquivos de log não são afetados.   Essa opção não tem suporte em contêineres de grupo de arquivos FILESTREAM.
  
TRUNCATEONLY  
Libera todo o espaço livre no final do arquivo para o sistema operacional, mas não executa nenhuma movimentação de página dentro do arquivo. O arquivo de dados é reduzido somente para a última extensão alocada.
*target_size* será ignorado se for especificado com TRUNCATEONLY.  
A opção TRUNCATEONLY não move informações no log, mas remove VLFs inativos do final do arquivo de log. Essa opção não tem suporte em contêineres de grupo de arquivos FILESTREAM.
  
WITH NO_INFOMSGS  
Suprime todas as mensagens informativas.
  
## <a name="result-sets"></a>Conjuntos de resultados  
A tabela a seguir descreve as colunas do conjunto de resultados.
  
|Nome da coluna|Descrição|  
|---|---|
|**DbId**|Número de identificação do banco de dados do arquivo que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentou reduzir.|  
|**FileId**|O número de identificação do arquivo que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentou reduzir.|  
|**CurrentSize**|Número de páginas de 8 KB que o arquivo ocupa atualmente.|  
|**MinimumSize**|Número de páginas de 8 KB que o arquivo poderia ocupar, no mínimo. Esse número corresponde ao tamanho mínimo ou tamanho de criação inicial de um arquivo.|  
|**UsedPages**|Número de páginas de 8 KB usado atualmente pelo arquivo.|  
|**EstimatedPages**|Número de páginas de 8 KB a que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula que o arquivo poderia ser reduzido.|  
  
## <a name="remarks"></a>Remarks  
DBCC SHRINKFILE aplica-se aos arquivos do banco de dados atual. Para obter mais informações sobre como alterar o banco de dados atual, consulte [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md).
  
Você pode interromper as operações DBCC SHRINKFILE a qualquer momento e todo o trabalho concluído será preservado. Se você usar o parâmetro EMPTYFILE e cancelar a operação, o arquivo não será marcado para impedir que dados adicionais sejam adicionados.
  
Quando ocorre uma falha na operação DBCC SHRINKFILE, um erro é gerado.
  
 Outros usuários poderão trabalhar no banco de dados durante a redução do arquivo – o banco de dados não precisa estar no modo de usuário único. Não é necessário executar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de usuário único para reduzir os bancos de dados de sistema.  
  
## <a name="shrinking-a-log-file"></a>Redução de um arquivo de log  

Para arquivos de log, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa *target_size* para calcular o tamanho de destino do log inteiro. Portanto, *target_size* é o espaço livre do log após a operação de redução. O tamanho de destino do log inteiro é então convertido para o tamanho designado para cada arquivo de log. DBCC SHRINKFILE tenta reduzir cada arquivo de log físico imediatamente para seu tamanho de destino. No entanto, se parte do log lógico residente nos logs virtuais for maior que o tamanho designado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] liberará o espaço disponível possível e emitirá uma mensagem informativa. A mensagem descreve as ações necessárias para mover o log lógico dos logs virtuais no final do arquivo. Depois que as ações forem executadas, DBCC SHRINKFILE poderá ser usado para liberar o espaço restante.
  
Como um arquivo de log poderá ser reduzido somente a um limite de arquivo de log virtual, talvez não seja possível reduzir um arquivo de log para um tamanho menor que o tamanho de um arquivo de log virtual, mesmo que o arquivo não esteja sendo usado. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] escolhe dinamicamente o tamanho do arquivo de log virtual quando os arquivos de log são criados ou estendidos.
  
## <a name="best-practices"></a>Práticas recomendadas 
 
Considere as seguintes informações ao planejar a redução de arquivos:
-   Uma operação de redução é mais eficiente depois de uma operação que cria uma grande quantidade de espaço não utilizado, como operações que truncam ou excluem uma tabela.  

-   A maioria dos bancos de dados exige algum espaço livre disponível para operações regulares rotineiras. Se você reduzir um banco de dados repetidamente e o tamanho dele aumentar novamente, é provável que as operações regulares exijam o espaço reduzido. Nesse caso, reduzir repetidamente um banco de dados é uma operação inútil.  

-   Uma operação de redução não preserva o estado de fragmentação de índices do banco de dados e, em geral, aumenta o nível de fragmentação. Essa fragmentação é outra razão para não reduzir o banco de dados repetidamente.  

-   Reduza vários arquivos no mesmo banco de dados sequencialmente, e não simultaneamente. A contenção em tabelas do sistema pode causar o bloqueio e gerar atrasos.  
  
## <a name="troubleshooting"></a>Solução de problemas  
Esta seção descreve como diagnosticar e corrigir problemas que podem ocorrer ao executar o comando DBCC SHRINKFILE.
  
### <a name="the-file-doesnt-shrink"></a>O arquivo não é reduzido
  
Se o tamanho do arquivo não sofrer alterações após uma operação de redução sem erros, tente o seguinte para verificar se o arquivo tem espaço livre o suficiente:

- Execute a seguinte consulta.  
  
```sql
SELECT name ,size/128.0 - CAST(FILEPROPERTY(name, 'SpaceUsed') AS int)/128.0 AS AvailableSpaceInMB
FROM sys.database_files;
```

-   Execute o comando [DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md) para retornar o espaço usado no log de transações.  

A operação de redução não poderá reduzir mais o tamanho do arquivo se não houver espaço livre suficiente disponível.
  
Normalmente, o arquivo de log é que parece não ser reduzido. Em geral, a não redução é resultado de um arquivo de log que não foi truncado. Para truncar o log, você pode definir o modelo de recuperação de banco de dados como SIMPLE ou fazer backup do log e executar novamente a operação DBCC SHRINKFILE.
  
### <a name="the-shrink-operation-is-blocked"></a>A operação de redução está bloqueada  

Uma transação em execução em um [nível de isolamento baseado em controle de versão de linha](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md) pode bloquear as operações de redução. Por exemplo, se uma grande operação de exclusão estiver sendo executada em um nível de isolamento de controle de versão de linha quando uma operação DBCC SHRINK DATABASE for executada, a operação de redução aguardará a exclusão ser concluída para continuar. Quando esse bloqueio ocorre, as operações DBCC SHRINKFILE e DBCC SHRINKDATABASE emitem uma mensagem informativa (5202 para SHRINKDATABASE e 5203 para SHRINKFILE) para o log de erros do SQL Server. Essa mensagem é registrada a cada cinco minutos na primeira hora e, em seguida, a cada hora. Por exemplo, se o log de erros contiver a mensagem de erro a seguir, ocorrerá o seguinte erro:
  
```sql
DBCC SHRINKFILE for file ID 1 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
Essa mensagem significa que transações de instantâneo com carimbos de data/hora anteriores a 109, que é a última transação concluída pela operação de redução, estão bloqueando a operação de redução. Também indica que as colunas **transaction_sequence_num** ou **first_snapshot_sequence_num** na exibição de gerenciamento dinâmico [sys.dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) contêm um valor igual a 15. Se as colunas de exibição **transaction_sequence_num** ou **first_snapshot_sequence_num** contiverem um número menor que o da última transação concluída por uma operação de redução (109), a operação de redução esperará o término dessas transações.
  
Para solucionar o problema, você pode executar uma destas tarefas:
-   Encerrar a transação que está bloqueando a operação de redução.
-   Encerrar a operação de redução. Todo trabalho concluído será preservado se a operação for encerrada.  
-   Não interferir e permitir que a operação de redução aguarde até que a transação de bloqueio seja concluída.  
  
## <a name="permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner** .
  
## <a name="examples"></a>Exemplos  
  
### <a name="shrinking-a-data-file-to-a-specified-target-size"></a>Reduzindo um arquivo de dados para um tamanho de destino especificado  
O exemplo a seguir reduz o tamanho de um arquivo de dados chamado `DataFile1` do banco de dados de usuário `UserDB` para 7 MB.
  
```sql  
USE UserDB;  
GO  
DBCC SHRINKFILE (DataFile1, 7);  
GO  
```  
  
### <a name="shrinking-a-log-file-to-a-specified-target-size"></a>Reduzindo um arquivo de log para um tamanho de destino especificado  
O exemplo a seguir reduz o arquivo de log do banco de dados `AdventureWorks` para 1 MB. Para permitir que o comando DBCC SHRINKFILE reduza o arquivo, primeiro ele será truncado, pela configuração do modelo de recuperação de banco de dados como SIMPLE.
  
```sql  
USE AdventureWorks2012;  
GO  
-- Truncate the log by changing the database recovery model to SIMPLE.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY SIMPLE;  
GO  
-- Shrink the truncated log file to 1 MB.  
DBCC SHRINKFILE (AdventureWorks2012_Log, 1);  
GO  
-- Reset the database recovery model.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL;  
GO  
```  
  
### <a name="c-truncating-a-data-file"></a>C. Truncando um arquivo de dados  
O exemplo a seguir trunca o arquivo de dados primário no banco de dados `AdventureWorks`. A exibição do catálogo `sys.database_files` é consultada para obter o `file_id` do arquivo de dados.
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT file_id, name  
FROM sys.database_files;  
GO  
DBCC SHRINKFILE (1, TRUNCATEONLY);  
```  
  
### <a name="d-emptying-a-file"></a>D. Esvaziando um arquivo  
O exemplo a seguir demonstra como esvaziar um arquivo de forma que ele possa ser removido do banco de dados. Para os fins deste exemplo, é preciso, primeiro, criar um arquivo de dados que contenha dados.
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create a data file and assume it contains data.  
ALTER DATABASE AdventureWorks2012   
ADD FILE (  
    NAME = Test1data,  
    FILENAME = 'C:\t1data.ndf',  
    SIZE = 5MB  
    );  
GO  
-- Empty the data file.  
DBCC SHRINKFILE (Test1data, EMPTYFILE);  
GO  
-- Remove the data file from the database.  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE Test1data;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)  
[FILE_ID &#40;Transact-SQL&#41;](../../t-sql/functions/file-id-transact-sql.md)  
[sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[Reduzir um arquivo](../../relational-databases/databases/shrink-a-file.md)
  
  
