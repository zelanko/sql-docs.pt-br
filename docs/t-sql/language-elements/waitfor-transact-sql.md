---
title: WAITFOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WAITFOR
- WAITFOR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TIME option
- delaying executions [SQL Server]
- batches [SQL Server], execution times
- stored procedures [SQL Server], executing
- DELAY
- time [SQL Server], execution delays
- blocking executions
- transactions [SQL Server], execution times
- WAITFOR statement
- timing executions
ms.assetid: 8e896e73-af27-4cae-a725-7a156733f3bd
author: rothja
ms.author: jroth
ms.openlocfilehash: d3b8ca20f5304dae35a54357b79c763831ceb280
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731360"
---
# <a name="waitfor-transact-sql"></a>WAITFOR (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Bloqueia a execução de um lote, procedimento armazenado ou transação até que uma hora ou intervalo de tempo especificado transcorra ou que uma instrução especificada modifique ou retorne pelo menos uma linha.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
WAITFOR   
{  
    DELAY 'time_to_pass'   
  | TIME 'time_to_execute'   
  | [ ( receive_statement ) | ( get_conversation_group_statement ) ]   
    [ , TIMEOUT timeout ]  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 DELAY  
 É o período de tempo especificado que deve decorrer, até no máximo 24 horas, antes que a execução de um lote, procedimento armazenado ou transação prossiga.  
  
 '*time_to_pass*'  
 É o período de tempo a ser aguardado. *time_to_pass* pode ser especificado em um formato de dados **datetime** ou como uma variável local. Não é possível especificar datas, portanto, a parte de data do valor de **datetime** não é permitida. *time_to_pass* é formatado como hh:mm[[:ss].mss].
  
 TIME  
 É a hora especificada em que o lote, o procedimento armazenado ou a transação é executada.  
  
 '*time_to_execute*'  
 É a hora na qual a instrução WAITFOR é concluída. *time_to_execute* pode ser especificado em um formato de dados **datetime** ou pode ser especificado como uma variável local. Não é possível especificar datas, portanto, a parte de data do valor de **datetime** não é permitida. *time_to_execute* é formatado como hh:mm[[:ss].mss] e, opcionalmente, pode incluir a data de 1900-01-01.
  
 *receive_statement*  
 É uma instrução RECEIVE válida.  
  
> [!IMPORTANT]  
>  WAITFOR com uma *receive_statement* é aplicável somente a mensagens [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Para obter mais informações, confira [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md).  
  
 *get_conversation_group_statement*  
 É uma instrução GET CONVERSATION GROUP válida.  
  
> [!IMPORTANT]  
>  WAITFOR com uma *get_conversation_group_statement* é aplicável somente a mensagens [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Para obter mais informações, confira [GET CONVERSATION GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md).  
  
 TIMEOUT *timeout*  
 Especifica o período de hora, em milissegundos, a esperar pela chegada de uma mensagem na fila.  
  
> [!IMPORTANT]  
>  A especificação de WAITFOR com TIMEOUT só é aplicável a mensagens do [!INCLUDE[ssSB](../../includes/sssb-md.md)]. Para obter mais informações, confira [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md) e [GET CONVERSATION GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 Ao executar a instrução WAITFOR, a transação está em execução e nenhuma outra solicitação pode executar sob a mesma transação.  
  
 O atraso de tempo real pode variar entre o horário especificado em *time_to_pass*, *time_to_execute* ou *timeout* e depende do nível de atividade do servidor. O contador de tempo inicia quando o thread da instrução WAITFOR é agendado. Se o servidor estiver ocupado, o thread pode não ser agendado imediatamente, portanto, o atraso de tempo pode ser maior que o tempo especificado.  
  
 WAITFOR não altera as semânticas de uma consulta. Se uma consulta não puder retornar nenhuma linha, WAITFOR esperará para sempre ou até que TIMEOUT seja alcançado, se for especificado.  
  
 Não é possível abrir cursores em instruções WAITFOR.  
  
 Não é possível definir exibições em instruções WAITFOR.  
  
 Quando a consulta exceder a opção query wait, o argumento da instrução WAITFOR poderá ser concluído sem executar. Para obter mais informações sobre a opção de configuração, confira [Configurar a opção de configuração de servidor query wait](../../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md). Para consultar os processos ativos e em espera, use [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md).  
  
 Cada instrução WAITFOR tem um thread associado a ela. Se forem especificadas muitas instruções WAITFOR no mesmo servidor, muitos threads poderão ser parados aguardando pela execução dessas instruções. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] monitora o número de threads das instruções WAITFOR e seleciona aleatoriamente alguns desses threads para sair se o servidor começar a sofrer privação de thread.  
  
 Você poderá criar um deadlock executando uma consulta com WAITFOR em uma transação que também contenha bloqueios impedindo alterações no conjunto de linhas acessado pela instrução WAITFOR. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identifica esses cenários e retorna um conjunto de resultados vazio, no caso de esse deadlock existir.  
  
> [!CAUTION]  
>  A inclusão de WAITFOR tornará mais lenta a conclusão do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e pode resultar em uma mensagem de tempo limite no aplicativo. Se necessário, ajuste a configuração de tempo limite para a conexão em nível de aplicativo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-waitfor-time"></a>a. Usando WAITFOR TIME  
 O exemplo a seguir executa o procedimento armazenado `sp_update_job` no banco de dados msdb às 22:20. (`22:20`).  
  
```  
EXECUTE sp_add_job @job_name = 'TestJob';  
BEGIN  
    WAITFOR TIME '22:20';  
    EXECUTE sp_update_job @job_name = 'TestJob',  
        @new_name = 'UpdatedJob';  
END;  
GO  
```  
  
### <a name="b-using-waitfor-delay"></a>B. Usando WAITFOR DELAY  
 O exemplo a seguir executa o procedimento armazenado depois de um atraso de duas horas.  
  
```  
BEGIN  
    WAITFOR DELAY '02:00';  
    EXECUTE sp_helpdb;  
END;  
GO  
```  
  
### <a name="c-using-waitfor-delay-with-a-local-variable"></a>C. Usando WAITFOR DELAY com uma variável local  
 O exemplo a seguir mostra como uma variável local pode ser usada com a opção `WAITFOR DELAY`. Esse procedimento armazenado aguarda por um período de tempo variável e retorna informações ao usuário, tais como o número de horas, minutos e segundos decorridos.  
  
```  
IF OBJECT_ID('dbo.TimeDelay_hh_mm_ss','P') IS NOT NULL  
    DROP PROCEDURE dbo.TimeDelay_hh_mm_ss;  
GO  
CREATE PROCEDURE dbo.TimeDelay_hh_mm_ss   
    (  
    @DelayLength char(8)= '00:00:00'  
    )  
AS  
DECLARE @ReturnInfo varchar(255)  
IF ISDATE('2000-01-01 ' + @DelayLength + '.000') = 0  
    BEGIN  
        SELECT @ReturnInfo = 'Invalid time ' + @DelayLength   
        + ',hh:mm:ss, submitted.';  
        -- This PRINT statement is for testing, not use in production.  
        PRINT @ReturnInfo   
        RETURN(1)  
    END  
BEGIN  
    WAITFOR DELAY @DelayLength  
    SELECT @ReturnInfo = 'A total time of ' + @DelayLength + ',   
        hh:mm:ss, has elapsed! Your time is up.'  
    -- This PRINT statement is for testing, not use in production.  
    PRINT @ReturnInfo;  
END;  
GO  
/* This statement executes the dbo.TimeDelay_hh_mm_ss procedure. */  
EXEC TimeDelay_hh_mm_ss '00:00:10';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `A total time of 00:00:10, in hh:mm:ss, has elapsed. Your time is up.`  
  
## <a name="see-also"></a>Consulte Também  
 [Linguagem de controle de fluxo &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
