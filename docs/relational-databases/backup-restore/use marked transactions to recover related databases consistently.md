---
title: "Usar transa&#231;&#245;es marcadas para recuperar bancos de dados relacionados consistentemente (modelo de recupera&#231;&#227;o completa) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "marcas de transações [SQL Server]"
  - "transações marcadas [SQL Server]"
  - "restaurações de banco de dados [SQL Server], inserindo marcas de transação para"
  - "recuperação [SQL Server], bancos de dados relacionados"
  - "restaurando bancos de dados [SQL Server], recuperação do banco de dados relacionado"
  - "restaurações do banco de dados [SQL Server], bancos de dados relacionados"
  - "transações marcadas [SQL Server], criando"
  - "instrução BEGIN TRAN...WITH MARK"
  - "protocolo 2PC"
ms.assetid: 50a73574-1a69-448e-83dd-9abcc7cb7e1a
caps.latest.revision: 45
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Usar transa&#231;&#245;es marcadas para recuperar bancos de dados relacionados consistentemente (modelo de recupera&#231;&#227;o completa)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tópico é relevante apenas para bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estejam usando modelos de recuperação completa ou bulk-logged.  
  
 Ao fazer atualizações relacionadas a dois ou mais bancos de dados, *bancos de dados relacionados*, você pode usar marcas de transação para recuperá-los a um ponto logicamente consistente. Contudo, essa recuperação perde qualquer transação confirmada após a marca usada como ponto de recuperação. A marcação de uma transação é indicada apenas quando se está testando bancos de dados relacionados, ou se está disposto a perder transações confirmadas recentemente.  
  
 A marcação de transações relacionadas rotineiramente em todo banco de dados relacionado estabelece uma série de pontos de recuperação comuns nesses bancos de dados. As marcas de transação são gravadas no log de transações e incluídas em backups de log. Em caso de desastre, você pode restaurar cada um dos bancos de dados para a mesma marca de transação para recuperá-los em um ponto consistente.  
  
> [!NOTE]  
>  Backups de log em bancos de dados diferentes podem ser criados independentemente um do outro, e não precisam ser simultâneos.  
  
 A recuperação de bancos de dados relacionados nos seguintes cenários exige que você já tenha marcado as transações em todos os bancos de dados relacionados:  
  
-   Um ou mais logs de transações são destruídos. Você deve restaurar o conjunto de bancos de dados em um estado consistente no momento do último backup de log.  
  
-   Você deve restaurar o conjunto inteiro de bancos de dados a um estado mutuamente consistente em algum point-in-time anterior.  
  
> [!IMPORTANT]  
>  Você pode fazer uma recuperação dos bancos de dados relacionados apenas para uma transação marcada, não uma resturação pontual.  
  
 Para obter informações sobre como criar transações de marcação, consulte "Criando transações marcadas", mais adiante neste tópico.  
  
## Cenário típico para o uso de transações marcadas  
 Um cenário típico para o uso de transações marcadas inclui as seguintes etapas:  
  
1.  Crie um backup de banco de dados completo ou diferencial de cada um dos bancos de dados relacionados.  
  
2.  Marque um bloco de transação em todos os bancos de dados.  
  
3.  Faça o backup de log de transações de todos os bancos de dados.  
  
4.  Restaure backups de bancos de dados WITH NORECOVERY.  
  
5.  Restaure logs WITH STOPATMARK.  
  
## Considerações para usar transações marcadas  
 Antes de inserir marcas nomeadas no log de transações, considere o seguinte:  
  
-   Como as marcas de transação consomem espaço de log, só as use para transações que têm um papel significativo na estratégia de recuperação de banco de dados.  
  
-   Depois que a transação marcada é confirmada, uma linha é inserida na tabela [logmarkhistory](../../relational-databases/system-tables/logmarkhistory-transact-sql.md) no **msdb**.  
  
-   Se uma transação marcada abrange vários bancos de dados no mesmo servidor de banco de dados ou em servidores diferentes, as marcas devem ser registradas nos logs de todos os bancos de dados afetados.  
  
## Criando as transações marcadas  
 Para criar uma transação marcada, use a instrução [BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md) e a cláusula WITH MARK [*descrição*]. A *descrição* opcional é uma descrição textual da marca. Um nome de marca da transação é obrigatório. Um nome de marca pode ser usado novamente. O log de transações registra o nome da marca, a descrição, o banco de dados, o usuário, as informações de data e hora e o LSN (número de sequência de log). As informações de data e hora são usadas junto com o nome da marca para identificar a marca com exclusividade.  
  
 **Para criar transações marcadas em um conjunto de bancos de dados:**  
  
1.  Nomeie a transação na instrução BEGIN TRAN e use a cláusula WITH MARK.  
  
     Você pode aninhar a instrução BEGIN TRAN *new_mark_name* WITH MARK dentro de uma transação existente. O valor de *new_mark_name* é o nome da marca para a transação, mesmo se a transação tiver um nome de transação.  
  
    > [!NOTE]  
    >  Se você emitir uma segunda instrução aninhada BEGIN TRAN...WITH MARK, ela será ignorada, mas provocará uma mensagem de aviso.  
  
