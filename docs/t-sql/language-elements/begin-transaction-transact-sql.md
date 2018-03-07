---
title: BEGIN TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BEGIN_TRANSACTION_TSQL
- TRANSACTION_TSQL
- TRANSACTION
- BEGIN TRANSACTION
- BEGIN TRAN
- BEGIN_TRAN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction logs [SQL Server], BEGIN TRANSACTION statement
- marked transactions [SQL Server], BEGIN TRANSACTION statement
- BEGIN TRANSACTION statement
- local transactions [SQL Server]
- marking transactions [SQL Server]
- transactions [SQL Server], starting
- transaction names [SQL Server]
- starting point marked for transactions
- starting transactions
ms.assetid: c6258df4-11f1-416a-816b-54f98c11145e
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 260399c0964afeeafc0f8a221de13169ef277496
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="begin-transaction-transact-sql"></a>BEGIN TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Marca o ponto inicial de uma transação local explícita. Transações explícitas começam com a instrução BEGIN TRANSACTION e terminam com a instrução COMMIT ou ROLLBACK.  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
--Applies to SQL Server and Azure SQL Database
 
BEGIN { TRAN | TRANSACTION }   
    [ { transaction_name | @tran_name_variable }  
      [ WITH MARK [ 'description' ] ]  
    ]  
[ ; ]  
```  
 
```  
--Applies to Azure SQL Data Warehouse and Parallel Data Warehouse
 
