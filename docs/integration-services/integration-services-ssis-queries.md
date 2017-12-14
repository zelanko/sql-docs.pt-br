---
title: Consultas do SSIS (Integration Services) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.querybuilder.f1
helpviewer_keywords:
- Query Builder [Integration Services]
- queries [Integration Services]
- statements [Integration Services]
- queries [Integration Services], about queries in packages
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
caps.latest.revision: "58"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 81dd719383f3a05356d15677ce61bad5e8962807
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-ssis-queries"></a>Consultas do SSIS (Integration Services)
  A tarefa Executar SQL, a origem OLE DB, o destino OLE DB e a transformação Pesquisa podem usar consultas de SQL. Na tarefa Executar SQL, as instruções SQL podem criar, atualizar e excluir objetos de banco de dados e dados; executar procedimentos armazenados e executar instruções SELECT. Na origem OLE DB e na transformação Pesquisa, as instruções SQL são normalmente instruções SELECT ou EXEC. Esta última normalmente executa procedimentos que retornam conjuntos de resultados.  
  
 Uma consulta pode ser analisada para estabelecer se é válida. Ao analisar uma consulta que usa uma conexão com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], a consulta é analisada, executada e o resultado de execução (sucesso ou falha) é atribuído ao resultado da análise. Se a consulta usar uma conexão com dados que seja diferente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], a instrução só será analisada.  
  
Você pode fornecer a instrução SQL das seguintes maneiras:
1.   Insira-a diretamente no designer.
2.   Especifique uma conexão a um arquivo que contém a instrução.
3.   Especifique uma variável que contém a instrução.  
  
## <a name="direct-input-sql"></a>SQL de entrada direta  
 O Construtor de Consultas está disponível na interface do usuário para a tarefa Executar SQL, a origem OLE DB, o destino OLE DB e a transformação Pesquisa. O Construtor de Consultas oferece as seguintes vantagens:  
  
-   Possibilidade de trabalhar visualmente com comandos SQL.  
  
     O Construtor de Consultas inclui painéis gráficos que compõem a consulta visualmente e um painel de texto que exibe o texto SQL de sua consulta. Você pode trabalhar nos painéis gráfico ou de texto. O Construtor de Consultas sempre sincroniza as exibições de forma que o texto da consulta e a representação gráfica sempre sejam correspondentes.  
  
-   Possibilidade de unir tabelas relacionadas.  
  
     Se você adicionar mais de uma tabela a sua consulta, o Construtor de Consultas determinará automaticamente como as tabelas estão relacionadas e construirá o comando de junção apropriado.  
  
-   Consulta ou atualização de bancos de dados.  
  
     Você pode usar o Construtor de Consultas para retornar dados usando instruções Transact-SQL SELECT ou para criar consultas que atualizem, adicionem ou excluam registros de um banco de dados.  
  
-   Exibição e edição imediatas de resultados.  
  
     Você pode executar sua consulta e trabalhar com um conjunto de registros em uma grade que permite rolagem e edição de registros no banco de dados.  
  
 Embora o Construtor de Consultas seja visualmente limitado para criação de consultas SELECT, você pode digitar o SQL para outros tipos de instruções como DELETE e UPDATE no painel de texto. O painel gráfico é atualizado automaticamente para refletir a instrução SQL digitada.  
  
 Você também pode fornecer entrada direta digitando a consulta na caixa de diálogo de componente de tarefa ou fluxo de dados ou na janela Propriedades.  
  
 Para obter mais informações, consulte [Query Builder](http://msdn.microsoft.com/library/780752c9-6e3c-4f44-aaff-4f4d5e5a45c5).  
  
## <a name="sql-in-files"></a>SQL em arquivos  
 A instrução SQL da tarefa Executar SQL também pode residir em um arquivo separado. Por exemplo, você pode escrever consultas usando ferramentas como o Editor de Consultas no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], salvar a consulta em um arquivo e depois ler a consulta no arquivo ao executar um pacote. O arquivo pode conter apenas as instruções SQL para execução e comentários. Para usar uma instrução SQL armazenada em um arquivo, forneça uma conexão de arquivo que especifique o nome do arquivo e o local. Para obter mais informações, consulte [File Connection Manager](../integration-services/connection-manager/file-connection-manager.md).  
  
