---
description: MSSQLSERVER_3414
title: MSSQLSERVER_3414 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3414 (Database Engine error)
ms.assetid: f25852f9-b91c-4356-b817-78bec9ec8db4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a7a7d69c27ed422763c5c697f003ba9fb4c82286
ms.sourcegitcommit: a0245fdae1ff9045f587a3a67b72f34405d35a4f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88618093"
---
# <a name="mssqlserver_3414"></a>MSSQLSERVER_3414
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|3414|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|REC_GIVEUP|  
|Texto da mensagem|Erro durante a recuperação, o que impede a reinicialização do banco de dados '%.*ls' (ID do banco de dados %d). Diagnostique os erros de recuperação e corrija-os ou restaure usando um backup válido. Se os erros não forem corrigidos ou se não eram esperados, entre em contato com o Suporte Técnico.|  
  
## <a name="explanation"></a>Explicação  
O banco de dados especificado foi recuperado, mas não foi iniciado, porque aconteceram erros durante a recuperação. Esse erro colocou o banco de dados no estado SUSPECT. O grupo de arquivos primário, e possivelmente outros grupos de arquivos, estão sob suspeita e podem estar danificados. O banco de dados não pode ser recuperado durante a inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, portanto, não está disponível. Ação do usuário é necessária para resolver o problema. Você verá o status SUSPECT no SQL Server Management Studio (ao lado do ícone do banco de dados) e na coluna sys.databases.state_desc. Qualquer tentativa de usar um banco de dados nesse estado resultará no seguinte erro:

```
Msg 926, Level 14, State 1, Line 1 
Database 'mydb' cannot be opened. It has been marked SUSPECT by recovery. See the SQL Server errorlog for more information
```
  
Observe que, se esse erro ocorrer em **tempdb**, a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será desligada.  

## <a name="cause"></a>Causa
Este erro pode ser causado por uma condição transitória existente no sistema durante uma determinada tentativa de iniciar a instância de servidor ou recuperar um banco de dados. Este erro também pode ser causado por uma falha permanente que ocorre toda vez que você tenta iniciar o banco de dados. A causa da falha de recuperação normalmente é encontrada nos erros que precedem o erro 3414 no ERRORLOG ou no Log de Eventos. O erro anterior no arquivo de log contém o mesmo valor de SPID<n>. Por exemplo, a falha de recuperação a seguir ocorre devido a um erro na soma de verificação ao tentar ler um bloco do log. Observe que o *SPID15s* está presente em todas as linhas:

```
2020-03-31 17:33:13.00 spid15s     Error: 824, Severity: 24, State: 4.  
2020-03-31 17:33:13.00 spid15s     SQL Server detected a logical consistency-based I/O error: (bad checksum). It occurred during a read of page (0:-1) in database ID 13 at offset 0x0000000000b800 in file 'C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\mydb_log.LDF'.  Additional messages in the SQL Server error log or system event log may provide more detail. This is a severe error condition that threatens database integrity and must be corrected immediately. Complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.   
2020-03-31 17:33:13.16 spid15s     Error: 3414, Severity: 21, State: 1.  
2020-03-31 17:33:13.16 spid15s     An error occurred during recovery, preventing the database 'mydb' (database ID 13) from restarting. Diagnose the recovery errors and fix them, or restore from a known good backup. If errors are not corrected or expected, contact Technical Support
```


Há uma ampla variedade de erros que podem causar falha na recuperação do banco de dados. Embora seja necessário avaliar os erros caso a caso, a resolução de uma falha de recuperação de banco de dados geralmente é a mesma descrita na seção Ação do Usuário, abaixo.

## <a name="user-action"></a>Ação do usuário  
 
