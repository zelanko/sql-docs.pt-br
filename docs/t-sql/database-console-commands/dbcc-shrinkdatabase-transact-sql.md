---
title: DBCC SHRINKDATABASE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_SHRINKDATABASE_TSQL
- DBCC SHRINKDATABASE
- SHRINKDATABASE_TSQL
- SHRINKDATABASE
dev_langs: TSQL
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
caps.latest.revision: "62"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 9e14fa00535414673f5526c6aedb3ec349235a29
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-shrinkdatabase-transact-sql"></a>DBCC SHRINKDATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Reduz o tamanho dos arquivos de dados e de log do banco de dados especificado.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC SHRINKDATABASE   
( database_name | database_id | 0   
     [ , target_percent ]   
     [ , { NOTRUNCATE | TRUNCATEONLY } ]   
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Database_Name* | *database_id* | 0  
 É o nome ou a ID do banco de dados a ser reduzido. Se 0 for especificado, será usado o banco de dados atual.  
  
 *target_percent*  
 É a porcentagem de espaço livre que você deseja deixar no arquivo de banco de dados após a redução do banco de dados.  
  
 NOTRUNCATE  
 Compacta os dados dos arquivos de dados, movendo as páginas alocadas do final de um arquivo para as páginas alocadas à frente do arquivo. *target_percent* é opcional.  
  
 O espaço livre no final do arquivo não é retornado ao sistema operacional, e o tamanho físico do arquivo não é alterado. Portanto, quando NOTRUNCATE é especificado, o banco de dados parece não ter sido reduzido.  
  
 NOTRUNCATE aplica-se apenas a arquivos de dados. O arquivo de log não é afetado.  
  
 TRUNCATEONLY  
 Libera todo o espaço livre no final do arquivo para o sistema operacional, mas não executa nenhuma movimentação de página dentro do arquivo. O arquivo de dados é reduzido somente para a última extensão alocada. *target_percent* será ignorado se especificado com TRUNCATEONLY.  
  
 TRUNCATEONLY afeta o arquivo de log. Para truncar somente o arquivo de dados, use DBCC SHRINKFILE.  
  
 WITH NO_INFOMSGS  
 Suprime todas as mensagens informativas com níveis de severidade de 0 a 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
A tabela a seguir descreve as colunas do conjunto de resultados.
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|**DbId**|Número de identificação do banco de dados do arquivo que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentou reduzir.|  
|**FileId**|Número de identificação do arquivo que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentou reduzir.|  
|**CurrentSize**|Número de páginas de 8 KB que o arquivo ocupa atualmente.|  
|**MinimumSize**|Número de páginas de 8 KB que o arquivo poderia ocupar, no mínimo. Corresponde ao tamanho mínimo ou tamanho de criação inicial de um arquivo.|  
|**UsedPages**|Número de páginas de 8 KB usado atualmente pelo arquivo.|  
|**EstimatedPages**|Número de páginas de 8 KB a que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula que o arquivo poderia ser reduzido.|  
  
>[!NOTE]
> O [!INCLUDE[ssDE](../../includes/ssde-md.md)] não exibe linhas para esses arquivos não reduzidos.  
  
## <a name="remarks"></a>Comentários  
Para reduzir todos os arquivos de dados e de log de um banco de dados específico, execute o comando DBCC SHRINKDATABASE. Para reduzir um dados ou arquivo de log em vez de um banco de dados, execute o [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) comando.
  
Para exibir a quantidade atual de espaço livre (não alocado) no banco de dados, execute [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md).
  
Operações DBCC SHRINKDATABASE podem ser interrompidas a qualquer momento do processo, sendo preservado todo o trabalho concluído.
  
O banco de dados não pode se tornar menor que o tamanho mínimo do banco de dados. O tamanho mínimo é aquele especificado durante a criação inicial do banco de dados ou o último tamanho explicitamente definido por meio de uma operação de alteração de tamanho de arquivo, como DBCC SHRINKFILE ou ALTER DATABASE. Por exemplo, se um banco de dados foi criado originalmente com um tamanho de 10 MB e atingir 100 MB, a redução máxima desse banco de dados será para 10 MB, mesmo se todos os dados do banco de dados forem excluídos.
  
Executar DBCC SHRINKDATABASE sem especificar a opção NOTRUNCATE ou a opção TRUNCATEONLY equivale a executar uma operação DBCC SHRINKDATABASE com NOTRUNCATE seguida de uma operação DBCC SHRINKDATABASE com TRUNCATEONLY.
  
O banco de dados que é reduzido não tem que estar em modo do usuário único; outros usuários podem trabalhar nele durante sua redução. Isto inclui os bancos de dados do sistema.
  
Não é possível reduzir um banco de dados enquanto ele estiver sendo armazenado em backup. Da mesma forma, não é possível fazer backup de um banco de dados enquanto houver uma operação de redução em processamento.
  
## <a name="how-dbcc-shrinkdatabase-works"></a>Como DBCC SHRINKDATABASE funciona  
O DBCC SHRINKDATABASE reduz arquivos de dados individualmente, porém reduz arquivos de log como se todos esses arquivos existissem em uma série de logs contíguos. Os arquivos são sempre reduzidos do final.
  
Suponha que um banco de dados denominado **mydb** com um arquivo de dados e dois arquivos de log. Os arquivos de dados e de log são de 10 MB e o arquivo de dados contém 6 MB de dados.
  
Para cada arquivo, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula um tamanho designado. Trata-se do tamanho a que se pretende chegar após a redução do arquivo. Quando DBCC SHRINKDATABASE é especificado com *target_percent*, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula o tamanho de destino para ser o *target_percent* quantidade de espaço livre no arquivo após a redução. Por exemplo, se você especificar um *target_percent* de 25 para a redução **mydb**, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcula o tamanho de destino para o arquivo de dados como 8 MB (6 MB de dados mais 2 MB de espaço livre). Portanto, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] move todos os dados de últimos 2 MB do arquivo de dados para qualquer espaço livre nos primeiros 8 MB do arquivo de dados e, em seguida, reduzirá o arquivo.
  
