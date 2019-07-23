---
title: Opções do Editor do Transact-SQL | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.RESULTS_TO_GRID
- sql.data.tools.SqlExecutionAdvancedSettingsOption
- sql.data.tools.SqlExecutionAnsiSettingsDlg
- sql.data.tools.SqlResultToTextSettingsDlg
- sql.data.tools.SqlExecutionGeneralSettingsDlg
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.GENERAL
- sql.data.tools.unittesting.tsqleditor
- sql.data.tools.SqlResultsToGridSettingsDlg
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.EDITOR_TAB_AND_STATUS_BAR
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_RESULTS.RESULTS_TO_TEXT
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.ANSI
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.GENERAL
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.ONLINE_EDITING
- VS.TOOLSOPTIONSPAGES.SQL_SERVER_TOOLS.TRANSACT-SQL_EDITOR.QUERY_EXECUTION.ADVANCED
ms.assetid: fa9a250f-7feb-433e-91bd-a09779d74c8b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e5de3a6bef68955611290cce77b95989b7ff72c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110630"
---
# <a name="transact-sql-editor-options"></a>Opções do Editor do Transact-SQL
Este tópico contém informações sobre algumas das opções do Editor Transact-SQL. Para definir essas opções, navegue até a caixa de diálogo **Opção** pelo menu **Ferramentas\Opções**.  
  
