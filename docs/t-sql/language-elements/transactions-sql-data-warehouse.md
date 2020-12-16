---
title: Transações (Azure Synapse Analytics)
description: Uma transação é um grupo de uma ou mais instruções de banco de dados que são totalmente confirmadas ou totalmente revertidas.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 87e5e593-a121-4428-9d3c-3af876224e35
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 7f22305a8b264b97675fed8949e11fa23f42b42f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464187"
---
# <a name="transactions-azure-synapse-analytics"></a>Transações (Azure Synapse Analytics)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Uma transação é um grupo de uma ou mais instruções de banco de dados que são totalmente confirmadas ou totalmente revertidas. Cada transação tem ACID (atomicidade, consistência, isolamento e durabilidade). Se a transação tiver êxito, todas as instruções dentro dela serão confirmadas. Se a transação falhar, ou seja, se pelo menos uma das instruções no grupo falhar, todo o grupo será revertido.  
  
 O início e o término das transações dependem da configuração de AUTOCOMMIT e das instruções BEGIN TRANSACTION, COMMIT e ROLLBACK. O [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] é compatível com os seguintes tipos de transações:  
  
-   As *transações explícitas* começam com a instrução BEGIN TRANSACTION e terminam com a instrução COMMIT ou ROLLBACK.  
  
-   *Transações de confirmação automática*: começam automaticamente em uma sessão e não começam com a instrução BEGIN TRANSACTION. Quando a configuração de AUTOCOMMIT for ON, cada instrução será executada em uma transação e não será necessária nenhuma instrução COMMIT ou ROLLBACK explícita. Quando a configuração de AUTOCOMMIT for OFF, uma instrução COMMIT ou ROLLBACK será necessária para determinar o resultado da transação. No [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], as transações de confirmação automática começam imediatamente após uma instrução COMMIT ou ROLLBACK, ou após uma instrução SET AUTOCOMMIT OFF.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
BEGIN TRANSACTION [;]  
COMMIT [ TRAN | TRANSACTION | WORK ] [;]  
ROLLBACK [ TRAN | TRANSACTION | WORK ] [;]  
SET AUTOCOMMIT { ON | OFF } [;]  
SET IMPLICIT_TRANSACTIONS { ON | OFF } [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 BEGIN TRANSACTION  
 Marca o ponto inicial de uma transação explícita.  
  
 COMMIT [ WORK ]  
 Marca o fim de uma transação explícita ou de confirmação automática. Essa instrução faz com que as alterações na transação sejam confirmadas permanentemente no banco de dados. A instrução COMMIT é idêntica a COMMIT WORK, COMMIT TRAN e COMMIT TRANSACTION.  
  
 ROLLBACK [ WORK ]  
 Reverte uma transação para o início da transação. Nenhuma alteração da transação é confirmada no banco de dados. A instrução ROLLBACK é idêntica a ROLLBACK WORK, ROLLBACK TRAN e ROLLBACK TRANSACTION.  
  
 SET AUTOCOMMIT { **ON** | OFF }  
 Determina como as transações podem ser iniciadas e terminadas.  
  
 ATIVADO  
 Cada instrução é executada em sua própria transação e não é necessária nenhuma instrução COMMIT ou ROLLBACK explícita. As transações explícitas são permitidas quando AUTOCOMMIT é ON.  
  
 OFF  
 O [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] inicia uma transação automaticamente quando ainda não há uma transação em andamento. Todas as próximas instruções são executadas como parte da transação e a instrução COMMIT ou ROLLBACK é necessária para determinar o resultado da transação. Assim que uma transação é confirmada ou revertida neste modo de operação, o modo permanece OFF e o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] inicia uma nova transação. As transações explícitas não são permitidas quando AUTOCOMMIT é OFF.  
  
 Se você alterar a configuração de AUTOCOMMIT em uma transação ativa, a configuração não afetará a transação atual e não terá nenhum efeito até que a transação seja concluída.  
  
 Se AUTOCOMMIT for ON, executar outra instrução SET AUTOCOMMIT ON como ON não terá nenhum efeito. Da mesma forma, se AUTOCOMMIT for OFF, executar outra SET AUTOCOMMIT OFF não terá nenhum efeito.  
  
 SET IMPLICIT_TRANSACTIONS { ON | **OFF** }  
 Isso alterna os mesmos modos como SET AUTOCOMMIT. Quando ON, SET IMPLICIT_TRANSACTIONS define a conexão em modo de transação implícita. Quando está OFF, ele retorna a conexão para o modo de confirmação automática.  Para obter mais informações, confira [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Nenhuma permissão específica é necessária para executar as instruções relacionadas à transação. São necessárias permissões para executar as instruções dentro da transação.  
  
## <a name="error-handling"></a>Tratamento de erros  
 Se COMMIT ou ROLLBACK for executada e não houver nenhuma transação ativa, um erro será gerado.  
  
 Se BEGIN TRANSACTION for executada enquanto uma transação já estiver em andamento, um erro será gerado. Isso poderá ocorrer se um BEGIN TRANSACTION ocorrer após uma instrução BEGIN TRANSACTION bem-sucedida ou quando a sessão estiver em SET AUTOCOMMIT OFF.  
  
 Se um erro que não seja de instrução de tempo de execução impedir que uma transação explícita seja concluída com sucesso, o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] reverterá a transação e liberará todos os recursos mantidos pela transação automaticamente. Por exemplo, se a conexão de rede do cliente com uma instância do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] for interrompida ou o cliente fizer logoff do aplicativo, todas as transações não confirmadas para a conexão serão revertidas quando a rede notificar a instância sobre a interrupção.  
  
 Se ocorrer um erro de instrução de tempo de execução em um lote, o [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] se comportará de forma consistente com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**XACT_ABORT** definido como **ON** e a transação inteira será revertida. Para obter mais informações sobre a configuração **XACT_ABORT**, confira [SET XACT_ABORT (Transact-SQL)](../statements/set-xact-abort-transact-sql.md).  
  
