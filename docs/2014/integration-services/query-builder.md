---
title: Construtor de consultas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.querybuilder.f1
helpviewer_keywords:
- Query Builder dialog box
ms.assetid: 780752c9-6e3c-4f44-aaff-4f4d5e5a45c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1880ceffb03389bc87ee8f25d1817a5e4f593566
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66056638"
---
# <a name="query-builder"></a>Construtor de Consultas
  Use a caixa de diálogo **Construtor de Consultas** para criar uma consulta a ser usada na tarefa Executar SQL, na origem e no destino OLE DB e na transformação Pesquisa.  
  
 Você pode utilizar o Construtor de Consultas para executar as seguintes tarefas:  
  
-   **Trabalhar com a representação gráfica de uma consulta ou com comandos SQL** O Construtor de Consultas inclui um painel que exibe sua consulta graficamente e um painel que exibe o texto SQL de sua consulta. Você pode trabalhar no painel gráfico ou no painel de texto. O Construtor de Consultas sincroniza as exibições de forma que elas fiquem sempre atuais.  
  
-   **Unir tabelas relacionadas** Se você adicionar mais de uma tabela a sua consulta, o Construtor de Consultas determinará automaticamente como as tabelas serão relacionadas e construirá o comando conjunto apropriado.  
  
-   **Consultar ou atualizar bancos de dados** Você pode usar o Construtor de Consultas para retornar dados usando instruções Transact-SQL SELECT e para criar consultas que atualizam, adicionam ou excluem registros de um banco de dados.  
  
-   **Exibir e editar resultados imediatamente** Você pode executar sua consulta e trabalhar com um conjunto de registros em uma grade que permite percorrer e editar registros no banco de dados.  
  
 As ferramentas gráficas na caixa de diálogo **Construtor de Consultas** permitem que você crie consultas usando usam operações de arrastar e soltar. Por padrão, a caixa de diálogo Construtor de Consultas cria consultas SELECT, mas você também pode criar consultas INSERT, UPDATE ou DELETE. Todos os tipos de instruções SQL podem ser analisados e executados na caixa de diálogo **Construtor de Consultas** . Para obter mais informações sobre instruções SQL em pacotes, consulte [Integration Services &#40;SSIS&#41; Consultas](integration-services-ssis-queries.md).  
  
 Para saber mais sobre a linguagem Transact-SQL e sua consulta, consulte [Referência de Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](/sql/t-sql/language-reference).  
  
 Você também pode usar variáveis em uma consulta para fornecer valores a um parâmetro de entrada, para capturar valores de parâmetros de saída e para armazenar códigos de retorno. Para saber mais sobre como usar variáveis nas consultas usadas por pacotes, consulte [Tarefa Executar SQL](control-flow/execute-sql-task.md), [Fonte OLE DB](data-flow/ole-db-source.md), e [Integration Services &#40;SSIS&#41; Queries](integration-services-ssis-queries.md). Para saber mais sobre o uso de variáveis na Tarefa Executar DQL, consulte [Parâmetros e códigos de retorno na Tarefa Executar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md) e [Conjuntos de resultados na tarefa Executar SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md).  
  
 As transformações Pesquisa e Pesquisa Difusa também podem usar variáveis com parâmetros e códigos de retorno. As informações sobre a origem OLE DB também se aplicam a estas duas transformações.  
  
## <a name="options"></a>Opções  
 **Barra de Ferramentas**  
 Use a barra de ferramentas para gerenciar conjuntos de dados, selecionar painéis para exibição e controlar funções de consulta.  
  
|Valor|Descrição|  
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
  
|Painel|Descrição|  
|----------|-----------------|  
|Painel**Diagrama** |Exibe a consulta em um diagrama. O diagrama mostra as tabelas incluídas na consulta e como elas estão unidas. Marque ou desmarque a caixa de seleção próxima a uma coluna em uma tabela para adicioná-la ou removê-la da saída da consulta.<br /><br /> Quando você adiciona tabelas à consulta, o Construtor de Consultas cria junções entre tabelas com base em tabelas, dependendo das chaves na tabela. Para adicionar uma junção, arraste um campo de uma tabela sobre um campo em outra tabela. Para gerenciar uma junção, clique com o botão direito do mouse na junção e selecione uma opção de menu.<br /><br /> Clique com o botão direito do mouse no painel **Diagrama** para adicionar ou remover tabelas, selecionar todas as tabelas e mostrar ou ocultar painéis.|  
|Painel**Grade** |Exibe a consulta em uma grade. Você pode usar esse painel para adicionar e remover colunas da consulta e alterar as configurações de cada coluna.|  
|Painel**SQL** |Exibe a consulta como texto SQL. As alterações feitas no painel **Diagrama** e no painel **Grade** aparecerão aqui e as alterações feitas aqui aparecerão no painel **Diagrama** e no painel **Grade** .|  
|Painel**Resultados** |Exibe os resultados da consulta quando você clica em **Executar** na barra de ferramentas.|  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa Executar SQL](control-flow/execute-sql-task.md)   
 [Origem de OLE DB](data-flow/ole-db-source.md)   
 [Destino OLE DB](data-flow/ole-db-destination.md)   
 [Transformação Pesquisa](data-flow/transformations/lookup-transformation.md)   
 [Serviços de integração &#40;SSIS&#41; consultas](integration-services-ssis-queries.md)   
 [MERGE em pacotes do Integration Services](control-flow/merge-in-integration-services-packages.md)  
  
  
