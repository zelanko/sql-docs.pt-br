---
title: sp_send_dbmail (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sendmail_sp_TSQL
- sendmail_sp
- SP_SEND_DBMAIL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_send_dbmail
ms.assetid: f1d7a795-a3fd-4043-ac4b-c781e76dab47
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42c763b37f5c721a259fbe87eca804e22f5c27b5
ms.sourcegitcommit: f6bfe4a0647ce7efebaca11d95412d6a9a92cd98
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2019
ms.locfileid: "71974372"
---
# <a name="sp_send_dbmail-transact-sql"></a>sp_send_dbmail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Envia uma mensagem de email aos destinatários especificados. A mensagem pode incluir um conjunto de resultados da consulta, anexos de arquivo ou ambos. Quando o email é colocado com êxito na fila de Database Mail, **sp_send_dbmail** retorna o **mailitem_id** da mensagem. Esse procedimento armazenado está no banco de dados **msdb** .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_send_dbmail [ [ @profile_name = ] 'profile_name' ]  
    [ , [ @recipients = ] 'recipients [ ; ...n ]' ]  
    [ , [ @copy_recipients = ] 'copy_recipient [ ; ...n ]' ]  
    [ , [ @blind_copy_recipients = ] 'blind_copy_recipient [ ; ...n ]' ]  
    [ , [ @from_address = ] 'from_address' ]  
    [ , [ @reply_to = ] 'reply_to' ]   
    [ , [ @subject = ] 'subject' ]   
    [ , [ @body = ] 'body' ]   
    [ , [ @body_format = ] 'body_format' ]  
    [ , [ @importance = ] 'importance' ]  
    [ , [ @sensitivity = ] 'sensitivity' ]  
    [ , [ @file_attachments = ] 'attachment [ ; ...n ]' ]  
    [ , [ @query = ] 'query' ]  
    [ , [ @execute_query_database = ] 'execute_query_database' ]  
    [ , [ @attach_query_result_as_file = ] attach_query_result_as_file ]  
    [ , [ @query_attachment_filename = ] query_attachment_filename ]  
    [ , [ @query_result_header = ] query_result_header ]  
    [ , [ @query_result_width = ] query_result_width ]  
    [ , [ @query_result_separator = ] 'query_result_separator' ]  
    [ , [ @exclude_query_output = ] exclude_query_output ]  
    [ , [ @append_query_error = ] append_query_error ]  
    [ , [ @query_no_truncate = ] query_no_truncate ]   
    [ , [ @query_result_no_padding = ] @query_result_no_padding ]   
    [ , [ @mailitem_id = ] mailitem_id ] [ OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_name = ] 'profile_name'` é o nome do perfil do qual enviar a mensagem. O *profile_name* é do tipo **sysname**, com um padrão de NULL. O *profile_name* deve ser o nome de um perfil de Database Mail existente. Quando nenhum *profile_name* é especificado, o **sp_send_dbmail** usa o perfil privado padrão para o usuário atual. Se o usuário não tiver um perfil privado padrão, o **sp_send_dbmail** usará o perfil público padrão para o banco de dados **msdb** . Se o usuário não tiver um perfil privado padrão e não houver um perfil público padrão para o banco de dados, **\@profile_name** deverá ser especificado.  
  
`[ @recipients = ] 'recipients'` é uma lista delimitada por ponto-e-vírgula de endereços de email para os quais enviar a mensagem. A lista de destinatários é do tipo **varchar (max)** . Embora esse parâmetro seja opcional, pelo menos um de **\@recipients**, **\@copy_recipients**ou **\@blind_copy_recipients** deve ser especificado ou **sp_send_dbmail** retorna um erro.  
  
`[ @copy_recipients = ] 'copy_recipients'` é uma lista delimitada por ponto-e-vírgula de endereços de email para copiar a mensagem. A lista de cópias de destinatários é do tipo **varchar (max)** . Embora esse parâmetro seja opcional, pelo menos um de **\@recipients**, **\@copy_recipients**ou **\@blind_copy_recipients** deve ser especificado ou **sp_send_dbmail** retorna um erro.  
  
`[ @blind_copy_recipients = ] 'blind_copy_recipients'` é uma lista delimitada por ponto-e-vírgula de endereços de email para copiar a mensagem na cópia oculta. A lista de destinatários de cópia oculta é do tipo **varchar (max)** . Embora esse parâmetro seja opcional, pelo menos um de **\@recipients**, **\@copy_recipients**ou **\@blind_copy_recipients** deve ser especificado ou **sp_send_dbmail** retorna um erro.  
  
`[ @from_address = ] 'from_address'` é o valor do ' endereço remetente ' da mensagem de email. Esse é um parâmetro opcional usado para substituir as configurações no perfil de email. Esse parâmetro é do tipo **varchar (max)** . As configurações de segurança de SMTP determinarão se essas substituições serão aceitas. Se nenhum parâmetro for especificado, o padrão será NULL.  
  
`[ @reply_to = ] 'reply_to'` é o valor do ' responder para endereço ' da mensagem de email. Aceita apenas um endereço de email como um valor válido. Esse é um parâmetro opcional usado para substituir as configurações no perfil de email. Esse parâmetro é do tipo **varchar (max)** . As configurações de segurança de SMTP determinarão se essas substituições serão aceitas. Se nenhum parâmetro for especificado, o padrão será NULL.  
  
`[ @subject = ] 'subject'` é o assunto da mensagem de email. O assunto é do tipo **nvarchar (255)** . Se nenhum assunto for especificado, o padrão será 'SQL Server Message'.  
  
`[ @body = ] 'body'` é o corpo da mensagem de email. O corpo da mensagem é do tipo **nvarchar (max)** , com um padrão de NULL.  
  
`[ @body_format = ] 'body_format'` é o formato do corpo da mensagem. O parâmetro é do tipo **varchar (20)** , com um padrão de NULL. Quando especificado, os cabeçalhos da mensagem de saída são definidos para indicar que o corpo da mensagem tem o formato especificado. O parâmetro pode conter um dos seguintes valores:  
  
-   TEXT  
  
-   HTML  
  
 Assume TEXT como padrão.  
  
`[ @importance = ] 'importance'` é a importância da mensagem. O parâmetro é do tipo **varchar (6)** . O parâmetro pode conter um dos seguintes valores:  
  
-   Baixa  
  
-   Normal  
  
-   Alto  
  
 Assume Normal como padrão.  
  
`[ @sensitivity = ] 'sensitivity'` é a sensibilidade da mensagem. O parâmetro é do tipo **varchar (12)** . O parâmetro pode conter um dos seguintes valores:  
  
-   Normal  
  
-   Personal  
  
-   Private  
  
-   Confidential  
  
 Assume Normal como padrão.  
  
`[ @file_attachments = ] 'file_attachments'` é uma lista delimitada por ponto-e-vírgula de nomes de arquivo a serem anexados à mensagem de email. Os arquivos da lista devem ser especificados como caminhos absolutos. A lista de anexos é do tipo **nvarchar (max)** . Por padrão, o Database Mail limita os anexos de arquivo a 1 MB por arquivo.  
 
 > [!IMPORTANT]
 > Esse parâmetro não está disponível no Azure SQL Instância Gerenciada porque ele não pode acessar o sistema de arquivos local.
  
`[ @query = ] 'query'` é uma consulta a ser executada. Os resultados da consulta podem ser anexados a um arquivo ou incluídos no corpo da mensagem de email. A consulta é do tipo **nvarchar (max)** e pode conter qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] válida. Observe que a consulta é executada em uma sessão separada, portanto, as variáveis locais no script que chamam **sp_send_dbmail** não estão disponíveis para a consulta.  
  
`[ @execute_query_database = ] 'execute_query_database'` é o contexto de banco de dados no qual o procedimento armazenado executa a consulta. O parâmetro é do tipo **sysname**, com um padrão do banco de dados atual. Esse parâmetro só será aplicável se **\@query** for especificado.  
  
`[ @attach_query_result_as_file = ] attach_query_result_as_file` especifica se o conjunto de resultados da consulta é retornado como um arquivo anexado. *attach_query_result_as_file* é do tipo **bit**, com um padrão de 0.  
  
 Quando o valor for 0, os resultados da consulta serão incluídos no corpo da mensagem de email, após o conteúdo do parâmetro **\@Body** . Quando o valor é 1, os resultados são retornados como um anexo. Esse parâmetro só será aplicável se **\@query** for especificado.  
  
`[ @query_attachment_filename = ] query_attachment_filename` especifica o nome do arquivo a ser usado para o conjunto de resultados do anexo da consulta. *query_attachment_filename* é do tipo **nvarchar (255)** , com um padrão de NULL. Esse parâmetro é ignorado quando *attach_query_result* é 0. Quando *attach_query_result* é 1 e esse parâmetro é nulo, Database Mail cria um nome de arquivo arbitrário.  
  
`[ @query_result_header = ] query_result_header` especifica se os resultados da consulta incluem cabeçalhos de coluna. O valor de query_result_header é do tipo **bit**. Quando o valor é 1, os resultados da consulta contêm cabeçalhos de coluna. Quando o valor é 0, resultados da consulta não incluem cabeçalhos de coluna. O padrão desse parâmetro é **1**. Esse parâmetro só será aplicável se **\@query** for especificado.  
 
   >[!NOTE]
   > O erro a seguir pode ocorrer ao definir \@query_result_header como 0 e definir \@query_no_truncate como 1:
   > <br> MSG 22050, nível 16, estado 1, linha 12: Falha ao inicializar a biblioteca sqlcmd com o número de erro-2147024809.
  
`[ @query_result_width = ] query_result_width` é a largura da linha, em caracteres, a ser usada para formatar os resultados da consulta. O *query_result_width* é do tipo **int**, com um padrão de 256. O valor fornecido deve estar entre 10 e 32767. Esse parâmetro só será aplicável se **\@query** for especificado.  
  
`[ @query_result_separator = ] 'query_result_separator'` é o caractere usado para separar colunas na saída da consulta. O separador é do tipo **Char (1)** . Usa como padrão ' ' (espaço).  
  
`[ @exclude_query_output = ] exclude_query_output` especifica se a saída da execução da consulta deve ser retornada na mensagem de email. **exclude_query_output** é bit, com um padrão de 0. Quando esse parâmetro é 0, a execução do procedimento armazenado **sp_send_dbmail** imprime a mensagem retornada como resultado da execução da consulta no console. Quando esse parâmetro é 1, a execução do procedimento armazenado **sp_send_dbmail** não imprime nenhuma das mensagens de execução de consulta no console.  
  
`[ @append_query_error = ] append_query_error` especifica se o email deve ser enviado quando um erro retorna da consulta especificada no argumento **\@query** . **append_query_error** é **bit**, com um padrão de 0. Quando esse parâmetro é 1, o Database Mail envia a mensagem de email e inclui a mensagem de erro de consulta no corpo da mensagem de email. Quando esse parâmetro for 0, Database Mail não enviará a mensagem de email e **sp_send_dbmail** terminará com o código de retorno 1, indicando falha.  
  
`[ @query_no_truncate = ] query_no_truncate` especifica se a consulta deve ser executada com a opção que evita o truncamento de tipos de dados de comprimento de variável grande (**varchar (max)** , **nvarchar (max)** , **varbinary (max)** , **XML**, **Text**, **ntext**, **Image** e tipos de dados definidos pelo usuário). Quando definido, os resultados da consulta não incluem cabeçalhos de coluna. O valor de *query_no_truncate* é do tipo **bit**. Quando o valor é 0 ou não especificado, as colunas na consulta são truncadas com 256 caracteres. Quando o valor é 1, as colunas da consulta não são truncadas. Esse parâmetro assume 0 como padrão.  
  
> [!NOTE]  
>  Quando usado com grandes quantidades de dados, a opção \@**query_no_truncate** consome recursos adicionais e pode reduzir o desempenho do servidor.  
  
`[ @query_result_no_padding ] @query_result_no_padding` o tipo é bit. O padrão é 0. Quando você define como 1, os resultados da consulta não são preenchidos, possivelmente reduzindo o tamanho do arquivo. Se você definir \@query_result_no_padding como 1 e definir o parâmetro \@query_result_width, o parâmetro \@query_result_no_padding substituirá o parâmetro \@query_result_width.  
  
 Nesse caso, não ocorre nenhum erro.  
 
  >[!NOTE]
  > O erro a seguir pode ocorrer ao definir \@query_result_no_padding como 1 e fornecer um parâmetro para \@query_no_truncate:
  > <br> MSG 22050, nível 16, estado 1, linha 0: Falha ao executar a consulta porque as opções \@query_result_no_append e \@query_no_truncate são mutuamente exclusivas. 
  
 Se você definir o \@query_result_no_padding como 1 e definir o parâmetro \@query_no_truncate, um erro será gerado.  
  
`[ @mailitem_id = ] mailitem_id [ OUTPUT ]` o parâmetro output opcional retorna o *mailitem_id* da mensagem. O *mailitem_id* é do tipo **int**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Um código de retorno de 0 significa êxito. Qualquer outro valor significa falha. O código de erro para a instrução que falhou é armazenado na variável \@ @ no__t-1ERROR.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Com êxito, retorna a mensagem que "Email enfileirado".  
  
## <a name="remarks"></a>Comentários  
 Antes de usar, Database Mail deve ser habilitado usando o assistente de configuração do Database Mail ou **sp_configure**.  
  
 **sysmail_stop_sp** para de Database Mail interrompendo os objetos de Service Broker que o programa externo usa. **sp_send_dbmail** ainda aceita email quando Database Mail é interrompido usando **sysmail_stop_sp**. Para iniciar Database Mail, use **sysmail_start_sp**.  
  
 Quando **\@Profile** não for especificado, o **sp_send_dbmail** usará um perfil padrão. Se o usuário que envia a mensagem de email tiver um perfil particular padrão, o Database Mail irá utilizá-lo. Se o usuário não tiver um perfil particular padrão, o **sp_send_dbmail** usará o perfil público padrão. Se não houver nenhum perfil particular padrão para o usuário e nenhum perfil público padrão, **sp_send_dbmail** retornará um erro.  
  
 **sp_send_dbmail** não dá suporte a mensagens de email sem conteúdo. Para enviar uma mensagem de email, você deve especificar pelo menos um dos **\@Body**, **\@query**, **\@file_attachments**ou **\@subject**. Caso contrário, **sp_send_dbmail** retornará um erro.  
  
 O Database Mail usa o contexto de segurança do usuário atual do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para controlar o acesso a arquivos. Portanto, os usuários que são autenticados com a autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem anexar arquivos usando o **\@file_attachments**. O Windows não permite que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forneça credenciais de um computador remoto para outro. Portanto, o Database Mail pode não conseguir anexar arquivos de um compartilhamento de rede caso o comando seja executado de um computador diferente daquele em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado.  
  
 Se **\@query** e **\@file_attachments** forem especificados e o arquivo não puder ser encontrado, a consulta ainda será executada, mas o email não será enviado.  
  
 Quando uma consulta é especificada, o conjunto de resultados é formatado como texto em linha. Dados binários no resultado são enviados em formato hexadecimal.  
  
 Os parâmetros **\@recipients**, **\@copy_recipients**e **\@blind_copy_recipients** são listas delimitadas por ponto e vírgula de endereços de email. Pelo menos um desses parâmetros deve ser fornecido ou **sp_send_dbmail** retorna um erro.  
  
 Ao executar **sp_send_dbmail** sem um contexto de transação, Database Mail inicia e confirma uma transação implícita. Ao executar **sp_send_dbmail** de dentro de uma transação existente, Database Mail se baseia no usuário para confirmar ou reverter quaisquer alterações. Ele não inicia uma transação interna.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para **sp_send_dbmail** padrão para todos os membros da função de banco de dados **DatabaseMailUser** no banco de dados **msdb** . No entanto, quando o usuário que envia a mensagem não tem permissão para usar o perfil da solicitação, **sp_send_dbmail** retorna um erro e não envia a mensagem.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-sending-an-e-mail-message"></a>A. Enviando uma mensagem de email  
 Este exemplo envia uma mensagem de email para seu amigo usando o endereço de email `myfriend@Adventure-Works.com`. O assunto da mensagem é `Automated Success Message`. O corpo da mensagem contém a sentença `'The stored procedure finished successfully'`.  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @body = 'The stored procedure finished successfully.',  
    @subject = 'Automated Success Message' ;  
```  
  
### <a name="b-sending-an-e-mail-message-with-the-results-of-a-query"></a>B. Enviando uma mensagem de email com os resultados de uma consulta  
 Este exemplo envia uma mensagem de email para seu amigo usando o endereço de email `yourfriend@Adventure-Works.com`. O assunto da mensagem é `Work Order Count` e executa uma consulta que mostra o número de ordens de trabalho com uma `DueDate` menor que dois dias, após 30 de abril de 2004. O Database Mail anexa o resultado como um arquivo de texto.  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @query = 'SELECT COUNT(*) FROM AdventureWorks2012.Production.WorkOrder  
                  WHERE DueDate > ''2004-04-30''  
                  AND  DATEDIFF(dd, ''2004-04-30'', DueDate) < 2' ,  
    @subject = 'Work Order Count',  
    @attach_query_result_as_file = 1 ;  
```  
  
### <a name="c-sending-an-html-e-mail-message"></a>C. Enviando uma mensagem de email HTML  
 Este exemplo envia uma mensagem de email para seu amigo usando o endereço de email `yourfriend@Adventure-Works.com`. O assunto da mensagem é `Work Order List` e contém um documento HTML que mostra o número de ordens de trabalho com uma `DueDate` menor que dois dias, após 30 de abril de 2004. O Database Mail envia a mensagem no formato HTML.  
  
```  
DECLARE @tableHTML  NVARCHAR(MAX) ;  
  
SET @tableHTML =  
    N'<H1>Work Order Report</H1>' +  
    N'<table border="1">' +  
    N'<tr><th>Work Order ID</th><th>Product ID</th>' +  
    N'<th>Name</th><th>Order Qty</th><th>Due Date</th>' +  
    N'<th>Expected Revenue</th></tr>' +  
    CAST ( ( SELECT td = wo.WorkOrderID,       '',  
                    td = p.ProductID, '',  
                    td = p.Name, '',  
                    td = wo.OrderQty, '',  
                    td = wo.DueDate, '',  
                    td = (p.ListPrice - p.StandardCost) * wo.OrderQty  
              FROM AdventureWorks.Production.WorkOrder as wo  
              JOIN AdventureWorks.Production.Product AS p  
              ON wo.ProductID = p.ProductID  
              WHERE DueDate > '2004-04-30'  
                AND DATEDIFF(dd, '2004-04-30', DueDate) < 2   
              ORDER BY DueDate ASC,  
                       (p.ListPrice - p.StandardCost) * wo.OrderQty DESC  
              FOR XML PATH('tr'), TYPE   
    ) AS NVARCHAR(MAX) ) +  
    N'</table>' ;  
  
EXEC msdb.dbo.sp_send_dbmail @recipients='yourfriend@Adventure-Works.com',  
    @subject = 'Work Order List',  
    @body = @tableHTML,  
    @body_format = 'HTML' ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail objetos de configuração](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail procedimentos &#40;armazenados Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)  
  
  
