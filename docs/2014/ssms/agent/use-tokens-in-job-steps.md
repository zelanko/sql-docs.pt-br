---
title: Usar tokens em etapas de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server Agent]
- security [SQL Server Agent], enabling alert job step tokens
- SQL Server Agent jobs, job steps
- tokens [SQL Server]
- escape macros [SQL Server Agent]
ms.assetid: 105bbb66-0ade-4b46-b8e4-f849e5fc4d43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2036dd0624e8c2c6479c8ba039aa5646f374902d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211319"
---
# <a name="use-tokens-in-job-steps"></a>Usar tokens em etapas de trabalho
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent permite usar tokens em scripts de etapas de trabalho [!INCLUDE[tsql](../../includes/tsql-md.md)] . O uso de tokens para escrever suas etapas de trabalho oferece a mesma flexibilidade fornecida por variáveis ao escrever programas de software. Quando você insere um token em um script de etapa de trabalho, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent o substitui em tempo de execução, antes de o trabalho ser executado pelo subsistema [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
> [!IMPORTANT]  
>  A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1, a sintaxe de token de etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mudou. Por consequência, uma macro de fuga agora deve acompanhar todos os tokens utilizados em etapas de trabalho ou elas falharão. O uso de macros de escape e a atualização das etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que utilizam tokens são descritos nas seções "Compreendendo o uso de tokens", "Tokens e macros do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent" e "Atualizando etapas de trabalho para usar macros" a seguir. Além disso, a sintaxe do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] , que usava colchetes para chamar tokens de etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (por exemplo, "`[DATE]`"), também mudou. Agora, deve-se colocar os nomes de token entre parênteses e um sinal de cifrão (`$`) no início da sintaxe do token. Por exemplo:  
>   
>  `$(ESCAPE_` *nome da macro* `(DATE))`  
  
## <a name="understanding-using-tokens"></a>Noções básicas sobre o uso de tokens  
  
> [!IMPORTANT]  
>  Qualquer usuário Windows com permissões de gravação no Log de Eventos do Windows pode acessar etapas de trabalho ativadas pelos alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent ou alertas do WMI. Para evitar riscos de segurança, os tokens do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que podem ser usados em trabalhos ativados por alertas encontram-se desabilitados por padrão. Esses tokens são: **a-DBN**, **a-SVR**, **a-Err**, **a-Sev**, **a-msg**. e **WMI (*`property`*)**. Observe que nesta versão, o uso de tokens foi estendido a todos os alertas.  
>   
>  Se tiver que usar esses tokens, garanta, primeiro, que apenas membros dos grupos de segurança confiáveis do Windows, como o grupo Administradores, tenham permissões de gravação no Log de Eventos do computador em que reside o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Depois, clique com o botão direito do mouse em **SQL Server Agent** no Pesquisador de Objetos, selecione **Propriedades**e, na página **Sistema de Alerta** , selecione **Substituir tokens de todas as respostas de trabalho aos alertas** para habilitar esses tokens.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A substituição de tokens do Agent é simples e eficiente: o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent substitui o token por um valor de cadeia de caracteres literal. Todos os tokens diferenciam maiúsculas de minúsculas. Suas etapas de trabalho devem levar isto em conta e usar aspas corretamente nos tokens utilizados ou converter a cadeia de caracteres de substituição pelo tipo de dados correto.  
  
 Por exemplo, você pode usar a seguinte instrução para imprimir o nome do banco de dados em uma etapa de trabalho:  
  
 `PRINT N'Current database name is $(ESCAPE_SQUOTE(A-DBN))' ;`  
  
 Neste exemplo, a macro **ESCAPE_SQUOTE** é inserida com o token **A-DBN** . Em tempo de execução, o token **A-DBN** será substituído pelo nome de banco de dados apropriado. A macro de fuga ignora eventuais aspas simples que possam ser transmitidas inadvertidamente na cadeia de caracteres de substituição do token. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent substituirá uma aspa simples por duas aspas simples na cadeia de caracteres final.  
  
 Por exemplo, se a cadeia de caracteres transmitida para substituição do token for `AdventureWorks2012'SELECT @@VERSION --`, o comando executado pela etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent será:  
  
 `PRINT N'Current database name is AdventureWorks2012''SELECT @@VERSION --' ;`  
  
 Neste caso, a instrução inserida `SELECT @@VERSION`não é executada. Em vez disso, a aspa simples adicional faz com que o servidor analise a instrução inserida como uma cadeia de caracteres. Se a cadeia de caracteres de substituição do token não contiver uma aspa simples, nenhum caractere será ignorado e a etapa de trabalho que contém o token será executada conforme se pretende.  
  
 Para depurar o uso de tokens em suas etapas de trabalho, use instruções de impressão, como `PRINT N'$(ESCAPE_SQUOTE(SQLDIR))'` , e salve a saída das etapas de trabalho em um arquivo ou tabela. Use a página **Avançado** da caixa de diálogo **Propriedades da Etapa de Trabalho** para especificar um arquivo ou tabela de saída da etapa de trabalho.  
  
