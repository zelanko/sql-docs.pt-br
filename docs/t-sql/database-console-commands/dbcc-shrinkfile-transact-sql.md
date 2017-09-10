---
title: DBCC SHRINKFILE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 87
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 14746a5bfac3674299e03b6eba0da1a823f1bba9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-shrinkfile-transact-sql"></a>DBCC SHRINKFILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Reduz o tamanho dos dados especificados ou do arquivo de log do banco de dados atual ou esvazia um arquivo movendo os dados do arquivo especificado para outros arquivos no mesmo grupo de arquivos, o que permite que o arquivo seja removido do banco de dados. Você pode reduzir um arquivo a um tamanho menor que o tamanho especificado no momento de sua criação. Isso redefine o tamanho mínimo de arquivo para o valor novo.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
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
É o nome lógico do arquivo que será reduzido.
  
*file_id*  
É o número de identificação (ID) do arquivo que será reduzido. Para obter uma ID de arquivo, use o [FILE_IDEX](../../t-sql/functions/file-idex-transact-sql.md) função do sistema ou a consulta a [sys. database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) exibição no banco de dados atual do catálogo.
  
*target_size*  
É o tamanho do arquivo em megabytes, expresso como um número inteiro. Se não for especificado, DBCC SHRINKFILE reduzirá o tamanho do arquivo ao tamanho padrão. O tamanho padrão é o tamanho especificado quando o arquivo foi criado.
  
> [!NOTE]  
>  Você pode reduzir o tamanho padrão de um arquivo vazio usando DBCC SHRINKFILE *target_size*. Por exemplo, se você cria um arquivo com 5 MB e depois o reduz para 3 MB enquanto o arquivo ainda está vazio, o tamanho do arquivo padrão é definido como 3 MB. Isso só se aplica a arquivos vazios que nunca contiveram dados.  
  
Essa opção não tem suporte em contêineres de grupo de arquivos FILESTREAM.  
Se *target_size* for especificado, DBCC SHRINKFILE tenta reduzir o arquivo para o tamanho especificado. Páginas usadas na parte do arquivo a ser liberada serão realocadas para o espaço livre disponível na parte do arquivo retida. Por exemplo, se houver um arquivo de dados de 10 MB, uma operação DBCC SHRINKFILE com um *target_size* de 8 fará com que todas as páginas usaram nos últimos 2 MB do arquivo sejam realocadas em qualquer página não alocada nos primeiros 8 MB do arquivo. DBCC SHRINKFILE não reduz um arquivo além do tamanho necessário para armazenar os dados no arquivo. Por exemplo, se 7 MB de um arquivo de dados de 10 MB é usado, uma instrução DBCC SHRINKFILE com um *target_size* de 6 reduzirá o arquivo somente para 7 MB, não 6 MB.
  
