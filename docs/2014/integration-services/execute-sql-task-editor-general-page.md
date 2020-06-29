---
title: Editor da tarefa Executar SQL (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.general.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: beb39086-28ce-46af-b6d8-f7b4fb8d9069
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 32bec035646c976442eb66ff1270b961835b243b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85429193"
---
# <a name="execute-sql-task-editor-general-page"></a>Editor da Tarefa Executar SQL (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Executar SQL** para configurar a tarefa Executar SQL e fornecer a instrução SQL executada pela tarefa.  
  
 Para saber mais sobre essa tarefa, consulte [Tarefa Executar SQL](control-flow/execute-sql-task.md) e [Parâmetros e códigos de retorno na Tarefa Executar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md) e [Conjuntos de resultados na tarefa Executar SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md). Para saber mais sobre a linguagem de consulta Transact-SQL, consulte [Referência de Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](/sql/t-sql/language-reference).  
  
## <a name="static-options"></a>Opções estáticas  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Executar SQL no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a tarefa Executar SQL. Como prática recomendável, para tornar os pacotes autodocumentados e mais fáceis de manter, descreva a tarefa de acordo com a sua finalidade.  
  
 **Cedido**  
 Especifique o número máximo de segundos que a tarefa será executada antes de atingir o tempo limite. Um valor de 0 indica um tempo infinito. O padrão é 0.  
  
> [!NOTE]  
>  Procedimentos armazenados não atingirão o tempo limite se emularem uma funcionalidade de suspensão fornecendo um tempo para que as conexões sejam estabelecidas e as transações completadas sejam maior que o número de segundos especificados pelo **TimeOut**. Porém, os procedimentos armazenados que executam as consultas estão sempre sujeitos à restrição de tempo especificada pelo **TimeOut**.  
  
 **Código**  
 Especifique a página de código a ser usada ao converter valores Unicode em variáveis. O valor padrão é a página de código do computador local.  
  
> [!NOTE]  
>  Quando a tarefa Executar SQL usa um gerenciador de conexões ADO ou ODBC, a propriedade **CodePage** não fica disponível. Se a sua solução requer o uso de uma página de código, utilize um gerenciador de conexões OLE DB ou ADO.NET com a tarefa Executar SQL.  
  
 **TypeConversionMode**  
 Quando você definir essa propriedade como `Allowed`, a Tarefa Executar SQL tentará converter o parâmetro de saída e os resultados da consulta no tipo de dados da variável à qual os resultados estão atribuídos. Isso se aplica ao tipo de conjunto de resultados de **Linha única** .  
  
 **ResultSet**  
 Especifique o tipo de resultado esperado pela instrução SQL que está sendo executada. Escolha entre **Linha Simples**, **Conjunto de Resultados Completo**, **XML**, ou **Nenhum**.  
  
 **ConnectionType**  
 Escolha o tipo de gerenciador de conexões a ser usado para conectar-se à fonte de dados. Os tipos de conexão disponíveis incluem **OLE DB**, **ODBC**, **ADO**, **ADO.NET** e **SQLMOBILE**.  
  
 **Tópicos relacionados:** [Gerenciador de conexões do OLE DB](connection-manager/ole-db-connection-manager.md)e [Gerenciador de conexões ODBC](connection-manager/odbc-connection-manager.md)e [Gerenciador de conexões ADO](connection-manager/ado-connection-manager.md)e [Gerenciador de conexões ADO.NET](connection-manager/ado-net-connection-manager.md)e [Gerenciador de conexões do SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **Conexão**  
 Escolha a conexão a partir de uma lista definida de gerenciadores de conexões. Para criar uma nova conexão, selecione \<**New connection...**> .  
  
 **SQLSourceType**  
 Selecione o tipo de origem da instrução SQL que a tarefa executa.  
  
 Dependendo do tipo de gerenciador de conexões que a tarefa Executar SQL utiliza, você deve usar marcadores de parâmetro específicos em instruções SQL com parâmetros.  
  
 **Tópicos Relacionados:** seção Executando comandos SQL com parâmetros em [Tarefa Executar SQL](control-flow/execute-sql-task.md)  
  
 As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a fonte como uma instrução Transact-SQL. Selecionando esse valor, a opção dinâmica **Instrução SQL**é exibida.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém uma instrução Transact-SQL. Definindo essa opção, a opção dinâmica **FileConnection**é exibida.|  
|**Variável**|Defina a fonte como uma variável que identifique a instrução Transact-SQL. Selecionando esse valor, a opção dinâmica **SourceVariable**é exibida.|  
  
 **QueryIsStoredProcedure**  
 Indica se a instrução SQL especificada a ser executada é um procedimento armazenado. Essa propriedade será de somente leitura/gravação se a tarefa usar o gerenciador de conexões ADO. Caso contrário a propriedade será somente leitura e seu valor será `false`.  
  
 **BypassPrepare**  
 Indique se a instrução SQL está preparada.  `true` ignora a preparação; `false` prepara a instrução SQL antes de executá-la. Essa opção só está disponível com conexões OLE DB que dão suporte à preparação.  
  
 **Tópicos relacionados:**  [Execução preparada](../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **Procurar**  
 Localize um arquivo que contém uma instrução SQL usando a caixa de diálogo **Abrir** . Selecione um arquivo para copiar o conteúdo do arquivo como uma instrução SQL para a propriedade **SQLStatement** .  
  
 **Construir Consulta**  
 Crie uma instrução SQL usando a caixa de diálogo **Construtor de Consultas** , uma ferramenta gráfica usada para criar consultas. Esta opção está disponível quando a opção **SQLSourceType** é definida como **Entrada Direta**.  
  
 **Analisar consulta**  
 Valide a sintaxe da instrução SQL.  
  
## <a name="sqlsourcetype-dynamic-options"></a>Opções dinâmicas SQLSourceType  
  
### <a name="sqlsourcetype--direct-input"></a>SQLSourceType = Entrada direta  
 **SQLStatement**  
 Digite a instrução SQL a ser executada na caixa de opção ou clique no botão procurar (...) para digitar a instrução SQL na caixa de diálogo **Inserir consulta SQL** ou clique em **criar consulta** para compor a instrução usando a caixa de diálogo **Construtor de consultas** .  
  
 **Tópicos relacionados:** [Construtor de Consultas](../../2014/integration-services/query-builder.md)  
  
### <a name="sqlsourcetype--file-connection"></a>SQLSourceType = Conexão do Arquivo  
 **FileConnection**  
 Selecione um Gerenciador de conexões de arquivo existente ou clique \<**New connection...**> para criar um novo Gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="sqlsourcetype--variable"></a>SQLSourceType = Variável  
 **SourceVariable**  
 Selecione uma variável existente ou clique \<**New variable...**> para criar uma nova variável.  
  
 **Tópicos relacionados:** [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa Executar SQL &#40;página mapeamento de parâmetro&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [Editor da tarefa Executar SQL &#40;página conjunto de resultados&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
  