Para obter informações sobre a causa dessa ocorrência do erro 3414, examine o Log de Eventos do Windows ou o ERRORLOG para encontrar um erro anterior que indique a falha específica. A ação do usuário adequada depende de se as informações no Log de Eventos do Windows indicam se o erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi provocado por uma condição transitória ou por uma falha permanente. A mensagem de erro informa "Diagnostique os erros de recuperação e corrija-os ou restaure usando um backup válido". Portanto, você pode tentar corrigir o erro encontrado para permitir que a recuperação seja concluída (confira [Erros corrigíveis e transações adiadas](#correctable-errors-and-deferred-transactions)).

Se os erros não puderem ser corrigidos, a primeira e melhor opção para resolver o problema será restaurar usando um backup válido. No entanto, se não for possível recuperar usando um backup, você terá duas opções adicionais, que não garantem a recuperação total dos dados: usar o reparo de emergência com o [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ou tentar copiar o máximo de dados possível para outro banco de dados. 

 1. Restaurar usando o último backup de banco de dados válido conhecido
 1. Usar o método de reparo de emergência fornecido pelo [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)
 1. Tentar copiar o máximo de dados possível para outro banco de dados.

O primeiro método de restauração usando um backup válido de banco de dados é a melhor opção para colocar um banco de dados em um estado consistente conhecido.  

A segunda melhor opção, se não houver nenhum backup válido disponível, é colocar o banco de dados online e torná-lo acessível. No entanto, nesse caso, é preciso observar que a consistência transacional não poderá ser garantida uma vez que a recuperação falhou. Não há como saber quais transações deveriam ter sido revertidas ou tido o roll forward efetuado, mas tal operação não fora permitida devido à falha de recuperação. As etapas para prosseguir com o reparo de emergência são descritas na seção intitulada [Resolvendo erros de banco de dados no modo de emergência](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md#resolving-errors-in-database-emergency-mode) da documentação do DBCC CHECKDB. 

Se o reparo de emergência não funcionar e você quiser tentar salvar alguns dados em outro banco de dados, a maneira de obter acesso ao banco de dado é colocando-o em modo de emergência por meio do comando ALTER DATABASE <dbname> SET EMERGENCY. Em seguida, você pode tentar copiar os dados das tabelas.

### <a name="correctable-errors-and-deferred-transactions"></a>Erros corrigíveis e transações adiadas
Nem todos os erros encontrados durante a recuperação de um banco de dados resultarão em falha de recuperação e em um banco de dados suspeito:

erros ao abrir o banco de dados e/ou os arquivos de log de transações pela primeira vez ocorrem antes da recuperação. Exemplos desses erros são [17204](mssqlserver-17204-database-engine-error.md) e [17207](mssqlserver-17207-database-engine-error.md). Depois que esses erros forem corrigidos, a recuperação poderá ter permissão para continuar (mas ainda não há garantia de que será concluída já que podem ocorrer outros erros de recuperação). Erros como 17204 e 17207 não resultam em um banco de dados com status SUSPECT. Na verdade, o status do banco de dados quando ocorrerem esses problemas será RECOVERY_PENDING. 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permitirá que a recuperação seja concluída mesmo quando ocorrer um erro no nível da página e ainda manterá a consistência transacional. Esse processo reduziu o número de cenários que resultam em um banco de dados com status SUSPECT. Esse conceito é chamado de [transações adiadas](../backup-restore/deferred-transactions-sql-server.md).

Se o erro encontrado durante a recuperação indicar um problema com uma página de um banco de dados (por exemplo, como um erro de soma de verificação ou uma mensagem de erro 824), a recuperação pode ter permissão para ser concluída com erros pendentes. Caso uma transação não seja confirmada, um erro em uma página pode resultar em uma [transação adiada](../backup-restore/deferred-transactions-sql-server.md) e permitir a conclusão da recuperação.  

As entradas do ERRORLOG a seguir mostram um exemplo de erro encontrado durante a recuperação com a mensagem de erro [824](mssqlserver-824-database-engine-error.md), mas a recuperação teve sua conclusão permitida com uma transação adiada. Observe a ausência do erro 3414 nessa situação e a mensagem informando que a recuperação foi concluída para o banco de dados:

```2010-03-31 19:17:18.45 spid7s      Error: 824, Severity: 24, State: 2.   
2010-03-31 19:17:18.45 spid7s      SQL Server detected a logical consistency-based I/O error: incorrect checksum (expected: 0xb2c87a0a; actual: 0xb6c0a5e2). It occurred during a read of page (1:153) in database ID 13 at offset 0x00000000132000 in file 'C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\mydb.mdf'.  Additional messages in the SQL Server error log or system event log may provide more detail. This is a severe error condition that threatens database integrity and must be corrected immediately. Complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.   
2010-03-31 19:17:18.45 spid7s      Error: 3314, Severity: 21, State: 1.   
2010-03-31 19:17:18.45 spid7s      During undoing of a logged operation in database 'mydb', an error occurred at log record ID (25:100:19). Typically, the specific failure is logged previously as an error in the Windows Event Log service. Restore the database or file from a backup, or repair the database.
2010-03-31 19:17:18.45 spid7s      Errors occurred during recovery while rolling back a transaction. The transaction was deferred. Restore the bad page or file, and re-run recovery.   
2010-03-31 19:17:18.45 spid7s      Recovery completed for database mydb (database ID 13) in 2 second(s) (analysis 204 ms, redo 25 ms, undo 1832 ms.) This is an informational message only. No user action is required.   
```

Se for para efetuar roll forward em uma transação confirmada, a página poderá ser marcada como inacessível (qualquer tentativa futura de acessar a página resultará na mensagem de erro 829) e a recuperação poderá ser concluída. Nessa situação, o erro deverá ser corrigido restaurando a página usando um backup ou desalocando a página usando o método de reparo do DBCC CHECKDB.


  
## <a name="see-also"></a>Confira também  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](~/relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
[Transações adiadas](../backup-restore/deferred-transactions-sql-server.md)  
[MSSQLSERVER_824](~/relational-databases/errors-events/mssqlserver-824-database-engine-error.md)  
[sys.databases &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)

  
