---
title: DBCC SHRINKDATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_SHRINKDATABASE_TSQL
- DBCC SHRINKDATABASE
- SHRINKDATABASE_TSQL
- SHRINKDATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- shrinking files
- shrinking databases
- DBCC SHRINKDATABASE statement
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
ms.assetid: fc976afd-1edb-4341-bf41-c4a42a69772b
author: pmasl
ms.author: umajay
monikerRange: = azuresqldb-current ||>= sql-server-2016 ||>= sql-server-linux-2017||=azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: 38d542d84121b41311cd8aa64d4ec9747bfc2bf8
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279523"
---
# <a name="dbcc-shrinkdatabase-transact-sql"></a>DBCC SHRINKDATABASE (Transact-SQL)
[!INCLUDE [sql-asdb-asa.md](../../includes/applies-to-version/sql-asdb-asa.md)]

Reduz o tamanho dos arquivos de dados e de log do banco de dados especificado.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DBCC SHRINKDATABASE   
( database_name | database_id | 0   
     [ , target_percent ]   
     [ , { NOTRUNCATE | TRUNCATEONLY } ]   
)  
[ WITH NO_INFOMSGS ]  
```  

```syntaxsql
-- Azure Synapse Analytics (formerly SQL DW)

DBCC SHRINKDATABASE   
( database_name   
     [ , target_percent ]   
)  
[ WITH NO_INFOMSGS ]

