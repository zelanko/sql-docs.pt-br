---
title: Blocos atômicos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 40e0e749-260c-4cfc-a848-444d30c09d85
caps.latest.revision: 12
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2468e7debaa34b08d40ffedef0a7f078f44343a3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37182303"
---
# <a name="atomic-blocks"></a>Blocos atômicos
  `BEGIN ATOMIC` não faz parte do padrão ANSI SQL. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a blocos atômicos somente no nível superior dos procedimentos armazenados compilados nativamente.  
  
-   Cada procedimento armazenado compilado nativamente contém exatamente um bloco de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] . Esse é um bloco ATOMIC.  
  
-   Os procedimentos armazenados [!INCLUDE[tsql](../../includes/tsql-md.md)] não nativos interpretados e os lotes ad hoc não oferecem suporte a blocos atômicos.  
  
 Os blocos atômicos são executados (atomicamente) na transação. Todas as instruções no bloco foram bem-sucedidas ou o bloco inteiro será revertido para o ponto de salvamento criado no início do bloco. Além disso, as configurações da sessão são corrigidas para o bloco atômico. A execução do mesmo bloco atômico nas sessões com diferentes configurações resultará no mesmo comportamento, independentemente das configurações da sessão atual.  
  
## <a name="transactions-and-error-handling"></a>Transações e tratamento de erros  
 Se uma transação já existir em uma sessão (porque um lote executou uma instrução `BEGIN TRANSACTION` e a transação permanece ativa), iniciar um bloco atômico criará um ponto de salvamento na transação. Se o bloco sair sem uma exceção, um novo ponto de salvamento criado para o bloco é confirmado, mas a transação não será confirmada até que isso ocorra no nível da sessão. Se o bloco lançar uma exceção, os efeitos do bloco serão revertidos, mas a transação no nível da sessão continuará, a menos que a exceção seja decretada por transação. Por exemplo, um conflito de gravação é decretado por transação, mas não um erro de conversão de tipo.  
  
 Se não houver transação ativa em uma sessão, `BEGIN ATOMIC` iniciará uma nova transação. Se nenhuma exceção for lançada fora do escopo do bloco, a transação será confirmada no fim do bloco. Se o bloco lançar uma exceção (ou seja, se a exceção não for capturada e tratada no bloco), a transação será revertida. Para transações que abrangem um único bloco atômico (um único procedimento armazenado compilado nativamente), você não precisa escrever explícito `BEGIN TRANSACTION` e `COMMIT` ou `ROLLBACK` instruções.  
  
 Compilado nativamente suporte a procedimentos armazenados do `TRY`, `CATCH`, e `THROW` construções de tratamento de erros. `RAISERROR` Não há suporte.  
  
 O exemplo a seguir ilustra o comportamento de tratamento de erros com blocos atômicos e procedimentos armazenados compilados nativamente:  
  
```tsql  
-- sample table  
CREATE TABLE dbo.t1 (  
  c1 int not null primary key nonclustered  
)  
WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- sample proc that inserts 2 rows  
CREATE PROCEDURE dbo.usp_t1 @v1 bigint not null, @v2 bigint not null  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC  
WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english', DELAYED_DURABILITY = ON)  
  
  INSERT dbo.t1 VALUES (@v1)  
  INSERT dbo.t1 VALUES (@v2)  
  
END  
GO  
  
-- insert two rows  
EXEC dbo.usp_t1 1, 2  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify the rows 1 and 2 were committed  
SELECT c1 FROM dbo.t1  
GO  
  
-- execute proc with arithmetic overflow  
EXEC dbo.usp_t1 3, 4444444444444  
GO  
-- expected error message:  
-- Msg 8115, Level 16, State 0, Procedure usp_t1  
-- Arithmetic overflow error converting bigint to data type int.  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 was not committed; usp_t1 has been rolled back  
SELECT c1 FROM dbo.t1  
GO  
  
-- start a new transaction  
BEGIN TRANSACTION  
  -- insert rows 3 and 4  
  EXEC dbo.usp_t1 3, 4  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify the rows 3 and 4 were inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
  -- catch the arithmetic overflow error  
  BEGIN TRY  
    EXEC dbo.usp_t1 5, 4444444444444  
  END TRY  
  BEGIN CATCH  
    PRINT N'Error occurred: ' + error_message()  
  END CATCH  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify rows 3 and 4 are still in the table, and row 5 has not been inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
COMMIT  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 and 4 has been committed  
SELECT c1 FROM dbo.t1  
ORDER BY c1  
GO  
```  
  
 As mensagens de erro a seguir específicas de tabelas com otimização de memória são decretadas por transação. Se elas ocorrerem no escopo de um bloco atômico, a transação será anulada: 10772, 41301, 41302, 41305, 41325, 41332 e 41333.  
  
## <a name="session-settings"></a>Configurações da sessão  
 As configurações da sessão nos blocos atômicos são corrigidas quando o procedimento armazenado é compilado. Algumas configurações podem ser especificadas com `BEGIN ATOMIC` enquanto outras configurações sempre são corrigidas para o mesmo valor.  
  
 As seguintes opções são necessárias com `BEGIN ATOMIC`:  
  
|Configuração necessária|Description|  
|----------------------|-----------------|  
|`TRANSACTION ISOLATION LEVEL`|Valores com suporte são `SNAPSHOT`, `REPEATABLEREAD`, e `SERIALIZABLE`.|  
|`LANGUAGE`|Determina os formatos de data e hora, e as mensagens do sistema. Todos os idiomas e alias em [sys.syslanguages &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql) têm suporte.|  
  
 As seguintes configurações são opcionais:  
  
|Configuração opcional|Description|  
|----------------------|-----------------|  
|`DATEFORMAT`|Há suporte para todos os formatos de data do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando especificado, `DATEFORMAT` substitui o formato de data padrão associado com `LANGUAGE`.|  
|`DATEFIRST`|Quando especificado, `DATEFIRST` substitui o padrão associado a `LANGUAGE`.|  
|`DELAYED_DURABILITY`|Valores com suporte são `OFF` e `ON`.<br /><br /> Confirmações de transação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser completamente duráveis, o padrão ou duráveis atrasadas. Para obter mais informações, consulte [Controlar a durabilidade da transação](../logs/control-transaction-durability.md).|  
  
 As opções SET a seguir têm o mesmo valor padrão de sistema para todos os blocos atômicos em todos os procedimentos armazenados compilados nativamente:  
  
|Opção Set|Padrão do sistema para blocos atômicos|  
|----------------|--------------------------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNING|ON|  
|ARITHABORT|ON|  
|ARITHIGNORE|OFF|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|IDENTITY_INSERT|OFF|  
|NOCOUNT|ON|  
|NUMERIC_ROUNDABORT|DESATIVADO|  
|QUOTED_IDENTIFIER|ON|  
|ROWCOUNT|0|  
|TEXTSIZE|0|  
|XACT_ABORT|OFF<br /><br /> As exceções não capturadas fazem com que o bloco atômico seja revertido, mas não fazem com que a transação seja anulada, a menos que o erro seja decretado por transação.|  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados compilados nativamente](natively-compiled-stored-procedures.md)  
  
  