BEGIN { TRAN | TRANSACTION }   
[ ; ]  
```  

  
## <a name="arguments"></a>Argumentos  
 *transaction_name*  
 **Aplica-se a:** SQL Server (começando com o 2008), o banco de dados do SQL Azure
 
 É o nome atribuído à transação. *transaction_name* devem estar em conformidade com as regras para identificadores, mas identificadores maiores que 32 caracteres não são permitidos. Somente use nomes de transação no par externo de instruções aninhadas BEGIN ...COMMIT ou BEGIN...ROLLBACK. *transaction_name* é sempre maiusculas e minúsculas, mesmo quando a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não diferencia maiusculas de minúsculas.  
  
 @*tran_name_variable*  
 **Aplica-se a:** SQL Server (começando com o 2008), o banco de dados do SQL Azure
 
 É o nome de uma variável definida pelo usuário que contém um nome de transação válido. A variável deve ser declarada com uma **char**, **varchar**, **nchar**, ou **nvarchar** tipo de dados. Se mais de 32 caracteres forem transmitidos à variável, apenas os primeiros 32 caracteres serão usados, os demais serão truncados.  
  
 WITH MARK ['*descrição*']  
**Aplica-se a:** SQL Server (começando com o 2008), o banco de dados do SQL Azure

Especifica que a transação é marcada no log. *Descrição* é uma cadeia de caracteres que descreve a marca. Um *descrição* mais de 128 caracteres é truncado para 128 caracteres antes de serem armazenados na tabela msdb.dbo.  
  
 Se WITH MARK for usado, o nome da transação deverá ser especificado. WITH MARK permite restaurar um log de transações para uma indicação nomeada.  
  
## <a name="general-remarks"></a>Comentários gerais
BEGIN TRANSACTION incrementa@TRANCOUNT em 1.
  
BEGIN TRANSACTION representa um ponto no qual os dados referenciados por uma conexão são lógica e fisicamente consistentes. Se forem encontrados erros, todas as modificações de dados feitas depois do BEGIN TRANSACTION poderão ser revertidas para voltar os dados ao estado conhecido de consistência. Cada transação dura até ser completada sem erros e COMMIT TRANSACTION é emitido para tornar as modificações parte permanente do banco de dados, ou são encontrados erros e todas as modificações são removidas com uma instrução ROLLBACK TRANSACTION.  
  
BEGIN TRANSACTION inicia uma transação local para a conexão que emite a instrução. Dependendo das configurações de nível de isolamento da transação atual, muitos recursos adquiridos para aceitar as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] emitidas pela conexão são fechados pela transação, até que seja completada com uma instrução COMMIT TRANSACTION ou ROLLBACK TRANSACTION. Transações pendentes por longos períodos de tempo podem impedir outros usuários de acessar estes recursos bloqueados e também podem prevenir a operação de truncar o log.  
  
 Embora BEGIN TRANSACTION inicie uma transação local, não é registrado no log de transações até que o aplicativo execute subsequentemente uma ação que deve ser registrada no log, como executar uma instrução INSERT, UPDATE ou DELETE. Um aplicativo pode executar ações como adquirir bloqueios para proteger o nível de isolamento da transação de instruções SELECT, mas nada é registrado no log até que o aplicativo execute uma ação de modificação.  
  
 Nomear múltiplas transações em uma série de transações aninhadas com um nome de transação tem pouco efeito na transação. Somente o primeiro nome da transação (externo) é registrado no sistema. Uma reversão para qualquer outro nome (diferente de um nome de ponto de salvamento válido) gera um erro. Nenhuma das instruções executadas antes da reversão são, na realidade, revertidas quando ocorre o erro. As instruções são revertidas somente quando a transação externa é revertida.  
  
 A transação local que foi iniciada pela instrução BEGIN TRANSACTION será escalada para uma transação distribuída, se as seguintes ações forem executadas antes de a instrução ser confirmada ou revertida:  
  
-   Uma instrução de INSERT, DELETE ou UPDATE que faz referência a uma tabela remota em um servidor vinculado é executada. A instrução INSERT, UPDATE ou DELETE falhará se o provedor de OLE DB usado para acessar o servidor vinculado não suporta a interface ITransactionJoin.  
  
-   Uma chamada é feita para um procedimento armazenado remoto quando a opção REMOTE_PROC_TRANSACTIONS é definida como ON.  
  
 A cópia local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se torna o controlador da transação e usa o MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)]) para gerenciar a transação distribuída.  
  
 Uma transação pode ser executada explicitamente como uma transação distribuída usando BEGIN DISTRIBUTED TRANSACTION. Para obter mais informações, consulte [BEGIN DISTRIBUTED TRANSACTION &#40; Transact-SQL &#41; ](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md).  
  
 Quando SET IMPLICIT_TRANSACTIONS está definida como ON, a instrução BEGIN TRANSACTION cria duas transações aninhadas. Para obter mais informações, consulte [SET IMPLICIT_TRANSACTIONS &#40; Transact-SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)  
  
## <a name="marked-transactions"></a>Transações marcadas  
 A opção WITH MARK faz com que o nome da transação ser inserido no log de transações. Ao restaurar um banco de dados a um estado anterior, a transação marcada pode ser usada em lugar de uma data e hora. Para obter mais informações, consulte [usar transações marcadas para recuperar bancos de dados relacionados consistentemente &#40; Modelo de recuperação completa &#41; ](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md) e [restauração &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-transact-sql.md).  
  
 Além disso, as marcas de log de transações serão necessárias se você precisar recuperar um conjunto de bancos de dados relacionados a um estado logicamente consistente. Prefixos podem ser colocados nos logs de transação dos bancos de dados relacionados por meio de uma transação distribuída. Recuperar o conjunto de bancos de dados relacionados a estes prefixos resulta em um conjunto de bancos de dados que são transacionalmente consistentes. A inserção de marcas em bancos de dados relacionados requer procedimentos especiais.  
  
 A marca é inserida no log de transações somente se o banco de dados for atualizado pela transação marcada. As transações que não modificam dados não têm prefixos.  
  
 BEGIN TRAN *novo_nome* WITH MARK podem ser aninhada dentro de uma transação já existente que não está marcada. Ao fazer isso, *novo_nome* torna-se o nome da marca da transação, apesar do nome que a transação pode já ter sido fornecida. No exemplo a seguir, `M2` é o nome do prefixo.  
  
```  
BEGIN TRAN T1;  
UPDATE table1 ...;  
BEGIN TRAN M2 WITH MARK;  
UPDATE table2 ...;  
SELECT * from table1;  
COMMIT TRAN M2;  
UPDATE table3 ...;  
COMMIT TRAN T1;  
```  
  
 Ao aninhar transações, tentando marcar uma transação que já possui resultados marcados em uma mensagem de aviso (não um erro):  
  
 "BEGIN TRAN T1 WITH MARK ...;"  
  
 "UPDATE table1 ...;"  
  
 "BEGIN TRAN M2 WITH MARK ...;"  
  
 "Server: Msg 3920, Level 16, State 1, Line 3"  
  
 “A opção WITH MARK é aplicável somente ao primeiro BEGIN TRAN WITH MARK."  
  
 "A opção é ignorada."  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-an-explicit-transaction"></a>A. Usando uma transação explícita
**Aplica-se a:** SQL Server (começando com o 2008), o banco de dados do SQL Azure, o Azure SQL Data Warehouse, Parallel Data Warehouse

Este exemplo usa o AdventureWorks. 

```
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```

### <a name="b-rolling-back-a-transaction"></a>B. Reverter uma transação
**Aplica-se a:** SQL Server (começando com o 2008), o banco de dados do SQL Azure, o Azure SQL Data Warehouse, Parallel Data Warehouse

O exemplo a seguir mostra o efeito da reversão de uma transação. Neste exemplo, a instrução ROLLBACK reverterá a instrução INSERT, mas a tabela criada ainda existirão.

```
 
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  

```

### <a name="c-naming-a-transaction"></a>C. Nomeando uma transação 
**Aplica-se a:** SQL Server (começando com o 2008), o banco de dados do SQL Azure

O exemplo a seguir mostra como nomear uma transação.  
  
```  
DECLARE @TranName VARCHAR(20);  
SELECT @TranName = 'MyTransaction';  
  
BEGIN TRANSACTION @TranName;  
USE AdventureWorks2012;  
DELETE FROM AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
  
COMMIT TRANSACTION @TranName;  
GO  
```  
  
### <a name="d-marking-a-transaction"></a>D. Marcando uma transação  
**Aplica-se a:** SQL Server (começando com o 2008), o banco de dados do SQL Azure

O exemplo a seguir mostra como marcar uma transação. A transação `CandidateDelete` é marcada.  
  
```  
BEGIN TRANSACTION CandidateDelete  
    WITH MARK N'Deleting a Job Candidate';  
GO  
USE AdventureWorks2012;  
GO  
DELETE FROM AdventureWorks2012.HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
GO  
COMMIT TRANSACTION CandidateDelete;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  