[Execução da consulta](#QueryExecution)  
  
[Resultados da consulta](#QueryResults)  
  
## <a name="QueryExecution"></a>Execução da consulta  
  
|Propriedade|Descrição|  
|------------|---------------|  
|**SET ROWCOUNT**|O valor padrão de 0 indica que o SQL Server esperará os resultados até que todos os resultados sejam recebidos. Forneça um valor maior que 0 se você quiser que o SQL Server interrompa a consulta depois de obter o número especificado de linhas. Para desligar essa opção (de forma que todas as linhas sejam retornadas), especifique SET ROWCOUNT 0.|  
|**SET TEXTSIZE**|O valor padrão de 2.147.483.647 bytes indica que o SQL Server fornecerá um campo de dados completo até o limite dos campos de dados text, ntext, nvarchar(max) e varchar(max). Não afeta o tipo de dados XML. Forneça um número menor para limitar os resultados no caso de valores grandes. Colunas maiores que o número fornecido serão truncadas.|  
|**Tempo limite de execução**|Indica o número de segundos para aguardar antes de cancelar a consulta. Um valor 0 indica uma espera infinita ou nenhum tempo limite.|  
|**Por padrão, abra consultas novas no Modo SQLCMD**|Marque esta caixa de seleção para abrir novas consultas no modo SQLCMD. Essa caixa de seleção só é visível quando a caixa de diálogo é aberta pelo menu Ferramentas.<br /><br />Ao selecionar essa opção, esteja atento às seguintes limitações:<br /><br />-   O IntelliSense no Editor de Consulta do Mecanismo de Banco de Dados está desativado.<br />-   Como o Editor de Consultas não é executado na linha de comando, você não pode passar parâmetros de linha de comando, como variáveis.<br />-   Como o Editor de Consultas não pode responder a prompts do sistema operacional, você deve ter cuidado para não executar instruções interativas.|  
|**SET NOCOUNT**|Para a mensagem indicando o número de linhas afetadas por uma instrução Transact-SQL impedidas de serem retornadas como parte dos resultados. Para obter mais informações, consulte [SET NOCOUNT](https://go.microsoft.com/fwlink/?LinkID=238731).|  
|**SET NOEXEC**|Quando estiver **ON**, informa ao Microsoft® SQL Server™ para compilar cada lote de instruções Transact-SQL, mas não executá-las. Quando estiver **OFF**, informará ao Microsoft® SQL Server™ para executar todos os lotes após a compilação. Para saber mais, confira [SET NOEXEC](https://go.microsoft.com/fwlink/?LinkId=238770).|  
|**SET PARSEONLY**|Verifica a sintaxe de cada instrução Transact-SQL e retorna as mensagens de erro sem compilar ou executar a instrução. Para obter mais informações, consulte [SET PARSEONLY](https://go.microsoft.com/fwlink/?LinkId=238734)|  
|**SET CONCAT_NULL_YIELDS_NULL**|Controla se os resultados da concatenação são tratados como valores de cadeia de caracteres nulas ou vazias. Para saber mais, confira [SET CONCAT_NULL_YIELDS_NULL](https://go.microsoft.com/fwlink/?LinkId=238733).|  
|**SET ARITHABORT**|Encerra uma consulta quando ocorre estouro ou erro de divisão por zero durante a execução da consulta. Para saber mais, confira [SET ARITHABORT](https://msdn.microsoft.com/library/aa259212(v=SQL.80).aspx).|  
|**SET SHOWPLAN_TEXT**|Faz com que o Microsoft® SQL Server™ não execute instruções Transact-SQL. Em vez disso, o SQL Server retorna informações detalhadas sobre como as instruções são executadas. Para saber mais, confira [SET SHOWPLAN_TEXT](https://go.microsoft.com/fwlink/?LinkID=238737).|  
|**SET STATISTICS TIME**|Exibe o número de milissegundos necessários para analisar, compilar e executar cada instrução.|  
|**SET STATISTICS IO**|Faz com que o Microsoft® SQL Server™ exiba informações referentes à quantidade de atividade em disco gerada pelas instruções Transact-SQL.|  
|**SET TRANSACTION ISOLATION LEVEL**|Controla o comportamento de bloqueio da transação padrão de todas as instruções **SELECT** do Microsoft® SQL Server™ emitidas por uma conexão. Para obter mais informações, consulte  [SET TRANSACTION ISOLATION LEVEL](https://go.microsoft.com/fwlink/?LinkId=238730).|  
|**SET LOCK_TIMEOUT**|Especifica o número de milissegundos que uma instrução espera a liberação de um bloqueio. Para saber mais, confira [SET LOCK_TIMEOUT](https://go.microsoft.com/fwlink/?LinkId=238747)|  
|**SET QUERY_GOVERNOR_COST_LIMIT**|Substitui o valor configurado atualmente pela conexão atual. Para saber mais, confira [SET QUERY_GOVERNOR_COST_LIMIT](https://go.microsoft.com/fwlink/?LinkId=238749).|  
|**SET ANSI_DEFAULTS**|Controla um grupo de configurações do Microsoft® SQL Server™ que especificam coletivamente alguns comportamentos padrão do SQL-92. Para saber mais, confira [SET ANSI_DEFAULTS](https://go.microsoft.com/fwlink/?LinkId=238750).|  
|**SET QUOTED_IDENTIFIER**|Faz com que o Microsoft® SQL Server™ siga as regras SQL-92 referentes à delimitação com aspas de identificadores e cadeias de caracteres literais. Os identificadores delimitados por aspas duplas podem ser palavras-chave reservadas do Transact-SQL ou podem conter caracteres geralmente não permitidos pelas regras de sintaxe Transact-SQL para identificadores. Para saber mais, confira [SET QUOTED_IDENTIFIER](https://go.microsoft.com/fwlink/?LinkId=238751).|  
|**SET ANSI_NULL_DFLT_ON**|Altera o comportamento da sessão para substituir a possibilidade de nulidade de novas colunas quando a opção padrão nulo de ANSI do banco de dados é falsa. Para saber mais, confira [SET ANSI_NULL_DFLT_ON](https://go.microsoft.com/fwlink/?LinkID=238752).|  
|**SET IMPLICIT_TRANSACTIONS**|Quando **ON**, define a conexão para o modo de transação implícita. Quando **OFF**, retorna a conexão para o modo de transação de confirmação automática. Para saber mais, confira [SET IMPLICIT_TRANSACTIONS](https://go.microsoft.com/fwlink/?LinkId=238753).|  
|**SET CURSOR_CLOSE_ON_COMMIT**|Controla se um cursor é fechado quando uma transação é confirmada. Para saber mais, confira [SET CURSOR_CLOSE_ON_COMMIT](https://go.microsoft.com/fwlink/?LinkId=238754).|  
|**SET ANSI_PADDING**|Controla a maneira como a coluna armazena valores menores que o tamanho definido da coluna e a maneira como armazena valores que têm espaços em branco à direita em dados **char**, **varchar**, **binary**e **varbinary** . Para saber mais, confira [SET ANSI_PADDING](https://go.microsoft.com/fwlink/?LinkId=238755).|  
|**SET ANSI_WARNINGS**|Especifica o comportamento padrão SQL-92 para várias condições de erro. Para saber mais, confira [SET ANSI_WARNINGS](https://go.microsoft.com/fwlink/?LinkId=238758).|  
|**SET ANSI_NULLS**|Especifica o comportamento compatível com SQL-92 para os operadores de comparação Igual a ( **=** ) e Diferente de ( **<>** ) quando usados com valores nulos. Para saber mais, confira [SET ANSI_NULLS](https://go.microsoft.com/fwlink/?LinkId=238759).|  
  
## <a name="QueryResults"></a>Resultados da consulta  
  
|Propriedade|Descrição|  
|------------|---------------|  
|**Incluir a consulta no conjunto de resultados**|Retorna o texto da consulta como parte do conjunto de resultados.|  
|**Inclua cabeçalhos de coluna ao copiar ou salvar resultados**|Inclui os cabeçalhos de coluna (títulos) quando os resultados são copiados para a área de transferência ou quando são salvos em um arquivo. Desmarque essa caixa de seleção se você não deseja que os dados de resultados copiados ou salvos contenham apenas os dados e não os cabeçalhos da coluna.|  
|**Descartar resultados após a execução**|Libera memória descartando os resultados da consulta após a tela tê-los recebido.|  
|**Exibir resultados em uma guia separada**|Exibe o conjunto de resultados em uma janela de documentos nova, em vez de na parte inferior da janela de documentos de consulta.|  
|**Alternar para a guia Resultados após a execução da consulta**|Define automaticamente o foco da tela para o conjunto de resultados.|  
|**Máximo de Caracteres Recuperados**|Dados não XML:<br /><br />Digite um número de 1 a 65535 para especificar o número máximo de caracteres que serão exibidos em cada célula. **Observação:** Especificar um número grande de caracteres pode fazer com que os dados no conjunto de resultados apareçam truncados. O número máximo de caracteres exibido em cada célula depende do tamanho da fonte. Quando conjuntos de resultados grandes são retornados, um valor alto nesta caixa pode fazer com que o SQL Server Management Studio seja executado com pouca memória e prejudicar o desempenho do sistema.<br /><br />Dados XML:<br /><br />Selecione 1 MB, 2 MB ou 5 MB. Selecione Ilimitado para recuperar todos os caracteres.|  
|**Formato de saída**|Por padrão, a saída é exibida em colunas criadas preenchendo os resultados com espaços. Outras opções são o uso de vírgulas, tabulações ou espaços para separar as colunas. Marque a caixa de seleção **Delimitador personalizado** para especificar um caractere delimitador diferente na caixa **Delimitador personalizado** .|  
|**Delimitador personalizado**|Especifique o caractere de sua escolha para separar colunas. Essa opção estará disponível somente se a caixa de seleção **Delimitador personalizado** estiver marcada na caixa **Formato de saída** .|  
|**Incluir cabeçalhos de coluna no conjunto de resultados**|Desmarque esta caixa de seleção se não quiser cada coluna rotulada com um título de coluna.|  
|**Rolar à medida que os resultados forem recebidos**|Marque esta caixa de seleção para manter o foco de exibição nos registros retornados mais recentemente na parte inferior. Desmarque esta caixa de seleção para manter o foco de exibição nas primeiras linhas recebidas.|  
|**Alinhar valores numéricos à direita**|Marque esta caixa de seleção para alinhar valores numéricos à direita da coluna. Essa opção pode facilitar a revisão de números com um número fixo de casas decimais.|  
|**Descartar resultado após a execução da consulta**|Libera memória descartando os resultados da consulta depois de serem recebidos pelo monitor.|  
|**Exibir resultados em uma guia separada**|Marque essa caixa de seleção para exibir o conjunto de resultados em uma nova janela de documento, em vez de na parte inferior da janela de documento de consulta.|  
|**Alternar para a guia Resultados após a execução da consulta**|Clique para definir automaticamente o foco da tela no conjunto de resultados.|  
|**Número máximo de caracteres exibidos em cada coluna**|Esse valor padrão é 256. Aumente o valor para exibir conjuntos de resultados maiores sem truncar.|  
|**Restaurar Padrões**|Redefine todos os valores dessa página com os valores padrão originais.|  
  