Suponha que o arquivo de dados de **mydb** contenha 7 MB de dados. Especificando um *target_percent* de 30 permite esse arquivo de dados será reduzido para porcentagem livre de 30. No entanto, especificando um *target_percent* de 40 não reduz o arquivo de dados porque o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não irá reduzir um arquivo para um tamanho menor do que os dados ocupam atualmente. Você também pode considerar esse problema outra maneira: 40 por cento espaço livre desejado + 70 por cento arquivo de dados completo (7 MB de 10 MB) é mais de 100 por cento. Como a porcentagem livre que se deseja somada à porcentagem atual ocupada pelo arquivo de dados é acima de 100 por cento (10 por cento), qualquer *target_size* maior que 30 não irá reduzir o arquivo de dados.
  
Para arquivos de log, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa *target_percent* para calcular o tamanho de destino para o log inteiro; portanto, *target_percent* é a quantidade de espaço livre no log após a operação de redução. O tamanho designado do log inteiro é convertido no tamanho designado de cada arquivo de log.
  
DBCC SHRINKDATABASE tenta reduzir cada arquivo de log físico imediatamente para seu tamanho designado. Se nenhuma parte do log lógico residir nos logs virtuais além do tamanho designado do arquivo de log, o arquivo será truncado com êxito e DBCC SHRINKDATABASE terminará sem nenhuma mensagem. No entanto, se parte do log lógico residente nos logs virtuais for maior que o tamanho designado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] liberará o espaço disponível possível e emitirá uma mensagem informativa. A mensagem descreve as ações necessárias para mover o log lógico dos logs virtuais no final do arquivo. Depois que as ações forem executadas, DBCC SHRINKDATABASE poderá ser usado para liberar o espaço restante.
  