## <a name="sql-server-agent-tokens-and-macros"></a>Tokens e macros do SQL Server Agent  
 As tabelas a seguir listam e descrevem os tokens e macros para os quais há suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
### <a name="sql-server-agent-tokens"></a>Tokens do SQL Server Agent  
  
|Token|Descrição|  
|-----------|-----------------|  
|**(A-DBN)**|nome do banco de dados. Se o trabalho é executado por um alerta, o valor de nome de banco de dados substitui este token automaticamente na etapa de trabalho.|  
|**(A-SVR)**|Nome de servidor. Se o trabalho é executado por um alerta, o valor de nome de servidor substitui este token automaticamente na etapa de trabalho.|  
|**(A-ERR)**|Número de erro. Se o trabalho é executado por um alerta, o valor de número de erro substitui este token automaticamente na etapa de trabalho.|  
|**(A-SEV)**|Severidade do erro. Se o trabalho é executado por um alerta, o valor de severidade do erro substitui este token automaticamente na etapa de trabalho.|  
|**(A-MSG)**|Texto de mensagem. Se o trabalho é executado por um alerta, o valor de texto de mensagem substitui este token automaticamente na etapa de trabalho.|  
|**Date**|Data atual (em formato AAAAMMDD).|  
|**Inst**|Nome da instância. Para uma instância padrão, este token terá o nome da instância padrão: MSSQLSERVER.|  
|**JobID**|ID do trabalho.|  
|**(MACH)**|Nome do computador.|  
|**(MSSA)**|Nome do serviço do SQLServerAgent mestre.|  
|**(OSCMD)**|Prefixo do programa usado para executar etapas de trabalho do **CmdExec** .|  
|**(SQLDIR)**|O diretório no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado. Por padrão, este valor é C:\Arquivos de Programas\Microsoft SQL Server\MSSQL.|  
|**(SQLLOGDIR)**|Token de substituição para o caminho da pasta de log de erros do SQL Server – por exemplo, $(ESCAPE_SQUOTE(SQLLOGDIR)).|  
|**(STEPCT)**|Contagem do número de vezes que a etapa foi executada (excluídas novas tentativas). Pode ser usado pelo comando de etapa para forçar terminação de um loop com várias etapas.|  
|**(STEPID)**|ID da etapa.|  
|**(SRVR)**|Nome do computador que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for uma instância nomeada, incluirá o nome da instância.|  
|**MOMENTO**|Hora atual (em formato HHMMSS).|  
|**(STRTTM)**|A hora (em formato HHMMSS) em que o trabalho começou a ser executado.|  
|**(STRTDT)**|A data (em formato AAAAMMDD) em que o trabalho começou a ser executado.|  
|**(WMI (** *propriedade* **))**|Em trabalhos executados em resposta a alertas do WMI, o valor da propriedade especificado por *propriedade*. Por exemplo, `$(WMI(DatabaseName))` fornece o valor da propriedade **DatabaseName** do evento WMI que provocou a execução do alerta.|  
  
### <a name="sql-server-agent-escape-macros"></a>Macros de fuga do SQL Server Agent  
  
