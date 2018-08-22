---
title: Diretrizes para lógica de repetição para transações em tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f2a35c37-4449-49ee-8bba-928028f1de66
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 86c97342ff2a9e3ed3facb6612c0899c3b436edc
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40396027"
---
# <a name="guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables"></a>Diretrizes para lógica de repetição das transações em tabelas com otimização de memória
  Há condições de erro que ocorrem com transações que acessam tabelas com otimização de memória.  
  
-   41302. A transação atual tentou atualizar um registro que foi atualizado desde que a transação foi iniciada.  
  
-   41305. A transação atual não foi confirmada devido a uma falha de validação de leitura repetida.  
  
-   41325. A transação atual não foi confirmada devido a uma falha de validação serializável.  
  
-   41301. Uma transação anterior na qual a transação atual obteve uma dependência foi anulada, e a transação atual não pode mais ser confirmada.  
  
 Uma causa comum desses erros é a interferência entre a transação executada simultaneamente. A ação corretiva comum é repetir a transação.  
  
 Para obter mais informações sobre essas condições de erro, consulte a seção sobre detecção de conflito, validação e verificações de dependência de confirmação em [transações em tabelas com otimização de memória](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 Os deadlocks (código de erro 1205) não podem ocorrer em tabelas com otimização de memória. Os bloqueios não são usados em tabelas com otimização de memória. No entanto, se o aplicativo já contiver a lógica de repetição de deadlocks, a lógica existente pode ser estendida para incluir os novos códigos de erro.  
  
## <a name="considerations-for-retrying"></a>Considerações sobre repetição  
 Os aplicativos normalmente encontrarão conflitos entre transações e precisarão implementar a lógica de repetição para resolver esses conflitos. O número de conflitos encontrados depende de vários fatores:  
  
-   Contenção para linhas individuais. O potencial para conflitos aumenta à medida que o número de transações que tentam atualizar a mesma linha aumenta.  
  
-   O número de linhas lidas pelas transações REPEATABLE READ. Quanto mais linhas forem lidas, maior a possibilidade de algumas dessas linhas serem atualizadas por transações simultâneas. Isso causa falhas de validação de leitura repetida.  
  
-   Tamanho dos intervalos de verificação usados pelas transações SERIALIZABLE. Quanto maior o intervalo de verificação, maior a possibilidade de as transações simultâneas inserirem linhas fantasmas, provocando falhas de validação serializável.  
  
     É difícil para um aplicativo evitar esses conflitos, o que exige uma lógica de repetição.  
  
> [!IMPORTANT]  
>  As transações de leitura/gravação que acessam tabelas com otimização de memória exigem a lógica de repetição.  
  
### <a name="considerations-for-read-only-transactions-and-natively-compiled-stored-procedures"></a>Considerações sobre transações somente leitura e procedimentos armazenados compilados nativamente  
 As transações somente leitura que abrangem uma única execução de um procedimento armazenado compilado nativamente não requer a validação de transações REPEATABLE READ e SERIALIZABLE. Os conflitos de gravação não podem ocorrer quando uma transação é somente leitura.  
  
 No entanto, as falhas de dependência ainda podem ocorrer. As falhas de dependência são mais raras do que os erros resultantes dos conflitos. Portanto, em muitos casos, uma lógica de repetição específica não é necessária em transações somente leitura que abrangem execuções únicas de procedimentos armazenados compilados nativamente.  
  
### <a name="considerations-for-read-only-transactions-and-cross-container-transactions"></a>Considerações sobre transações somente leitura e transações entre contêineres  
 As transações somente leitura entre contêineres, que são as transações iniciadas fora do contexto de um procedimento armazenado compilado nativamente, não executarão a validação se as tabelas com otimização de memória forem acessadas no isolamento SNAPSHOT. No entanto, quando as tabelas com otimização de memória forem acessadas no isolamento REPEATABLE READ ou SERIALIZABLE, a validação será executada no momento da confirmação. Nesse caso, a lógica de repetição talvez seja necessária.  
  
 Para obter mais informações, consulte a seção sobre transações entre contêineres em [níveis de isolamento da transação](../../2014/database-engine/transaction-isolation-levels.md).  
  
## <a name="implementing-retry-logic"></a>Implementando a lógica de repetição  
 Como ocorre com todas as transações que acessam tabelas com otimização de memória, é necessário considerar a lógica de repetição para controlar as falhas potenciais, como conflitos de gravação (o código de erro 41302) ou falhas de dependência (código de erro 41301). Na maioria dos aplicativos, a taxa de falhas será baixa, mas ainda será necessário controlar as falhas repetindo a transação. Duas maneiras sugeridas de implementar a lógica de repetição são:  
  
-   Repetições do lado do cliente. As tentativas do lado do cliente são a maneira preferida de implementar a lógica de repetição em casos gerais. O aplicativo cliente captura o erro gerado pela transação e repete a transação. Se um aplicativo cliente existente tiver a lógica de repetição para controlar deadlocks, você poderá estender o aplicativo para tratar os novos códigos de erro.  
  
-   Usando um procedimentos armazenado de wrapper. O cliente chama um procedimento armazenado [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado que chama o procedimento armazenado originalmente criado ou executa a transação. O procedimento de wrapper em seguida usa a lógica try/catch para capturar o erro e repetir a chamada de procedimento se for necessário. É possível que os resultados sejam retornados para o cliente antes da falha, e o cliente não saberia como rejeitá-los. Portanto, para ter segurança, é melhor usar esse método apenas com procedimentos armazenados compilados de modo nativo que não retornam nenhum conjunto de resultados para o cliente.  
  
 A lógica de repetição pode ser implementada no [!INCLUDE[tsql](../includes/tsql-md.md)] ou no código de aplicativo da camada intermediária.  
  
 Dois motivos possíveis para considerar a lógica de repetição:  
  
-   O aplicativo cliente tem uma lógica de repetição para outros códigos de erro, como 1205, que você pode estender.  
  
-   Os conflitos são raros, e é importante reduzir a latência completa usando a execução preparada. Para obter mais informações sobre como executar nativamente compilados diretamente a procedimentos armazenados, consulte [procedimentos armazenados compilados nativamente](../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
 O exemplo a seguir mostra uma lógica de repetição em um procedimento armazenado interpretado [!INCLUDE[tsql](../includes/tsql-md.md)], que contém uma chamada para um procedimento armazenado compilado nativamente ou para uma transação entre contêineres.  
  
```tsql  
CREATE PROCEDURE usp_my_procedure @param1 type1, @param2 type2, ...  
AS  
BEGIN  
  -- number of retries – tune based on the workload  
  DECLARE @retry INT = 10  
  
  WHILE (@retry > 0)  
  BEGIN  
    BEGIN TRY  
  
      -- exec usp_my_native_proc @param1, @param2, ...  
  
      --       or  
  
      -- BEGIN TRANSACTION  
      --   …  
      -- COMMIT TRANSACTION  
  
      SET @retry = 0  
    END TRY  
    BEGIN CATCH  
      SET @retry -= 1  
  
      -- the error number for deadlocks (1205) does not need to be included for   
      -- transactions that do not access disk-based tables  
      IF (@retry > 0 AND error_number() in (41302, 41305, 41325, 41301, 1205))  
      BEGIN  
        -- these error conditions are transaction dooming - rollback the transaction  
        -- this is not needed if the transaction spans a single native proc execution  
        --   as the native proc will simply rollback when an error is thrown   
        IF XACT_STATE() = -1  
          ROLLBACK TRANSACTION  
  
        -- use a delay if there is a high rate of write conflicts (41302)  
        --   length of delay should depend on the typical duration of conflicting transactions  
        -- WAITFOR DELAY '00:00:00.001'  
      END  
      ELSE  
      BEGIN  
        -- insert custom error handling for other error conditions here  
  
        -- throw if this is not a qualifying error condition  
        ;THROW  
      END  
    END CATCH  
  END  
END  
```  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre transações em tabelas com otimização de memória](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [Transações em tabelas com otimização de memória](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [Diretrizes para níveis de isolamento da transação com tabelas com otimização de memória](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)  
  
  