EMPTYFILE  
Migra todos os dados do arquivo especificado para outros arquivos de **mesmo grupo de arquivos**. Em outras palavras, EmptyFile migrará os dados do arquivo especificado para outros arquivos no mesmo grupo de arquivos. Emptyfile garante que nenhum dado novo será adicionado ao arquivo. O arquivo pode ser removido usando o [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) instrução.
Em contêineres de grupo de arquivos FILESTREAM, o arquivo não pode ser removido usando ALTER DATABASE até que o coletor de lixo FILESTREAM tenha sido executado e tenha excluído todos os arquivos do contêiner de grupo de arquivos desnecessários que EMPTYFILE copiou em outro contêiner. Para obter mais informações, consulte [sp_filestream_force_garbage_collection &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
> [!NOTE]  
>  Para obter informações sobre como remover um contêiner FILESTREAM, consulte a seção correspondente [alterar o arquivo de banco de dados e opções de grupo de arquivos &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
  
NOTRUNCATE  
Move o páginas alocadas do final de um arquivo de dados para as páginas alocadas à frente do arquivo com ou sem especificar *target_percent*. O espaço livre no final do arquivo não é retornado ao sistema operacional, e o tamanho físico do arquivo não é alterado. Portanto, se NOTRUNCATE for especificado, o arquivo não parecerá reduzido.
NOTRUNCATE aplica-se apenas a arquivos de dados. Os arquivos de log não são afetados.   Essa opção não tem suporte em contêineres de grupo de arquivos FILESTREAM.
  
TRUNCATEONLY  
Libera todo o espaço livre no final do arquivo para o sistema operacional, mas não executa nenhuma movimentação de página dentro do arquivo. O arquivo de dados é reduzido somente para a última extensão alocada.
*target_size* será ignorado se especificado com TRUNCATEONLY.  
A opção TRUNCATEONLY não move informações no log, mas remove VLFs inativos do final do arquivo de log. Essa opção não tem suporte em contêineres de grupo de arquivos FILESTREAM.
  
WITH NO_INFOMSGS  
Suprime todas as mensagens informativas.
  
## <a name="result-sets"></a>Conjuntos de resultados  
A tabela a seguir descreve as colunas do conjunto de resultados.
  
|Nome da coluna|Description|  
|---|---|
|**DbId**|Número de identificação do banco de dados do arquivo que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentou reduzir.|  
|**FileId**|O número de identificação de arquivo do arquivo de [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentou reduzir.|  
|**CurrentSize**|Número de páginas de 8 KB que o arquivo ocupa atualmente.|  
|**MinimumSize**|Número de páginas de 8 KB que o arquivo poderia ocupar, no mínimo. Corresponde ao tamanho mínimo ou tamanho de criação inicial de um arquivo.|  
|**UsedPages**|Número de páginas de 8 KB usado atualmente pelo arquivo.|  
|**EstimatedPages**|Número de páginas de 8 KB a que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula que o arquivo poderia ser reduzido.|  
  
## <a name="remarks"></a>Comentários  
DBCC SHRINKFILE aplica-se aos arquivos do banco de dados atual. Para obter mais informações sobre como alterar o banco de dados atual, consulte [USE &#40; Transact-SQL &#41; ](../../t-sql/language-elements/use-transact-sql.md).
  
Operações DBCC SHRINKFILE podem ser interrompidas a qualquer momento do processo e todo o trabalho concluído será mantido.
  
Quando ocorre uma falha na operação DBCC SHRINKFILE, um erro é gerado.
  
 O banco de dados que está sendo reduzido não precisa estar em modo de usuário único; outros usuários podem estar trabalhando no banco de dados quando o arquivo for reduzido. Não é necessário executar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de usuário único para reduzir os bancos de dados de sistema.  
  
## <a name="shrinking-a-log-file"></a>Para reduzir um arquivo de log  
Para arquivos de log, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa *target_size* para calcular o tamanho de destino para o log inteiro; portanto, *target_size* é a quantidade de espaço livre no log após a operação de redução. O tamanho de destino do log inteiro é então convertido para o tamanho designado para cada arquivo de log. DBCC SHRINKFILE tenta reduzir cada arquivo de log físico imediatamente para seu tamanho de destino. No entanto, se parte do log lógico residente nos logs virtuais for maior que o tamanho designado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] liberará o espaço disponível possível e emitirá uma mensagem informativa. A mensagem descreve as ações necessárias para mover o log lógico dos logs virtuais no final do arquivo. Depois que as ações forem executadas, DBCC SHRINKFILE poderá ser usado para liberar o espaço restante.
  
Como um arquivo de log poderá ser reduzido somente a um limite de arquivo de log virtual, talvez não seja possível reduzir um arquivo de log para um tamanho menor que o tamanho de um arquivo de log virtual, mesmo que o arquivo não esteja sendo usado. O tamanho do arquivo de log virtual é definido dinamicamente pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] quando os arquivos de log são criados ou estendidos.
  
## <a name="best-practices"></a>Práticas recomendadas  
Considere as seguintes informações ao planejar a redução de arquivos:
-   Uma operação de redução é mais eficiente depois de uma operação que cria muito espaço não utilizado, como operações que truncam ou excluem uma tabela.  
-   A maioria dos bancos de dados exige algum espaço livre disponível para operações comuns rotineiras. Se você reduzir um banco de dados repetidamente e perceber que ele aumentou novamente, isso indica que o espaço reduzido é necessário para as operações rotineiras. Nesse caso, reduzir repetidamente um banco de dados é uma operação inútil.  
-   Uma operação de redução não preserva o estado de fragmentação de índices do banco de dados e, geralmente, aumenta o nível de fragmentação. Essa é outra razão para não reduzir o banco de dados repetidamente.  
-   Reduza vários arquivos no mesmo banco de dados sequencialmente, e não simultaneamente. A contenção em tabelas do sistema pode causar atrasos devido ao bloqueio.  
  
## <a name="troubleshooting"></a>Solução de problemas  
Esta seção descreve como diagnosticar e corrigir problemas que podem ocorrer ao executar o comando DBCC SHRINKFILE.
  
### <a name="the-file-does-not-shrink"></a>O arquivo não foi reduzido  
Se a operação de redução ocorrer sem erro, mas parecer que o tamanho do arquivo não foi alterado, verifique se o arquivo tem espaço livre adequado para remoção, executando uma das seguintes operações:
- Execute a seguinte consulta.  
  
```sql
SELECT name ,size/128.0 - CAST(FILEPROPERTY(name, 'SpaceUsed') AS int)/128.0 AS AvailableSpaceInMB
FROM sys.database_files;
```

-   Execute o [DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md) comando para retornar o espaço usado no log de transações.  
Se não houver espaço livre suficiente disponível, a operação de redução não poderá reduzir mais o tamanho de arquivo.
  
Normalmente, o arquivo de log é que parece não ser reduzido. Em geral, isso é resultado de um arquivo de log que não foi truncado. Você pode truncar o log definindo o modelo de recuperação de banco de dados como SIMPLE ou fazendo backup do log e executando novamente a operação DBCC SHRINKFILE.
  
### <a name="the-shrink-operation-is-blocked"></a>Operação de redução bloqueada  
É possível que operações de redução sejam bloqueadas por uma transação que está sendo executado em um [nível de isolamento com base em controle de versão de linha](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md). Por exemplo, se uma grande operação de exclusão estiver sendo executada em um nível de isolamento de controle de versão de linha quando uma operação DBCC SHRINK DATABASE for executada, a operação de redução aguardará a operação de exclusão ser concluída antes de reduzir os arquivos. Quando isso ocorre, as operações DBCC SHRINKFILE e DBCC SHRINKDATABASE emitem uma mensagem informativa (5202 para SHRINKDATABASE e 5203 para SHRINKFILE) para o log de erros do SQL Server a cada cinco minutos na primeira hora e depois a cada hora. Por exemplo, se o log de erros contiver a mensagem de erro a seguir, ocorrerá o seguinte erro:
  
```sql
DBCC SHRINKFILE for file ID 1 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
Isso significa que a operação de redução foi bloqueada por transações de instantâneo que têm carimbos de data/hora anteriores a 109, que é a última transação concluída pela operação de redução. Ele também indica que o **transaction_sequence_num**, ou **first_snapshot_sequence_num** colunas o [sys.DM tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) exibição de gerenciamento dinâmico contém um valor de 15. Se o **transaction_sequence_num**, ou **first_snapshot_sequence_num** colunas no modo de exibição contém um número que seja menor do que a última transação concluída por uma operação de redução (109), o reduzir operação aguardará a finalização dessas transações.
  
Para solucionar o problema, você pode executar uma destas tarefas:
-   Encerrar a transação que está bloqueando a operação de redução.
-   Encerrar a operação de redução. Nesse caso, todo trabalho concluído será preservado.  
-   Não interferir e permitir que a operação de redução aguarde até que a transação de bloqueio seja concluída.  
  
## <a name="permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner** .
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-shrinking-a-data-file-to-a-specified-target-size"></a>A. Reduzindo um arquivo de dados para um tamanho de destino especificado  
O exemplo a seguir reduz o tamanho de um arquivo de dados denominado `DataFile1` no `UserDB` banco de dados de usuário para 7 MB.
  
```sql  
USE UserDB;  
GO  
DBCC SHRINKFILE (DataFile1, 7);  
GO  
```  
  
### <a name="b-shrinking-a-log-file-to-a-specified-target-size"></a>B. Reduzindo um arquivo de log para um tamanho de destino especificado  
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
O exemplo a seguir demonstra o procedimento para esvaziar um arquivo de forma que ele possa ser removido do banco de dados. Neste exemplo, primeiro é criado um arquivo de dados, presumindo-se que ele contenha dados.
  
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
  
## <a name="see-also"></a>Consulte também  
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)  
[FILE_ID &#40; Transact-SQL &#41;](../../t-sql/functions/file-id-transact-sql.md)  
[sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[Reduzir um arquivo](../../relational-databases/databases/shrink-a-file.md)
  
  