2.  Execute uma atualização de todos os bancos de dados do conjunto.  
  
     A marca para uma transação específica é inserida em logs de transações apenas na instância de servidor na qual a instrução BEGIN TRAN...WITH MARK é executada. A marca de transações é colocada no log de transações de todos os bancos de dados atualizados pela transação marcada naquela instância de servidor. Se os bancos de dados residirem em instâncias de servidor diferentes, deverão ser criadas marcas idênticas em cada uma das instâncias de servidor.  
  
### Exemplos  
 O exemplo a seguir restaura o log de transações até a marca na transação marcada denominada `ListPriceUpdate`.  
  
```tsql  
USE AdventureWorks  
GO  
BEGIN TRANSACTION ListPriceUpdate  
   WITH MARK 'UPDATE Product list prices';  
GO  
  
UPDATE Production.Product  
   SET ListPrice = ListPrice * 1.10  
   WHERE ProductNumber LIKE 'BK-%';  
GO  
  
COMMIT TRANSACTION ListPriceUpdate;  
GO  
  
-- Time passes. Regular database   
-- and log backups are taken.  
-- An error occurs in the database.  
USE master  
GO  
  
RESTORE DATABASE AdventureWorks  
FROM AdventureWorksBackups  
WITH FILE = 3, NORECOVERY;  
GO  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups   
   WITH FILE = 4,  
   RECOVERY,   
   STOPATMARK = 'ListPriceUpdate';  
```  
  
## Forçando uma marca para ser difundida em outros servidores  
 O nome de uma marca de transação não é automaticamente distribuído para outro servidor à medida que a transação é difundida. Para forçar a difusão da marca em outros servidores, é necessário gravar um procedimento armazenado que contenha uma instrução BEGIN TRAN *name* WITH MARK. Esse procedimento armazenado deve ser executado no servidor remoto dentro do escopo da transação no servidor de origem.  
  
 Por exemplo, considere um banco de dados particionado que exista em várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em cada instância é um banco de dados chamado `coyote`. Primeiro, em todos os bancos de dados, crie um procedimento armazenado, por exemplo, `sp_SetMark`.  
  
```tsql  
CREATE PROCEDURE sp_SetMark  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION @name WITH MARK  
UPDATE coyote.dbo.Marks SET one = 1  
COMMIT TRANSACTION;  
GO  
```  
  
 Em seguida, crie um procedimento armazenado `sp_MarkAll` que contenha uma transação que coloque uma marca em cada banco de dados. `sp_MarkAll` pode ser executado em qualquer instância.  
  
```tsql  
CREATE PROCEDURE sp_MarkAll  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION  
EXEC instance0.coyote.dbo.sp_SetMark @name  
EXEC instance1.coyote.dbo.sp_SetMark @name  
EXEC instance2.coyote.dbo.sp_SetMark @name  
COMMIT TRANSACTION;  
GO  
```  
  
### Protocolo 2PC  
 A confirmação de uma transação distribuída ocorre em duas fases: preparar e confirmar. Quando uma transação marcada é confirmada, o registro de log de confirmação de cada banco de dados na transação marcada é colocado no log em um ponto em que não há nenhuma transação duvidosa em nenhum dos logs. Nesse ponto, há a garantia de que não há nenhuma transação que aparece confirmada em um log, mas não confirmada em outro log.  
  
 As seguintes etapas fazem isso durante a confirmação de uma transação marcada:  
  
1.  A fase de preparação da marcação de transação pausa todas as novas preparações e confirmações.  
  
2.  Somente as confirmações de transações já preparadas podem continuar.  
  
3.  A marcação de transação espera que todas as transações preparadas se esgotem (com tempo limite).  
  
4.  A transação marcada é preparada e confirmada.  
  
5.  A pausa de novas preparações e confirmações é suspensa.  
  
 As pausas geradas por transações marcadas que são estendidas em vários bancos de dados podem diminuir o desempenho do processamento de transações do servidor.  
  
 Não recomendamos a execução de transações marcadas simultâneas. Apesar de ser raro, é possível que a confirmação de uma transação marcada distribuída faça deadlock em outras transações marcadas distribuídas que estejam sendo confirmadas ao mesmo tempo. Quando isso acontece, a marcação da transação é escolhida como vítima de deadlock e é revertida. Quando ocorre esse erro, o aplicativo pode repetir a transação marcada. Quando várias transações marcadas tentam confirmar simultaneamente, a probabilidade de haver deadlock aumenta.  
  
## Recuperando para uma transação marcada  
 Para obter informações sobre como recuperar um banco de dados que contém transações marcadas ou um pouco antes de uma determinada marca, consulte [Recuperação de bancos de dados relacionados que contêm transação marcada](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md).  
  
## Consulte também  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Backups de bancos de dados completos &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [Recuperação de bancos de dados relacionados que contêm transação marcada](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)  
  
  