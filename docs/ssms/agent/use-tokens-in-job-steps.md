---
title: Usar tokens em etapas de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c6a48d0eb6abae94ba6e3c54e0aa5b0b6b874371
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65089447"
---
# <a name="use-tokens-in-job-steps"></a>Usar tokens em etapas de trabalho
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent permite usar tokens em scripts de etapas de trabalho [!INCLUDE[tsql](../../includes/tsql-md.md)] . O uso de tokens para escrever suas etapas de trabalho oferece a mesma flexibilidade fornecida por variáveis ao escrever programas de software. Quando você insere um token em um script de etapa de trabalho, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent o substitui em tempo de execução, antes de o trabalho ser executado pelo subsistema [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
  
## <a name="understanding-using-tokens"></a>Noções básicas sobre o uso de tokens  
  
> [!IMPORTANT]  
> Qualquer usuário Windows com permissões de gravação no Log de Eventos do Windows pode acessar etapas de trabalho ativadas pelos alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent ou alertas do WMI. Para evitar riscos de segurança, os tokens do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que podem ser usados em trabalhos ativados por alertas encontram-se desabilitados por padrão. Esses tokens são: **A-DBN**, **A-SVR**, **A-ERR**, **A-SEV**, **A-MSG** e **WMI(** _propriedade_ **)** . Observe que nesta versão, o uso de tokens foi estendido a todos os alertas.  
>   
> Se tiver que usar esses tokens, garanta, primeiro, que apenas membros dos grupos de segurança confiáveis do Windows, como o grupo Administradores, tenham permissões de gravação no Log de Eventos do computador em que reside o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Depois, clique com o botão direito do mouse em **SQL Server Agent** no Pesquisador de Objetos, selecione **Propriedades**e, na página **Sistema de Alerta** , selecione **Substituir tokens de todas as respostas de trabalho aos alertas** para habilitar esses tokens.  
  
A substituição de tokens do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é simples e eficiente: O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent substitui um valor de cadeia de caracteres literal exato para o token. Todos os tokens diferenciam maiúsculas de minúsculas. Suas etapas de trabalho devem levar isto em conta e usar aspas corretamente nos tokens utilizados ou converter a cadeia de caracteres de substituição pelo tipo de dados correto.  
  
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
|---------|---------------|  
|**(A-DBN)**|Nome do banco de dados. Se o trabalho é executado por um alerta, o valor de nome de banco de dados substitui este token automaticamente na etapa de trabalho.|  
|**(A-SVR)**|Nome de servidor. Se o trabalho é executado por um alerta, o valor de nome de servidor substitui este token automaticamente na etapa de trabalho.|  
|**(A-ERR)**|Número de erro. Se o trabalho é executado por um alerta, o valor de número de erro substitui este token automaticamente na etapa de trabalho.|  
|**(A-SEV)**|Severidade do erro. Se o trabalho é executado por um alerta, o valor de severidade do erro substitui este token automaticamente na etapa de trabalho.|  
|**(A-MSG)**|Texto de mensagem. Se o trabalho é executado por um alerta, o valor de texto de mensagem substitui este token automaticamente na etapa de trabalho.|  
|**(JOBNAME)**|O nome do trabalho. Esse token só está disponível no SQL Server 2016 e posterior.|  
|**(STEPNAME)**|O nome da etapa. Esse token só está disponível no SQL Server 2016 e posterior.|  
|**(DATE)**|Data atual (em formato AAAAMMDD).|  
|**(INST)**|Nome da instância. Para uma instância padrão, este token terá o nome da instância padrão: MSSQLSERVER.|  
|**(JOBID)**|ID do trabalho.|  
|**(MACH)**|Nome do computador.|  
|**(MSSA)**|Nome do serviço do SQLServerAgent mestre.|  
|**(OSCMD)**|Prefixo do programa usado para executar etapas de trabalho do **CmdExec** .|  
|**(SQLDIR)**|O diretório no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado. Por padrão, este valor é C:\Arquivos de Programas\Microsoft SQL Server\MSSQL.|  
|**(SQLLOGDIR)**|Token de substituição para o caminho da pasta de log de erros do SQL Server – por exemplo, $(ESCAPE_SQUOTE(SQLLOGDIR)). Esse token só está disponível no SQL Server 2014 e posterior.|  
|**(STEPCT)**|Contagem do número de vezes que a etapa foi executada (excluídas novas tentativas). Pode ser usado pelo comando de etapa para forçar terminação de um loop com várias etapas.|  
|**(STEPID)**|ID da etapa.|  
|**(SRVR)**|Nome do computador que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for uma instância nomeada, incluirá o nome da instância.|  
|**(TIME)**|Hora atual (em formato HHMMSS).|  
|**(STRTTM)**|A hora (em formato HHMMSS) em que o trabalho começou a ser executado.|  
|**(STRTDT)**|A data (em formato AAAAMMDD) em que o trabalho começou a ser executado.|  
|**(WMI (** _propriedade_ **))**|Em trabalhos executados em resposta a alertas do WMI, o valor da propriedade especificado por *propriedade*. Por exemplo, `$(WMI(DatabaseName))` fornece o valor da propriedade **DatabaseName** do evento WMI que provocou a execução do alerta.|  
  
### <a name="sql-server-agent-escape-macros"></a>Macros de fuga do SQL Server Agent  
  
|Macros de fuga|Descrição|  
|-----------------|---------------|  
|**$(ESCAPE_SQUOTE(** _nome\_do token_ **))**|Ignora aspas simples (') na cadeia de caracteres de substituição do token. Substitui um aspa simples por duas aspas simples.|  
|**$(ESCAPE_DQUOTE(** _nome\_do token_ **))**|Ignora aspas duplas (") na cadeia de caracteres de substituição do token. Substitui um aspa dupla por duas aspas duplas.|  
|**$(ESCAPE_RBRACKET(** _nome\_do token_ **))**|Ignora colchetes de fechamento (]) na cadeia de caracteres de substituição do token. Substitui um colchete de fechamento por dois colchetes de fechamento.|  
|**$(ESCAPE_NONE(** _nome\_do token_ **))**|Substitui o token sem ignorar nenhum caractere da cadeia. Esta macro é fornecida para dar suporte a compatibilidade retroativa em ambientes nos quais cadeias de caracteres de substituição de tokens são esperadas apenas de usuários confiáveis. Para obter mais informações, consulte "Atualizando etapas de trabalho para usar macros", mais adiante, neste tópico.|  
  
## <a name="updating-job-steps-to-use-macros"></a>Atualizando etapas de trabalho para usar macros  
A tabela a seguir descreve como a substituição de tokens é manipulada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para ativar ou desativar a substituição do token de alerta, clique com o botão direito do mouse em **SQL Server Agent** no Pesquisador de Objetos, selecione **Propriedades**e, na página **Sistema de Alerta** , marque ou desmarque a caixa de seleção **Substituir tokens de todas as respostas de trabalho aos alertas** .  
  
|Sintaxe do token|Substituição do token de alerta ativada|Substituição do token de alerta desativada|  
|----------------|------------------------------|-------------------------------|  
|Macro ESCAPE usada|Todos os tokens em trabalhos são substituídos com êxito.|Não são substituídos tokens ativados por alertas. São eles: **A-DBN**, **A-SVR**, **A-ERR**, **A-SEV**, **A-MSG**e **WMI(** _propriedade_ **)** . Outros tokens estáticos são substituídos com êxito.|  
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
  
<pre>DECLARE @msgString nvarchar(max)  
SET @msgString = '$(ESCAPE_SQUOTE(A-MSG))'  
SET @msgString = QUOTENAME(@msgString,'''')  
PRINT N'Print ' + @msgString ;</pre>  
  
Note ainda, neste exemplo, que a função QUOTENAME define o caractere aspas.  
  
### <a name="c-using-tokens-with-the-escapenone-macro"></a>C. Usando tokens com a macro ESCAPE_NONE  
O exemplo a seguir é parte de um script que recupera o `job_id` da tabela `sysjobs` e usa o token `JOBID` para popular a variável `@JobID` , declarada anteriormente no script como tipo de dados binário. Note que, como não são necessários delimitadores para tipos de dados binários, a macro `ESCAPE_NONE` é usada com o token `JOBID` . Você não precisaria atualizar esta etapa de trabalho após executar o script de atualização.  
  
<pre>SELECT * FROM msdb.dbo.sysjobs  
WHERE @JobID = CONVERT(uniqueidentifier, $(ESCAPE_NONE(JOBID))) ;</pre>  
  
## <a name="see-also"></a>Consulte Também  
[Implementar trabalhos](../../ssms/agent/implement-jobs.md)  
[Gerenciar etapas de trabalho](../../ssms/agent/manage-job-steps.md)  
  