## <a name="sql-in-variables"></a>SQL em variáveis  
 Se a origem da instrução SQL na tarefa Executar SQL for uma variável, forneça o nome da variável que contém a consulta. A propriedade Value da variável contém o texto de consulta. Você define a propriedade ValueType da variável como um tipo de dados String e digita ou copia a instrução SQL na propriedade Value. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md) e [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  

## <a name="query-builder-dialog-box"></a>Caixa de diálogo Construtor de Consultas
Use a caixa de diálogo **Construtor de Consultas** para criar uma consulta a ser usada na tarefa Executar SQL, na origem e no destino OLE DB e na transformação Pesquisa.  
  
 Você pode utilizar o Construtor de Consultas para executar as seguintes tarefas:  
  
-   **Trabalhar com a representação gráfica de uma consulta ou com comandos SQL** O Construtor de Consultas inclui um painel que exibe sua consulta graficamente e um painel que exibe o texto SQL de sua consulta. Você pode trabalhar no painel gráfico ou no painel de texto. O Construtor de Consultas sincroniza as exibições de forma que elas fiquem sempre atuais.  
  
-   **Unir tabelas relacionadas** Se você adicionar mais de uma tabela a sua consulta, o Construtor de Consultas determinará automaticamente como as tabelas serão relacionadas e construirá o comando conjunto apropriado.  
  
-   **Consultar ou atualizar bancos de dados** Você pode usar o Construtor de Consultas para retornar dados usando instruções Transact-SQL SELECT e para criar consultas que atualizam, adicionam ou excluem registros de um banco de dados.  
  
-   **Exibir e editar resultados imediatamente** Você pode executar sua consulta e trabalhar com um conjunto de registros em uma grade que permite percorrer e editar registros no banco de dados.  
  
 As ferramentas gráficas na caixa de diálogo **Construtor de Consultas** permitem que você crie consultas usando usam operações de arrastar e soltar. Por padrão, a caixa de diálogo Construtor de Consultas cria consultas SELECT, mas você também pode criar consultas INSERT, UPDATE ou DELETE. Todos os tipos de instruções SQL podem ser analisados e executados na caixa de diálogo **Construtor de Consultas** . Para obter mais informações sobre instruções SQL em pacotes, consulte [Integration Services &#40;SSIS&#41; Consultas](../integration-services/integration-services-ssis-queries.md).  
  
 Para saber mais sobre a linguagem Transact-SQL e sua consulta, consulte [Referência de Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](../t-sql/transact-sql-reference-database-engine.md).  
  
 Você também pode usar variáveis em uma consulta para fornecer valores a um parâmetro de entrada, para capturar valores de parâmetros de saída e para armazenar códigos de retorno. Para saber mais sobre como usar variáveis nas consultas usadas por pacotes, consulte [Tarefa Executar SQL](../integration-services/control-flow/execute-sql-task.md), [Fonte OLE DB](../integration-services/data-flow/ole-db-source.md), e [Integration Services &#40;SSIS&#41; Queries](../integration-services/integration-services-ssis-queries.md). Para saber mais sobre o uso de variáveis na Tarefa Executar DQL, consulte [Parâmetros e códigos de retorno na Tarefa Executar SQL](http://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663) e [Conjuntos de resultados na tarefa Executar SQL](http://msdn.microsoft.com/library/62605b63-d43b-49e8-a863-e154011e6109).  
  
 As transformações Pesquisa e Pesquisa Difusa também podem usar variáveis com parâmetros e códigos de retorno. As informações sobre a origem OLE DB também se aplicam a estas duas transformações.  
  
### <a name="options"></a>Opções  
 **Barra de Ferramentas**  
 Use a barra de ferramentas para gerenciar conjuntos de dados, selecionar painéis para exibição e controlar funções de consulta.  
  
|Value|Description|  
|-----------|-----------------|  
|**Painel Mostrar/Ocultar Diagrama**|Exibe ou oculta o painel **Diagrama** .|  
|**Painel Mostrar/Ocultar Grade**|Exibe ou oculta o painel **Grade** .|  
|**Painel Mostrar/Ocultar SQL**|Exibe ou oculta o painel **SQL** .|  
|**Painel Mostrar/Ocultar Resultados**|Exibe ou oculta o painel de **Resultados** .|  
|**Executar**|Executa a consulta. Os resultados são exibidos no painel de Resultados.|  
|**Verificar SQL**|Verifica se a instrução SQL é válida.|  
|**Classificar em Ordem Crescente**|Classifica as linhas de saída na coluna selecionada no painel Grade em ordem crescente.|  
|**Classificar em Ordem Decrescente**|Classifica as linhas de saída na coluna selecionada no painel Grade em ordem decrescente.|  
|**Remover Filtro**|Selecione um nome de coluna no painel de grade e clique em **Remover Filtro** para remover os critérios de classificação da coluna.|  
|**Usar Agrupar Por**|Adiciona a funcionalidade GROUP BY à consulta.|  
|**Adicionar Tabela**|Adiciona uma nova tabela à consulta.|  
  
 **Definição da Consulta**  
 A definição de consulta fornece uma barra de ferramentas e painéis nos quais definir e testar a consulta.  
  
|Painel|Description|  
|----------|-----------------|  
|Painel**Diagrama** |Exibe a consulta em um diagrama. O diagrama mostra as tabelas incluídas na consulta e como elas estão unidas. Marque ou desmarque a caixa de seleção próxima a uma coluna em uma tabela para adicioná-la ou removê-la da saída da consulta.<br /><br /> Quando você adiciona tabelas à consulta, o Construtor de Consultas cria junções entre tabelas com base em tabelas, dependendo das chaves na tabela. Para adicionar uma junção, arraste um campo de uma tabela sobre um campo em outra tabela. Para gerenciar uma junção, clique com o botão direito do mouse na junção e selecione uma opção de menu.<br /><br /> Clique com o botão direito do mouse no painel **Diagrama** para adicionar ou remover tabelas, selecionar todas as tabelas e mostrar ou ocultar painéis.|  
|Painel**Grade** |Exibe a consulta em uma grade. Você pode usar esse painel para adicionar e remover colunas da consulta e alterar as configurações de cada coluna.|  
|Painel**SQL** |Exibe a consulta como texto SQL. As alterações feitas no painel **Diagrama** e no painel **Grade** aparecerão aqui e as alterações feitas aqui aparecerão no painel **Diagrama** e no painel **Grade** .|  
|Painel**Resultados** |Exibe os resultados da consulta quando você clica em **Executar** na barra de ferramentas.| 

  
