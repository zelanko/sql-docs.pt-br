---
title: sp_trace_create (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_create_TSQL
- sp_trace_create
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_create
ms.assetid: f3a43597-4c5a-4520-bcab-becdbbf81d2e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7d698932bb7ef7e0fd37a0ced8ab536eeb0d5d68
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096028"
---
# <a name="sp_trace_create-transact-sql"></a>sp_trace_create (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria uma definição de rastreamento. O rastreamento novo estará em um estado interrompido.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use Eventos Estendidos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_trace_create [ @traceid = ] trace_id OUTPUT   
          , [ @options = ] option_value   
          , [ @tracefile = ] 'trace_file'   
     [ , [ @maxfilesize = ] max_file_size ]  
     [ , [ @stoptime = ] 'stop_time' ]  
     [ , [ @filecount = ] 'max_rollover_files' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @traceid = ] trace_id`É o número atribuído pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao novo rastreamento. Qualquer entrada fornecida pelo usuário será ignorada. *trace_id* é **int**, com um padrão de NULL. O usuário emprega o valor *trace_id* para identificar, modificar e controlar o rastreamento definido por esse procedimento armazenado.  
  
`[ @options = ] option_value`Especifica as opções definidas para o rastreamento. *option_value* é **int**, sem padrão. Os usuários podem escolher uma combinação destas opções especificando o valor de soma das opções escolhidas. Por exemplo, para ativar as opções TRACE_FILE_ROLLOVER e SHUTDOWN_ON_ERROR, especifique **6** para *option_value*.  
  
 A tabela a seguir lista as opções, as descrições e seus valores.  
  
|Nome da opção|Valor de opção|DESCRIÇÃO|  
|-----------------|------------------|-----------------|  
|TRACE_FILE_ROLLOVER|**2**|Especifica que quando o *max_file_size* é atingido, o arquivo de rastreamento atual é fechado e um novo arquivo é criado. Todos os novos registros serão gravados no novo arquivo. O novo arquivo terá o mesmo nome do anterior, mas um número inteiro será adicionado para indicar a sequência. Por exemplo, se o arquivo de rastreamento original for filename.trc, o próximo arquivo de rastreamento será filename_1.trc, o seguinte será filename_2.trc, e assim por diante.<br /><br /> Quanto mais arquivos de rastreamento de substituição forem criados, o valor do inteiro adicionado ao nome de arquivo aumentará consecutivamente.<br /><br /> SQL Server usa o valor padrão de *max_file_size* (5 MB) se essa opção for especificada sem especificar um valor para *max_file_size*.|  
|SHUTDOWN_ON_ERROR|**quatro**|Especifica que, se o rastreamento não puder ser gravado no arquivo por qualquer motivo, o SQL Server será encerrado. Esta opção é útil ao executar rastreamentos de auditoria de segurança.|  
|TRACE_PRODUCE_BLACKBOX|**8**|Especifica que um registro dos últimos 5 MB de informações de rastreamento produzidas pelo servidor será salvo pelo servidor. TRACE_PRODUCE_BLACKBOX é incompatível com todas as outras opções.|  
  
`[ @tracefile = ] 'trace_file'`Especifica o local e o nome do arquivo para o qual o rastreamento será gravado. *trace_file* é **nvarchar (245)** sem padrão. o *trace_file* pode ser um diretório local (como N ' C:\MSSQL\Trace\trace.trc ') ou um UNC para um compartilhamento ou caminho (n '\\\\*nomedoservidor*\\*ShareName*\\*Directory*\trace.trc ').  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]acrescentará uma extensão **. trc** a todos os nomes de arquivo de rastreamento. Se a opção TRACE_FILE_ROLLOVER e uma *max_file_size* forem especificadas, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o criará um novo arquivo de rastreamento quando o arquivo de rastreamento original aumentar para seu tamanho máximo. O novo arquivo tem o mesmo nome que o arquivo original, mas _*n* é acrescentado para indicar sua sequência, começando com **1**. Por exemplo, se o primeiro arquivo de rastreamento for denominado **filename. trc**, o segundo arquivo de rastreamento será chamado de **filename_1. trc**.  
  
 Se você usa a opção TRACE_FILE_ROLLOVER, é recomendável que não use caracteres de sublinhado no nome de arquivo de rastreamento original. Se você usar sublinhados, ocorrerá o seguinte comportamento:  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]o não carrega automaticamente ou solicita que você carregue os arquivos de substituição (se uma dessas opções de substituição de arquivo estiver configurada).  
  
-   A função fn_trace_gettable não carrega arquivos de substituição (quando especificado usando o argumento *number_files* ) em que o nome do arquivo original termina com um sublinhado e um valor numérico. (Isso não se aplica ao sublinhado e ao número que são acrescentados automaticamente quando um arquivo é substituído.)  
  
> [!NOTE]  
>  Como alternativa para ambos os comportamentos, você pode renomear os arquivos de rastreamento para remover os sublinhados no nome de arquivo original. Por exemplo, se o arquivo original for denominado **my_trace. trc**e o arquivo de substituição for nomeado **my_trace_1. trc**, você poderá renomear os arquivos para **mytrace. trc** e **mytrace_1. trc** antes de abrir os [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]arquivos no.  
  
 Não é possível especificar *trace_file* quando a opção TRACE_PRODUCE_BLACKBOX é usada.  
  
`[ @maxfilesize = ] max_file_size`Especifica o tamanho máximo em megabytes (MB) que um arquivo de rastreamento pode aumentar. *max_file_size* é **bigint**, com um valor padrão de **5**.  
  
 Se esse parâmetro for especificado sem a opção TRACE_FILE_ROLLOVER, o rastreamento interromperá a gravação no arquivo quando o espaço em disco usado exceder o valor especificado por *max_file_size*.  
  
`[ @stoptime = ] 'stop_time'`Especifica a data e a hora em que o rastreamento será interrompido. *stop_time* é **DateTime**, com um padrão de NULL. Se for NULL, o rastreamento será executado até que seja parado manualmente ou até que o servidor seja encerrado.  
  
 Se *stop_time* e *max_file_size* forem especificados e TRACE_FILE_ROLLOVER não for especificado, o rastreamento será alcançado quando a hora de parada especificada ou o tamanho máximo do arquivo for atingido. Se *stop_time*, *max_file_size*e TRACE_FILE_ROLLOVER forem especificados, o rastreamento parará na hora de parada especificada, supondo que o rastreamento não preencha a unidade.  
  
`[ @filecount = ] 'max_rollover_files'`Especifica o número máximo ou os arquivos de rastreamento a serem mantidos com o mesmo nome de arquivo base. *MAX_ROLLOVER_FILES* é **int**, maior que um. Este parâmetro só será válido se a opção TRACE_FILE_ROLLOVER for especificada. Quando *MAX_ROLLOVER_FILES* for especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tentará manter não mais do que *MAX_ROLLOVER_FILES* arquivos de rastreamento excluindo o arquivo de rastreamento mais antigo antes de abrir um novo arquivo de rastreamento. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rastreia a idade dos arquivos de rastreamento adicionando um número ao nome de arquivo base.  
  
 Por exemplo, quando o parâmetro *trace_file* é especificado como "c:\mytrace", um arquivo com o nome "c:\ mytrace_123. trc" é mais antigo que um arquivo com o nome "c:\ mytrace_124. trc". Se *MAX_ROLLOVER_FILES* for definido como 2, SQL Server excluirá o arquivo "c:\ mytrace_123. trc" antes de criar o arquivo de rastreamento "c:\ mytrace_125. trc".  
  
 Observe que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta excluir cada arquivo somente uma vez e não pode excluir um arquivo que está sendo usado por outro processo. Portanto, se outro aplicativo estiver trabalhando com arquivos de rastreamento enquanto o rastreamento está em execução, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá deixar esses arquivos de rastreamento no sistema de arquivos.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 A tabela a seguir descreve os valores de código que os usuários podem obter após a conclusão do procedimento armazenado.  
  
|Código de retorno|DESCRIÇÃO|  
|-----------------|-----------------|  
|0|Nenhum erro.|  
|1|Erro desconhecido.|  
|10|Opções inválidas. Retornado quando as opções especificadas são incompatíveis.|  
|12|Arquivo não criado.|  
|13|Memória insuficiente. Retornado quando não há memória suficiente para executar a ação especificada.|  
|14|Horário de parada inválido. Retornado quando o horário de parada especificado já aconteceu.|  
|15|Parâmetros inválidos. Retornado quando o usuário forneceu parâmetros incompatíveis.|  
  
## <a name="remarks"></a>Comentários  
 **sp_trace_create** é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimento armazenado que executa muitas das ações executadas anteriormente por **xp_trace_\* ** procedimentos armazenados estendidos disponíveis em versões anteriores do SQL Server. Use **sp_trace_create** em vez de:  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_setqueuecreateinfo**  
  
-   **xp_trace_setqueuedestination**  
  
 **sp_trace_create** cria apenas uma definição de rastreamento. Este procedimento armazenado não pode ser usado para iniciar ou alterar um rastreamento.  
  
 Parâmetros de todos os procedimentos armazenados de rastreamento do SQL (**sp_trace_xx**) são estritamente tipados. Se esses parâmetros não forem chamados com os tipos de dados com parâmetro de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
 Por **sp_trace_create**, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço deve ter permissão de gravação na pasta de arquivos de rastreamento. Se a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não for um administrador no computador onde o arquivo de rastreamento está localizado, você deve conceder explicitamente a permissão de gravação para a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Você pode carregar automaticamente o arquivo de rastreamento criado com **sp_trace_create** em uma tabela usando a função de sistema **fn_trace_gettable** . Para obter informações sobre como usar essa função do sistema, consulte [Sys. fn_trace_gettable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md).  
  
 Para obter um exemplo de como usar procedimentos armazenados de rastreamento, veja [Criar um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
 **TRACE_PRODUCE_BLACKBOX** tem as seguintes características:  
  
-   É um rastreamento de substituição. O *file_count* padrão é 2, mas pode ser substituído pelo usuário usando a opção *FileCount* .  
  
-   O *file_size* padrão como com outros rastreamentos é de 5 MB e pode ser alterado.  
  
-   Nenhum nome de arquivo pode ser especificado. O arquivo será salvo como: **N '%SQLDIR%\MSSQL\DATA\blackbox.trc '**  
  
-   Apenas os eventos a seguir e suas colunas são contidas no rastreamento:  
  
    -   **RPC starting**  
  
    -   **Batch starting**  
  
    -   **Exceção**  
  
    -   **Segura**  
  
-   Eventos ou colunas não podem ser adicionados ou removidos desse rastreamento.  
  
-   Não é possível especificar filtros para este rastreamento.  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão ALTER TRACE.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_trace_generateevent](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Rastreamento do SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
