---
title: RAISERROR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RAISERROR
- RAISERROR_TSQL
- RAISEERROR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmessages system table
- errors [SQL Server], RAISERROR statement
- user-defined error messages [SQL Server]
- system flags
- generating errors [SQL Server]
- TRY block [SQL Server]
- recording errors
- ad hoc messages
- RAISERROR statement
- CATCH block
- messages [SQL Server], RAISERROR statement
ms.assetid: 483588bd-021b-4eae-b4ee-216268003e79
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 787a402f51fd9caf9f02c319dae0ed87455bb56d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47625884"
---
# <a name="raiserror-transact-sql"></a>RAISERROR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gera uma mensagem de erro e inicia o processamento de erros da sessão. RAISERROR pode referenciar uma mensagem de erro definida pelo usuário na exibição do catálogo sys.messages ou criar uma mensagem dinamicamente. A mensagem é retornada como uma mensagem de erro de servidor ao aplicativo de chamada ou a um bloco CATCH de uma construção TRY...CATCH. Em vez disso, os novos aplicativos devem usar [THROW](../../t-sql/language-elements/throw-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
RAISERROR ( { msg_id | msg_str | @local_variable }  
    { ,severity ,state }  
    [ ,argument [ ,...n ] ] )  
    [ WITH option [ ,...n ] ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
RAISERROR ( { msg_str | @local_variable }  
    { ,severity ,state }  
    [ ,argument [ ,...n ] ] )  
    [ WITH option [ ,...n ] ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *msg_id*  
 É um número de mensagem de erro definido pelo usuário armazenado na exibição do catálogo sys.messages usando sp_addmessage. Os números de erro para mensagens de erro definidas pelo usuário deve ser maiores que 50000. Quando *msg_id* não é especificado, RAISERROR gera uma mensagem de erro com o número de erro 50000.  
  
 *msg_str*  
 É uma mensagem definida pelo usuário com formatação semelhante à função **printf** na biblioteca padrão C. A mensagem de erro pode ter no máximo 2.047 caracteres. Se a mensagem tiver 2.048 caracteres ou mais, somente os primeiros 2.044 serão exibidos e um sinal de reticências será adicionado para indicar que a mensagem foi truncada. Observe que os parâmetros de substituição consomem mais caracteres que a saída mostra por causa de comportamento de armazenamento interno. Por exemplo, o parâmetro de substituição de *%d* com um valor atribuído 2 realmente produz um caractere na cadeia de caracteres da mensagem, mas também ocupa internamente três caracteres adicionais de armazenamento. Esse requisito de armazenamento diminui o número de caracteres disponíveis para a saída de mensagem.  
  
 Quando *msg_id* é especificado, RAISERROR gera uma mensagem de erro com o número de erro 50000.  
  
 *msg_str* é uma cadeia de caracteres com especificações de conversão inseridas opcionais. Cada especificação de conversão define como um valor na lista de argumentos é formatado e colocado em um campo no local da especificação de conversão em *msg_str*. As especificações de conversão têm este formato:  
  
 % [[*flag*] [*width*] [. *precision*] [{h | l}]] *type*  
  
 Os parâmetros que podem ser usados em *msg_str* são:  
  
 *flag*  
  
 É um código que determina o espaçamento e a justificação do valor substituído.  
  
|Código|Prefixo ou justificação|Descrição|  
|----------|-----------------------------|-----------------|  
|- (menos)|Justificado à esquerda|Justifica o valor de argumento à esquerda dentro da largura de campo especificada.|  
|+ (mais)|Prefixo de sinal|Precede o valor do argumento com um mais (+) ou menos (-) se o valor for de um tipo assinado.|  
|0 (zero)|Preenchimento de zeros|Precede a saída com zeros até que a largura mínima seja atingida. Quando 0 e o sinal de menos (-) são exibidos, 0 é ignorado.|  
|# (número)|Prefixo 0x para o tipo hexadecimal de x ou X|Quando usado com o formato o, x ou X, o sinalizador de tecla de cerquilha (#) precede qualquer valor diferente de zero com 0, 0x ou 0X, respectivamente. Quando d, i ou u são precedidos pelo sinalizador de tecla de cerquilha (#), o sinalizador é ignorado.|  
|' ' (em branco)|Preenchimento de espaço|Precede o valor de saída com espaços em branco se o valor for assinado e positivo. Isso é ignorado quando incluído com o sinalizador do sinal mais (+).|  
  
 *width*  
  
 É um inteiro que define a largura mínima para o campo no qual o valor do argumento é colocado. Se o tamanho do valor do argumento for igual ou maior que *width*, o valor será impresso sem nenhum preenchimento. Se o valor for menor que *width*, o valor será preenchido com o tamanho especificado em *width*.  
  
 Um asterisco (*) significa que a largura é especificada pelo argumento associado na lista de argumentos, que deve ser um valor inteiro.  
  
 *precisão*  
  
 É o número máximo de caracteres obtido do valor de argumento para os valores da cadeia de caracteres. Por exemplo, se uma cadeia de caracteres tiver cinco caracteres e a precisão for 3, somente os três primeiros caracteres do valor da cadeia serão usados.  
  
 Para valores inteiros, *precision* é o número mínimo de dígitos impressos.  
  
 Um asterisco (*) significa que a precisão é especificada pelo argumento associado na lista de argumentos, que deve ser um valor inteiro.  
  
 {h | l} *type*  
  
 É usado com os tipos de caracteres d, i, o, s, x, X ou u e cria valores **shortint** (h) ou **longint** (l).  
  
|Especificação de tipo|Representa|  
|------------------------|----------------|  
|d ou i|Inteiro assinado|  
|o|Octal não assinado|  
|s|Cadeia de caracteres|  
|u|Inteiro não assinado|  
|x ou X|Hexadecimal não assinado|  
  
> [!NOTE]  
>  Essas especificações de tipo são baseadas naquelas originalmente definidas para a função **printf** na biblioteca padrão C. As especificações de tipo usadas na cadeia de caracteres de mensagem RAISERROR são mapeadas para tipos de dados [!INCLUDE[tsql](../../includes/tsql-md.md)], enquanto as especificações usadas em **printf** são mapeadas para tipos de dados de linguagem C. As especificações de tipo usadas em **printf** não são compatíveis com RAISERROR quando o [!INCLUDE[tsql](../../includes/tsql-md.md)] não tem um tipo de dados semelhante ao tipo de dados C associado. Por exemplo, não há suporte para a especificação de *%p* de ponteiros em RAISERROR porque o [!INCLUDE[tsql](../../includes/tsql-md.md)] não tem um tipo de dados de ponteiro.  
  
> [!NOTE]  
>  Para converter um valor no tipo de dados **bigint** do [!INCLUDE[tsql](../../includes/tsql-md.md)], especifique **%I64d**.  
  
 *@local_variable*  
 É uma variável de qualquer tipo de dados de caractere válido que contém uma cadeia de caracteres formatada da mesma maneira que *msg_str*. *@local_variable* deve ser **char** ou **varchar** ou poder ser convertido implicitamente nesses tipos de dados.  
  
 *severity*  
 É o nível de severidade definido pelo usuário associado a essa mensagem. Ao usar *msg_id* para gerar uma mensagem definida pelo usuário criada com sp_addmessage, a severidade especificada em RAISERROR substitui a severidade especificada em sp_addmessage.  
  
 Níveis de severidade de 0 a 18 podem ser especificados por qualquer usuário. Níveis de severidade de 19 a 25 podem ser especificados apenas por membros da função de servidor fixa sysadmin ou por usuários com permissões ALTER TRACE. Para níveis de severidade de 19 a 25, a opção WITH LOG é obrigatória. Níveis de severidade menores que 0 são interpretados como 0. Níveis de severidade maiores que 25 são interpretados como 25.  
  
> [!CAUTION]  
>  Níveis de severidade de 20 a 25 são considerados fatais. Se um nível de severidade fatal for encontrado, a conexão de cliente é encerrada depois de receber a mensagem, e o erro é registrado nos logs de erro e de aplicativo.  
  
 Você pode especificar -1 para retornar o valor de severidade associado ao erro, conforme mostrado no exemplo a seguir.  
  
```  
RAISERROR (15600,-1,-1, 'mysp_CreateCustomer');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Msg 15600, Level 15, State 1, Line 1   
 An invalid parameter or option was specified for procedure 'mysp_CreateCustomer'.
 ```  
  
 *state*  
 É um número inteiro de 0 a 255. Os valores negativos usam 1 como padrão. Valores maiores que 255 não devem ser usados. 
  
 Se o mesmo erro definido pelo usuário for gerado em vários locais, o uso de um número de estado exclusivo para cada local pode ajudar a encontrar a seção de código que está gerando os erros.  
  
 *argument*  
 São os parâmetros usados na substituição de variáveis definidas em *msg_str* ou na mensagem que corresponde a *msg_id*. Pode haver 0 ou mais parâmetros de substituição, mas o número total de parâmetros de substituição não pode exceder 20. Cada parâmetro de substituição pode ser uma variável local ou um destes tipos de dados: **tinyint**, **smallint**, **int**, **char**, **varchar**, **nchar**, **nvarchar**, **binary** ou **varbinary**. Nenhum outro tipo de dados possui suporte.  
  
 *opção*  
 É uma opção personalizada para o erro e pode ser um dos valores na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|LOG|Registra o erro no log de erros e no log do aplicativo para a instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Os erros registrados no log de erros atualmente estão limitados a no máximo 440 bytes. Somente um membro da função de servidor fixa sysadmin ou um usuário com permissões ALTER TRACE pode especificar WITH LOG.<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|NOWAIT|Envia mensagens imediatamente ao cliente.<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|SETERROR|Define os valores de @@ERROR e ERROR_NUMBER como *msg_id* ou 50.000, independentemente do nível de severidade.<br /><br /> [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
  
## <a name="remarks"></a>Remarks  
 Os erros gerados por RAISERROR funcionam da mesma maneira que os erros gerados pelo código do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Os valores especificados por RAISERROR são relatados pelas funções do sistema ERROR_LINE, ERROR_MESSAGE, ERROR_NUMBER, ERROR_PROCEDURE, ERROR_SEVERITY, ERROR_STATE e @@ERROR. Quando RAISERROR é executado com uma severidade de 11 ou mais em um bloco TRY, ele transfere o controle para o bloco CATCH associado. O erro será retornado ao chamador se RAISERROR for executado:  
  
-   Fora do escopo de qualquer bloco TRY.  
  
-   Com uma severidade de 10 ou menos em um bloco TRY.  
  
-   Com uma severidade de 20 ou mais que encerra a conexão de banco de dados.  
  
 Blocos CATCH podem usar RAISERROR para lançar novamente o erro que invocou o bloco CATCH usando funções de sistema como ERROR_NUMBER e ERROR_MESSAGE a fim de recuperar as informações de erro originais. @@ERROR é definido como 0 por padrão para mensagens com uma severidade de 1 a 10.  
  
 Quando *msg_id* especifica uma mensagem definida pelo usuário disponível na exibição do catálogo sys.messages, RAISERROR processa a mensagem da coluna de texto usando as mesmas regras que são aplicadas ao texto de uma mensagem definida pelo usuário especificada usando *msg_str*. O texto da mensagem definida pelo usuário pode conter especificações de conversão, e RAISERROR mapeará valores de argumento nas especificações de conversão. Use sp_addmessage para adicionar mensagens de erro definidas pelo usuário e sp_dropmessage para excluí-las.  
  
 RAISERROR pode ser usado como uma alternativa para PRINT a fim de retornar mensagens para aplicativos de chamada. RAISERROR dá suporte à substituição de caracteres de forma semelhante à funcionalidade da função **printf** na biblioteca padrão C, ao contrário da instrução PRINT do [!INCLUDE[tsql](../../includes/tsql-md.md)]. A instrução PRINT não é afetada por blocos TRY, enquanto que a execução de RAISERROR com uma severidade de 11 a 19 em um bloco TRY e transfere o controle para o bloco CATCH associado. Especifique uma severidade de 10 ou menos para que RAISERROR retorne uma mensagem de um bloco TRY sem invocar o bloco CATCH.  
  
 Normalmente, argumentos sucessivos substituem especificações de conversão sucessivas; o primeiro argumento substitui a primeira especificação de conversão, o segundo argumento substitui a segunda especificação de conversão e assim por diante. Por exemplo, na seguinte instrução `RAISERROR`, o primeiro argumento de `N'number'` substitui a primeira especificação de conversão de `%s`; e o segundo argumento de `5` substitui a segunda especificação de conversão de `%d.`  
  
```  
RAISERROR (N'This is message %s %d.', -- Message text.  
           10, -- Severity,  
           1, -- State,  
           N'number', -- First argument.  
           5); -- Second argument.  
-- The message text returned is: This is message number 5.  
GO  
```  
  
 Se um asterisco (*) for especificado para a largura ou precisão de uma especificação de conversão, o valor a ser usado para elas é especificado como um valor de argumento inteiro. Nesse caso, uma especificação de conversão pode usar até três argumentos, um para a largura, outro para a precisão e outro para o valor de substituição.  
  
 Por exemplo, as duas instruções `RAISERROR` a seguir retornam a mesma cadeia de caracteres. Uma especifica os valores de largura e de precisão na lista de argumentos; a outra os especifica na especificação de conversão.  
  
```  
RAISERROR (N'<\<%*.*s>>', -- Message text.  
           10, -- Severity,  
           1, -- State,  
           7, -- First argument used for width.  
           3, -- Second argument used for precision.  
           N'abcde'); -- Third argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
RAISERROR (N'<\<%7.3s>>', -- Message text.  
           10, -- Severity,  
           1, -- State,  
           N'abcde'); -- First argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
```  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-error-information-from-a-catch-block"></a>A. Retornando informações de erro de um bloco CATCH  
 O exemplo de código a seguir mostra como usar o bloco `RAISERROR` dentro de um bloco `TRY` para fazer a execução saltar para o bloco `CATCH` associado. Também mostra como usar `RAISERROR` para retornar informações sobre o erro que invocou o bloco `CATCH`.  
  
> [!NOTE]  
>  RAISERROR somente gera erros com estado de 1 a 127. Como o [!INCLUDE[ssDE](../../includes/ssde-md.md)] pode gerar erros com o estado 0, recomendamos que você verifique o estado de erro retornado por ERROR_STATE antes de passá-lo como um valor ao parâmetro de estado de RAISERROR.  
  
```  
BEGIN TRY  
    -- RAISERROR with severity 11-19 will cause execution to   
    -- jump to the CATCH block.  
    RAISERROR ('Error raised in TRY block.', -- Message text.  
               16, -- Severity.  
               1 -- State.  
               );  
END TRY  
BEGIN CATCH  
    DECLARE @ErrorMessage NVARCHAR(4000);  
    DECLARE @ErrorSeverity INT;  
    DECLARE @ErrorState INT;  
  
    SELECT   
        @ErrorMessage = ERROR_MESSAGE(),  
        @ErrorSeverity = ERROR_SEVERITY(),  
        @ErrorState = ERROR_STATE();  
  
    -- Use RAISERROR inside the CATCH block to return error  
    -- information about the original error that caused  
    -- execution to jump to the CATCH block.  
    RAISERROR (@ErrorMessage, -- Message text.  
               @ErrorSeverity, -- Severity.  
               @ErrorState -- State.  
               );  
END CATCH;  
```  
  
### <a name="b-creating-an-ad-hoc-message-in-sysmessages"></a>B. Criando uma mensagem ad hoc em sys.messages  
 O exemplo a seguir mostra como gerar uma mensagem armazenada na exibição do catálogo sys.messages. A mensagem foi adicionada à exibição do catálogo sys.messages usando o procedimento armazenado do sistema `sp_addmessage` como o número de mensagem `50005`.  
  
```  
sp_addmessage @msgnum = 50005,  
              @severity = 10,  
              @msgtext = N'<\<%7.3s>>';  
GO  
RAISERROR (50005, -- Message id.  
           10, -- Severity,  
           1, -- State,  
           N'abcde'); -- First argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
sp_dropmessage @msgnum = 50005;  
GO  
```  
  
### <a name="c-using-a-local-variable-to-supply-the-message-text"></a>C. Usando uma variável local para fornecer o texto da mensagem  
 O exemplo de código a seguir mostra como usar uma variável local para fornecer o texto da mensagem a uma instrução `RAISERROR`.  
  
```  
DECLARE @StringVariable NVARCHAR(50);  
SET @StringVariable = N'<\<%7.3s>>';  
  
RAISERROR (@StringVariable, -- Message text.  
           10, -- Severity,  
           1, -- State,  
           N'abcde'); -- First argument supplies the string.  
-- The message text returned is: <<    abc>>.  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [PRINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [xp_logevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logevent-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  