|Macros de fuga|Descrição|  
|-------------------|-----------------|  
|**$(ESCAPE_SQUOTE(** *token_name* **))**|Ignora aspas simples (') na cadeia de caracteres de substituição do token. Substitui um aspa simples por duas aspas simples.|  
|**$(ESCAPE_DQUOTE(** *token_name* **))**|Ignora aspas duplas (") na cadeia de caracteres de substituição do token. Substitui um aspa dupla por duas aspas duplas.|  
|**$(ESCAPE_RBRACKET(** *token_name* **))**|Ignora colchetes de fechamento (]) na cadeia de caracteres de substituição do token. Substitui um colchete de fechamento por dois colchetes de fechamento.|  
|**$(ESCAPE_NONE(** *token_name* **))**|Substitui o token sem ignorar nenhum caractere da cadeia. Esta macro é fornecida para dar suporte a compatibilidade retroativa em ambientes nos quais cadeias de caracteres de substituição de tokens são esperadas apenas de usuários confiáveis. Para obter mais informações, consulte "Atualizando etapas de trabalho para usar macros", mais adiante, neste tópico.|  
  
## <a name="updating-job-steps-to-use-macros"></a>Atualizando etapas de trabalho para usar macros  
 A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1, as etapas de trabalho que contêm tokens sem macros de fuga passaram a falhar e a retornar uma mensagem de erro indicando que a etapa contém um ou mais tokens que devem ser atualizados com uma macro para que o trabalho possa ser executado.  
  
 Um script é fornecido com o artigo 915845 da Base de Dados de Conhecimento da [!INCLUDE[msCoName](../../includes/msconame-md.md)] : [Etapas de trabalho do SQL Server Agent que usam tokens falham no SQL Server 2005 Service Pack 1](https://support.microsoft.com/kb/915845). Você pode usar esse script para atualizar todas as suas etapas de trabalho que usam tokens com a macro **ESCAPE_NONE** . Após usar o script, recomendamos que você examine as etapas de trabalho que usam tokens o mais rápido possível e substitua a macro **ESCAPE_NONE** por uma macro de fuga apropriada ao contexto da etapa de trabalho.  
  
 A tabela a seguir descreve como a substituição de tokens é manipulada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para ativar ou desativar a substituição do token de alerta, clique com o botão direito do mouse em **SQL Server Agent** no Pesquisador de Objetos, selecione **Propriedades**e, na página **Sistema de Alerta** , marque ou desmarque a caixa de seleção **Substituir tokens de todas as respostas de trabalho aos alertas** .  
  
|Sintaxe do token|Substituição do token de alerta ativada|Substituição do token de alerta desativada|  
|------------------|--------------------------------|---------------------------------|  
|Macro ESCAPE usada|Todos os tokens em trabalhos são substituídos com êxito.|Não são substituídos tokens ativados por alertas. Esses tokens **são a-DBN**, **a-SVR**, **a-Err**, **a-Sev**, **a-msg**e **WMI (*`property`*)**. Outros tokens estáticos são substituídos com êxito.|  
|Nenhuma macro ESCAPE usada|Todo trabalho contendo tokens falha.|Todo trabalho contendo tokens falha.|  
  
## <a name="token-syntax-update-examples"></a>Exemplos de atualização de sintaxe de token  
  
### <a name="a-using-tokens-in-non-nested-strings"></a>A. Usando tokens em cadeias de caracteres não aninhadas  
 O exemplo a seguir mostra como atualizar um script não aninhado simples com a macro de fuga apropriada. Antes de executar o script de atualização, o seguinte script de etapa de trabalho usa um token para imprimir o nome do banco de dados apropriado:  
  
 `PRINT N'Current database name is $(A-DBN)' ;`  
  
 Executado o script de atualização, uma macro `ESCAPE_NONE` é inserida antes do token `A-DBN` . Como são usadas aspas simples para delimitar a cadeia de caracteres de impressão, é necessário atualizar a etapa de trabalho, inserindo a macro `ESCAPE_SQUOTE` da seguinte maneira:  
  
 `PRINT N'Current database name is $(ESCAPE_SQUOTE(A-DBN))' ;`  
  
### <a name="b-using-tokens-in-nested-strings"></a>B. Usando tokens em cadeias de caracteres aninhadas  
 Em scripts de etapa de trabalho em que são usados tokens em cadeias de caracteres ou instruções aninhadas, estas devem ser rescritas como várias instruções para que possam ser inseridas as macros de fuga apropriadas.  
  
 Por exemplo, considere a seguinte etapa de trabalho, que usa o token `A-MSG` e não foi atualizada com uma macro de fuga:  
  
 `PRINT N'Print ''$(A-MSG)''' ;`  
  
 Executado o script de atualização, uma macro `ESCAPE_NONE` é inserida com o token. Contudo, neste caso, você teria que rescrever o script sem usar aninhamento, como segue, e inserir a macro `ESCAPE_SQUOTE` para ignorar adequadamente delimitadores que pudessem ser transmitidos na cadeia de caracteres de substituição do token:  
  
 `DECLARE @msgString nvarchar(max)`  
  
 `SET @msgString = '$(ESCAPE_SQUOTE(A-MSG))'`  
  
 `SET @msgString = QUOTENAME(@msgString,'''')`  
  
 `PRINT N'Print ' + @msgString ;`  
  
 Note ainda, neste exemplo, que a função QUOTENAME define o caractere aspas.  
  
### <a name="c-using-tokens-with-the-escape_none-macro"></a>C. Usando tokens com a macro ESCAPE_NONE  
 O exemplo a seguir é parte de um script que recupera o `job_id` da tabela `sysjobs` e usa o token `JOBID` para popular a variável `@JobID` , declarada anteriormente no script como tipo de dados binário. Note que, como não são necessários delimitadores para tipos de dados binários, a macro `ESCAPE_NONE` é usada com o token `JOBID` . Você não precisaria atualizar esta etapa de trabalho após executar o script de atualização.  
  
 `SELECT * FROM msdb.dbo.sysjobs`  
  
 `WHERE @JobID = CONVERT(uniqueidentifier, $(ESCAPE_NONE(JOBID))) ;`  
  
## <a name="see-also"></a>Consulte Também  
 [Implementar trabalhos](implement-jobs.md)   
 [Gerenciar etapas de trabalho](manage-job-steps.md)  
  
  