```  

## <a name="arguments"></a>Argumentos  
_database\_name_ | _database\_id_ | 0  
É o nome ou a ID do banco de dados a ser reduzido. Se 0 for especificado, o banco de dados atual será usado.  
  
_target\_percent_  
É a porcentagem de espaço livre que você deseja deixar no arquivo de banco de dados após a redução do banco de dados.  
  
NOTRUNCATE  
Move as páginas atribuídas do final do arquivo para páginas não atribuídas no início do arquivo. Essa ação compacta os dados dentro do arquivo. _target\_percent_ é opcional. O SQL Data Warehouse do Azure não é compatível com essa opção. 
  
O espaço livre no final do arquivo não é retornado ao sistema operacional, e o tamanho físico do arquivo não é alterado. Como tal, o banco de dados não parecerá reduzido quando você especificar NOTRUNCATE.  
  
NOTRUNCATE aplica-se apenas a arquivos de dados. NOTRUNCATE não afeta o arquivo de log.  
  
TRUNCATEONLY  
Libera todo o espaço livre no final do arquivo para o sistema operacional. Não move todas as páginas dentro do arquivo. O arquivo de dados é reduzido somente para a última extensão atribuída. Ignora _target\_percent_ se ele é especificado com TRUNCATEONLY. O SQL Data Warehouse do Azure não é compatível com essa opção.
  
TRUNCATEONLY afeta o arquivo de log. Para truncar somente o arquivo de dados, use DBCC SHRINKFILE.  
  
WITH NO_INFOMSGS  
Suprime todas as mensagens informativas com níveis de severidade de 0 a 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
A tabela a seguir descreve as colunas do conjunto de resultados.
  
|Nome da coluna|Descrição|  
|-----------------|-----------------|  
|**DbId**|Número de identificação do banco de dados do arquivo que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentou reduzir.|  
|**FileId**|Número de identificação do arquivo que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentou reduzir.|  
|**CurrentSize**|Número de páginas de 8 KB que o arquivo ocupa atualmente.|  
|**MinimumSize**|Número de páginas de 8 KB que o arquivo poderia ocupar, no mínimo. Esse valor corresponde ao tamanho mínimo ou tamanho de criação original de um arquivo.|  
|**UsedPages**|Número de páginas de 8 KB usado atualmente pelo arquivo.|  
|**EstimatedPages**|Número de páginas de 8 KB a que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula que o arquivo poderia ser reduzido.|  
  
>[!NOTE]
> O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não exibe linhas para esses arquivos não reduzidos.  
  
## <a name="remarks"></a>Comentários  

>[!NOTE]
> Não é recomendável executar esse comando, uma vez que esta é uma operação que faz uso intenso de E/S e pode deixar seu data warehouse offline. Além disso, haverá implicações de custo para seus instantâneos de data warehouse depois de executar esse comando. 

Para reduzir todos os arquivos de dados e de log de um banco de dados específico, execute o comando DBCC SHRINKDATABASE. Para reduzir um arquivo de dados ou de log de cada vez para um banco de dados específico, execute o comando [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md).
  
Para exibir a quantidade atual de espaço livre (não alocado) no banco de dados, execute [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md).
  
Operações DBCC SHRINKDATABASE podem ser interrompidas a qualquer momento do processo, sendo preservado todo o trabalho concluído.
  
O banco de dados não pode ser menor que o tamanho mínimo configurado do banco de dados. Você especifica o tamanho mínimo quando o banco de dados é originalmente criado. Ou então, o tamanho mínimo pode ser o último tamanho explicitamente definido por meio de uma operação de alteração de tamanho do arquivo. Operações como DBCC SHRINKFILE ou ALTER DATABASE são exemplos de operações de alteração do tamanho do arquivo. 

Digamos que um banco de dados foi criado originalmente com um tamanho de 10 MB. Em seguida, ele atinge 100 MB. O tamanho mínimo ao qual o banco de dados pode ser reduzido é 10 MB, mesmo se todos os dados no banco de dados são excluídos.
  
Especifique a opção NOTRUNCATE ou a opção TRUNCATEONLY ao executar DBCC SHRINKDATABASE. Se você não fizer isso, o resultado será o mesmo que se você executar uma operação DBCC SHRINKDATABASE com NOTRUNCATE seguida pela execução de uma operação DBCC SHRINKDATABASE com TRUNCATEONLY.
  
O banco de dados reduzido não precisa estar no modo do usuário único. Outros usuários podem trabalhar no banco de dados quando ele é reduzido, incluindo bancos de dados do sistema.
  
Não é possível reduzir um banco de dados enquanto ele estiver sendo armazenado em backup. Da mesma forma, não é possível fazer backup de um banco de dados enquanto houver uma operação de redução em processamento.
  
## <a name="how-dbcc-shrinkdatabase-works"></a>Como DBCC SHRINKDATABASE funciona  
O DBCC SHRINKDATABASE reduz arquivos de dados individualmente, porém reduz arquivos de log como se todos esses arquivos existissem em uma série de logs contíguos. Os arquivos são sempre reduzidos do final.
  
Suponha que você tem alguns arquivos de log, um arquivo de dados e um banco de dados denominado **mydb**. Os arquivos de dados e de log têm 10 MB cada e o arquivo de dados contém 6 MB de dados. Para cada arquivo, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula um tamanho de destino. O valor é o tamanho a que se pretende chegar após a redução do arquivo. Quando DBCC SHRINKDATABASE é especificado com _target\_percent_, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula o tamanho de destino como a quantidade _target\_percent_ de espaço livre no arquivo após a redução. 

Por exemplo, se você especificar um _target\_percent_ igual a 25 para a redução de **mydb**, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] calculará o tamanho de destino para o arquivo de dados como 8 MB (6 MB de dados mais 2 MB de espaço livre). Portanto, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] moverá todos os dados dos últimos 2 MB do arquivo de dados para qualquer espaço livre nos primeiros 8 MB do arquivo de dados e, em seguida, reduzirá o arquivo.
  
Considere que o arquivo de dados de **mydb** contém 7 MB de dados. Especificar um _target\_percent_ igual a 30 permite que esse arquivo de dados seja reduzido para um percentual livre igual a 30. No entanto, especificar um_target\_percent_ igual a 40 não reduz o arquivo de dados porque o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não reduzirá um arquivo para um tamanho menor do que aquele que os dados ocuparem no momento. 

Você também pode pensar neste assunto outro modo: um arquivo de dados com 40 por cento de espaço livre desejado + 70 por cento de espaço cheio de dados (7 MB de 10 MB) dá mais que 100 por cento. Qualquer _target\_size_ maior que 30 não reduzirá o arquivo de dados. Ele não será reduzido porque o percentual de espaço que você deseja mais o percentual atual ocupado pelo arquivo de dados soma mais de 100%.
  
Para arquivos de log, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa _target\_percent_ para calcular o tamanho de destino do log inteiro. É por isso que _target\_percent_ é a quantidade de espaço livre no log após a operação de redução. O tamanho designado do log inteiro é convertido no tamanho designado de cada arquivo de log.
  
DBCC SHRINKDATABASE tenta reduzir cada arquivo de log físico imediatamente para seu tamanho designado. Digamos que nenhuma parte do log lógico permanece nos logs virtuais além do tamanho de destino do arquivo de log. Em seguida, o arquivo será truncado com êxito e DBCC SHRINKDATABASE terminará sem nenhuma mensagem. No entanto, se parte do log lógico permanecer nos logs virtuais com tamanho maior que o tamanho de destino, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] liberará o espaço disponível possível e emitirá uma mensagem informativa. A mensagem descreve as ações necessárias para mover o log lógico dos logs virtuais no final do arquivo. Depois que as ações forem executadas, DBCC SHRINKDATABASE poderá ser usado para liberar o espaço restante.
  
Um arquivo de log só pode ser reduzido para um limite de arquivo de log virtual. Esse é o motivo pelo qual reduzir um arquivo de log para um tamanho menor que o tamanho de um arquivo de log virtual pode não ser possível. Isso pode não ser possível mesmo que ele não esteja sendo usado. O tamanho do arquivo de log virtual é definido dinamicamente pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] quando os arquivos de log são criados ou estendidos.
  
## <a name="best-practices"></a>Práticas Recomendadas  
Considere as seguintes informações ao planejar reduzir um banco de dados:
-   Uma operação de redução é mais eficiente depois de uma operação que cria espaço não utilizado, como operações truncate table ou drop table.
-   A maioria dos bancos de dados exige algum espaço livre disponível para operações comuns rotineiras. Você pode reduzir um banco de dados repetidamente e observar que o tamanho do banco de dados cresce novamente. Esse crescimento indica que o espaço reduzido é necessário para operações regulares. Nesse caso, reduzir repetidamente um banco de dados é uma operação inútil.  
-   Uma operação de redução não preserva o estado de fragmentação de índices do banco de dados e, em geral, aumenta o nível de fragmentação. Esse resultado é outra razão para não reduzir o banco de dados repetidamente.  
-   A menos que você tenha um requisito específico, não defina a opção de banco de dados AUTO_SHRINK como ON.  
  
## <a name="troubleshooting"></a>Solução de problemas  
É possível bloquear operações de redução por uma transação que está esteja executada em um [nível de isolamento baseado em controle de versão de linha](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md). Por exemplo, se uma grande operação de exclusão estiver sendo executada em um nível de isolamento de controle de versão de linha quando uma operação DBCC SHRINK DATABASE é executada. Quando essa situação ocorrer, a operação de redução aguardará a operação de exclusão ser concluída para então reduzir os arquivos. Quando essa operação de redução aguarda, as operações DBCC SHRINKFILE e DBCC SHRINKDATABASE emitem uma mensagem informativa (5202 para SHRINKDATABASE e 5203 para SHRINKFILE). Essa mensagem é registrada no log de erros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cada cinco minutos na primeira hora e, posteriormente, a cada hora. Por exemplo, se o log de erros contiver a seguinte mensagem de erro:  
  
```sql
DBCC SHRINKDATABASE for database ID 9 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
Esse erro significa que as transações de instantâneo que têm carimbos de data/hora anteriores a 109 bloquearão a operação de redução. Essa transação é a última transação concluída pela operação de redução. Ele também indica que as colunas **transaction_sequence_num** ou **first_snapshot_sequence_num** na exibição de gerenciamento dinâmica [sys.dm_tran_active_snapshot_database_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) contêm um valor igual a 15. A coluna **transaction_sequence_num** ou **first_snapshot_sequence_num** da exibição pode conter um número menor que o da última transação concluída por uma operação de redução (109). Nesse caso, a operação de redução esperará o término dessas transações.
  