## <a name="general-remarks"></a>Comentários gerais  
 Uma sessão só pode executar uma única transação em um determinado momento. Não há compatibilidade com pontos de salvamento e transações aninhadas.  
  
 É responsabilidade do programador do [!INCLUDE[DWsql](../../includes/dwsql-md.md)] emitir COMMIT apenas em um momento em que todos os dados referenciados pela transação estejam logicamente corretos.  
  
 Quando uma sessão for terminada antes de uma transação ser concluída, a transação será revertida.  
  
 Os modos de transação são gerenciados no nível da sessão. Por exemplo, se uma sessão começar uma transação explícita ou definir AUTOCOMMIT como OFF ou IMPLICIT_TRANSACTIONS como ON, ela não terá efeito nos modos de transação de nenhuma outra sessão.  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 Não é possível reverter uma transação depois que uma instrução COMMIT é emitida porque as modificações nos dados tornaram-se permanentes no banco de dados.  
  
 Os comandos [CREATE DATABASE &#40;Azure Synapse Analytics&#41;](../statements/create-database-transact-sql.md) e [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md) não podem ser usados dentro de uma transação explícita.  
  
 O [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] não tem nenhum mecanismo de compartilhamento de transação. Isso significa que em um determinado momento, somente uma sessão pode estar executando o trabalho em uma transação no sistema.  
  
## <a name="locking-behavior"></a>Comportamento de bloqueio  
 O [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] usa o bloqueio para garantir a integridade das transações e manter a consistência dos bancos de dados quando vários usuários estão acessando os dados ao mesmo tempo. O bloqueio é usado por transações implícitas e explícitas. Cada transação solicita bloqueios de diferentes tipos de recursos, como tabelas ou bancos de dados dos quais a transação depende. Todos os bloqueios do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ocorrem no nível da tabela ou acima. Os bloqueios não permitem que outras transações modifiquem os recursos de uma maneira que causaria problemas para a transação que solicita o bloqueio. Cada transação libera seus bloqueios quando deixa de depender dos recursos bloqueados. As transações explícitas mantêm os bloqueios até que a transação seja concluída, como confirmada ou revertida.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-an-explicit-transaction"></a>a. Usando uma transação explícita  
  
```sql  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### <a name="b-rolling-back-a-transaction"></a>B. Revertendo uma transação  
 O exemplo a seguir mostra o efeito da reversão de uma transação.  Neste exemplo, a instrução ROLLBACK reverterá a instrução INSERT, mas a tabela criada ainda continuará a existir.  
  
```sql  
CREATE TABLE ValueTable (id INT);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### <a name="c-setting-autocommit"></a>C. Configurando AUTOCOMMIT  
 O exemplo a seguir define a configuração de AUTOCOMMIT como `ON`.  
  
```sql  
SET AUTOCOMMIT ON;  
```  
  
 O exemplo a seguir define a configuração de AUTOCOMMIT como `OFF`.  
  
```sql  
SET AUTOCOMMIT OFF;  
```  
  
### <a name="d-using-an-implicit-multi-statement-transaction"></a>D. Usando uma transação implícita de várias instruções  
  
```sql  
SET AUTOCOMMIT OFF;  
CREATE TABLE ValueTable (id INT);  
INSERT INTO ValueTable VALUES(1);  
INSERT INTO ValueTable VALUES(2);  
COMMIT;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