Como um arquivo de log poderá ser reduzido somente a um limite de arquivo de log virtual, talvez não seja possível reduzir um arquivo de log para um tamanho menor que o tamanho de um arquivo de log virtual, mesmo que o arquivo não esteja sendo usado. O tamanho do arquivo de log virtual é definido dinamicamente pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] quando os arquivos de log são criados ou estendidos.
  
## <a name="best-practices"></a>Práticas recomendadas  
Considere as seguintes informações ao planejar reduzir um banco de dados:
-   Uma operação de redução é mais eficiente depois de uma operação que cria muito espaço não utilizado, como operações que truncam ou excluem uma tabela.  
-   A maioria dos bancos de dados exige algum espaço livre disponível para operações comuns rotineiras. Se você reduzir um banco de dados repetidamente e perceber que ele aumentou novamente, isso indica que o espaço reduzido é necessário para as operações rotineiras. Nesse caso, reduzir repetidamente um banco de dados é uma operação inútil.  
-   Uma operação de redução não preserva o estado de fragmentação de índices do banco de dados e, geralmente, aumenta o nível de fragmentação. Essa é outra razão para não reduzir o banco de dados repetidamente.  
-   A menos que você tenha um requisito específico, não defina a opção de banco de dados AUTO_SHRINK como ON.  
  
## <a name="troubleshooting"></a>Solução de problemas  
 É possível que operações de redução sejam bloqueadas por uma transação que está sendo executado em um [nível de isolamento com base em controle de versão de linha](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md). Por exemplo, se uma grande operação de exclusão estiver sendo executada em um nível de isolamento de controle de versão de linha quando uma operação DBCC SHRINK DATABASE for executada, a operação de redução aguardará a operação de exclusão ser concluída antes de reduzir os arquivos. Quando isso acontece, as operações DBCC SHRINKFILE e DBCC SHRINKDATABASE emitem uma mensagem informativa (5202 para SHRINKDATABASE e 5203 para SHRINKFILE) para o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cada cinco minutos, na primeira hora, e, depois, a cada hora. Por exemplo, se o log de erros contiver a seguinte mensagem de erro:  
  
```sql
DBCC SHRINKDATABASE for database ID 9 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
Isso significa que a operação de redução foi bloqueada por transações de instantâneo que têm carimbos de data/hora anteriores a 109, que é a última transação concluída pela operação de redução. Ele também indica que o **transaction_sequence_num**, ou **first_snapshot_sequence_num** colunas o [sys.DM tran_active_snapshot_database_transactions &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) exibição de gerenciamento dinâmico contém um valor de 15. Se o **transaction_sequence_num**, ou **first_snapshot_sequence_num** colunas no modo de exibição contém um número que seja menor do que a última transação concluída por uma operação de redução (109), o reduzir operação aguardará a finalização dessas transações.
  
Para resolver o problema, você pode fazer uma das seguintes tarefas:
-   Encerrar a transação que está bloqueando a operação de redução.  
-   Encerrar a operação de redução. Todo trabalho concluído será preservado.  
-   Não interferir e permitir que a operação de redução aguarde até que a transação de bloqueio seja concluída.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-shrinking-a-database-and-specifying-a-percentage-of-free-space"></a>A. Reduzindo um banco de dados e especificando uma porcentagem de espaço livre  
 O exemplo a seguir diminui o tamanho dos arquivos de dados e de log no banco de dados de usuário `UserDB` para permitir 10 por cento de espaço livre no banco de dados.  
  
```sql  
DBCC SHRINKDATABASE (UserDB, 10);  
GO  
```  
  
### <a name="b-truncating-a-database"></a>B. Truncando um banco de dados  
 O exemplo a seguir reduz os arquivos de dados e de log no banco de dados de exemplo `AdventureWorks` até a última extensão alocada.  
  
```sql  
DBCC SHRINKDATABASE (AdventureWorks2012, TRUNCATEONLY);  
```  
  
## <a name="see-also"></a>Consulte também  
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
[Reduzir um banco de dados](../../relational-databases/databases/shrink-a-database.md)
  
  