Para resolver o problema, você pode fazer uma das seguintes tarefas:
-   Encerrar a transação que está bloqueando a operação de redução.  
-   Encerrar a operação de redução. Todo o trabalho concluído será preservado.  
-   Não interferir e permitir que a operação de redução aguarde até que a transação de bloqueio seja concluída.  
  
## <a name="permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-shrinking-a-database-and-specifying-a-percentage-of-free-space"></a>a. Reduzindo um banco de dados e especificando uma porcentagem de espaço livre  
O exemplo a seguir reduz o tamanho dos arquivos de dados e de log no banco de dados de usuário `UserDB` para permitir 10 por cento de espaço livre no banco de dados.  
  
```sql  
DBCC SHRINKDATABASE (UserDB, 10);  
GO  
```  
  
### <a name="b-truncating-a-database"></a>B. Truncando um banco de dados  
O exemplo a seguir reduz os arquivos de dados e de log no banco de dados de exemplo `AdventureWorks` até a última extensão atribuída.  
  
```sql  
DBCC SHRINKDATABASE (AdventureWorks2012, TRUNCATEONLY);  
```  
### <a name="c-shrinking-an-azure-synapse-analytics-database"></a>C. Reduzindo um banco de dados do Azure Synapse Analytics

```
DBCC SHRINKDATABASE (database_A);
DBCC SHRINKDATABASE (database_B, 10); 

```

## <a name="see-also"></a>Confira também  
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
[Reduzir um banco de dados](../../relational-databases/databases/shrink-a-database.md)
  
  
