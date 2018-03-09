---
title: "Transações (SQL Data Warehouse) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 87e5e593-a121-4428-9d3c-3af876224e35
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4ea7244857dcd25b1e36f3420811ef035d4ee3b2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="transactions-sql-data-warehouse"></a>Transações (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Uma transação é um grupo de uma ou mais instruções de banco de dados que são totalmente confirmada ou revertida inteiramente. Cada transação é atômico, consistente, isolado e durável (ACID). Se a transação tiver êxito, todas as instruções dentro dele são confirmadas. Se a transação falhar, que é pelo menos uma das instruções no grupo falha, todo o grupo é revertido.  
  
 O início e término de transações depende da configuração de confirmação automática e as instruções BEGIN TRANSACTION, COMMIT e ROLLBACK. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]suporta os seguintes tipos de transações:  
  
-   *Transações explícitas* começam com a instrução BEGIN TRANSACTION e terminam com a instrução COMMIT ou ROLLBACK.  
  
-   *Transações de confirmação automática* iniciar automaticamente em uma sessão e não começam com a instrução BEGIN TRANSACTION. Quando a configuração de confirmação automática for ON, cada instrução é executada em uma transação e nenhuma explícita confirmação ou REVERSÃO é necessária. Quando a configuração de confirmação automática for OFF, uma instrução COMMIT ou ROLLBACK é necessário para determinar o resultado da transação. Em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], transações de confirmação automática começarem imediatamente após uma instrução COMMIT ou ROLLBACK, ou após uma instrução SET AUTOCOMMIT OFF.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
BEGIN TRANSACTION [;]  
COMMIT [ TRAN | TRANSACTION | WORK ] [;]  
ROLLBACK [ TRAN | TRANSACTION | WORK ] [;]  
SET AUTOCOMMIT { ON | OFF } [;]  
SET IMPLICIT_TRANSACTIONS { ON | OFF } [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 BEGIN TRANSACTION  
 Marca o ponto de partida de uma transação explícita.  
  
 CONFIRMAÇÃO [TRABALHO]  
 Marca o fim de uma transação explícita ou confirmação automática. Essa instrução faz com que as alterações na transação confirmada permanentemente no banco de dados. A instrução COMMIT é idêntico ao COMMIT TRANSACTION, COMMIT TRAN e COMMIT WORK.  
  
 REVERSÃO [TRABALHO]  
 Reverte uma transação para o início da transação. Nenhuma alteração para a transação é confirmada no banco de dados. A instrução ROLLBACK é idêntico ao ROLLBACK WORK, ROLLBACK TRAN e ROLLBACK TRANSACTION.  
  
 CONFIRMAÇÃO AUTOMÁTICA DO CONJUNTO { **ON** | OFF}  
 Determina como as transações podem iniciar e terminar.  
  
 ON  
 Cada instrução é executada em sua própria transação e nenhuma instrução COMMIT ou ROLLBACK explícita é necessária. Transações explícitas são permitidas quando a confirmação automática está ativada.  
  
 OFF  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]inicia uma transação automaticamente quando uma transação ainda não está em andamento. Todas as instruções subsequentes são executadas como parte da transação e COMMIT ou ROLLBACK é necessária para determinar o resultado da transação. Assim que uma transação é confirmada ou revertida neste modo de operação, o modo permaneça em OFF, e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] inicia uma nova transação. Transações explícitas não são permitidas quando a confirmação automática é desativada.  
  
 Se você alterar a configuração de confirmação automática em uma transação ativa, a configuração afeta a transação atual e não têm efeito até que a transação seja concluída.  
  
 Se a confirmação automática for ON, executar outra instrução de confirmação automática definida como ON não tem nenhum efeito. Da mesma forma, se a confirmação automática for OFF, executar outro SET AUTOCOMMIT OFF não tem nenhum efeito.  
  
 SET IMPLICIT_TRANSACTIONS {ON | **OFF** }  
 Isso alterna os modos mesmo como AUTOCOMMIT definido. Quando ON, SET IMPLICIT_TRANSACTIONS define a conexão em modo de transação implícita. Quando OFF, ele retorna a conexão para o modo de confirmação automática.  Para obter mais informações, consulte [SET IMPLICIT_TRANSACTIONS &#40; Transact-SQL &#41; ](../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Nenhuma permissão específica é necessária para executar as instruções relacionadas à transação. São necessárias permissões para executar as instruções dentro da transação.  
  
## <a name="error-handling"></a>Tratamento de erros  
 Se a confirmação ou REVERSÃO são executados, e não há nenhuma transação ativa, um erro é gerado.  
  
 Se um BEGIN TRANSACTION é executado enquanto uma transação já está em andamento, um erro será gerado. Isso pode ocorrer se um BEGIN TRANSACTION ocorre após uma instrução BEGIN TRANSACTION bem-sucedida ou quando a sessão está em SET AUTOCOMMIT OFF.  
  
 Se um erro que não seja um erro de tempo de execução de instrução impede a conclusão bem-sucedida de uma transação explícita, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] reverte a transação e libera todos os recursos mantidos pela transação automaticamente. Por exemplo, se conexão de rede do cliente para uma instância de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] for interrompida ou o cliente fizer logoff do aplicativo, todas as transações não confirmadas para a conexão serão revertidas quando a rede notificar a instância da quebra.  
  
 Se ocorrer um erro de tempo de execução de instrução em um lote, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] se comporta consistente com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **XACT_ABORT** definida como **ON** e a transação inteira é revertida. Para obter mais informações sobre o **XACT_ABORT** configuração, consulte [SET XACT_ABORT (Transact-SQL)](http://msdn.microsoft.com/library/ms188792.aspx).  
  
## <a name="general-remarks"></a>Comentários gerais  
 Uma sessão só pode executar uma transação em um determinado momento; Não há suporte para pontos de salvamento e transações aninhadas.  
  
 É responsabilidade do [!INCLUDE[DWsql](../../includes/dwsql-md.md)] programador emitir confirmação apenas em um momento quando todos os dados referidos pela transação esteja logicamente correto.  
  
 Quando uma sessão é encerrada antes de uma transação é concluída, a transação será revertida.  
  
 Modos de transação são gerenciados no nível da sessão. Por exemplo, se uma sessão começa uma transação explícita ou define a confirmação automática como OFF ou define IMPLICIT_TRANSACTIONS como ON, ele não terá efeito nos modos de transação de qualquer outra sessão.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Não é possível reverter uma transação depois que uma instrução COMMIT é emitida porque as modificações de dados foi feitas uma parte permanente do banco de dados.  
  
 O [criar banco de dados &#40; Depósito de dados SQL do Azure &#41; ](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) e [descartar o banco de dados &#40; Transact-SQL &#41; ](../../t-sql/statements/drop-database-transact-sql.md) comandos não podem ser usados dentro de uma transação explícita.  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]não tem uma transação de mecanismo de compartilhamento. Isso significa que em qualquer ponto no tempo, somente uma sessão pode estar executando o trabalho em qualquer transação no sistema.  
  
## <a name="locking-behavior"></a>Comportamento de bloqueio  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]usa bloqueio para garantir a integridade de transações e manter a consistência de bancos de dados quando vários usuários estão acessando os dados ao mesmo tempo. O bloqueio é usado por transações implícitas e explícitas. Cada transação solicita bloqueios de tipos diferentes de recursos, como tabelas ou bancos de dados do qual depende a transação. Todos os [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] bloqueios são tabela nível ou superior. Os bloqueios não permitem que outras transações modifiquem os recursos de uma maneira que causaria problemas para a transação que solicita o bloqueio. Cada transação libera seus bloqueios quando ele não tem uma dependência dos recursos bloqueados; transações explícitas mantêm bloqueios até que a transação é concluída quando ele for confirmado ou revertido.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-an-explicit-transaction"></a>A. Usando uma transação explícita  
  
```  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### <a name="b-rolling-back-a-transaction"></a>B. Reverter uma transação  
 O exemplo a seguir mostra o efeito da reversão de uma transação.  Neste exemplo, a instrução ROLLBACK reverterá a instrução INSERT, mas a tabela criada ainda existirão.  
  
```  
CREATE TABLE ValueTable (id int);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### <a name="c-setting-autocommit"></a>C. Configuração de confirmação automática  
 O exemplo a seguir define a configuração de confirmação automática `ON`.  
  
```  
SET AUTOCOMMIT ON;  
```  
  
 O exemplo a seguir define a configuração de confirmação automática `OFF`.  
  
```  
SET AUTOCOMMIT OFF;  
```  
  
### <a name="d-using-an-implicit-multi-statement-transaction"></a>D. Usando uma transação implícita de várias instruções  
  
```  
SET AUTOCOMMIT OFF;  
CREATE TABLE ValueTable (id int);  
INSERT INTO ValueTable VALUES(1);  
INSERT INTO ValueTable VALUES(2);  
COMMIT;  
```  
  
## <a name="see-also"></a>Consulte também  
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  
