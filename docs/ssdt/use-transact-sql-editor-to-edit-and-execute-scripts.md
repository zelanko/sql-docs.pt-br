---
title: Usar o Editor Transact-SQL para editar e executar scripts | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.SQLEDITOR
ms.assetid: fa78e2cf-3c64-49f5-93cc-a3d50b1e7d05
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2c2b84cb9f75987995e9e0cdbf92165fa28f61a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006035"
---
# <a name="use-transact-sql-editor-to-edit-and-execute-scripts"></a>Usar o Editor Transact-SQL para editar e executar scripts
O Editor Transact\-SQL proporciona uma experiência avançada de edição e depuração quando você está trabalhando com scripts. Ele é invocado quando você usa o menu contextual **Exibir Código** para abrir uma entidade de banco de dados em um banco de dados conectado ou um projeto. Ele também é aberto automaticamente quando você usa o menu contextual **Nova Consulta** no Pesquisador de Objetos do SQL Server ou adiciona um novo objeto de script a um projeto de banco de dados.  
  
Se você não estiver conectado a um banco de dados, mas quiser executar uma consulta em algum, também poderá usar a caixa de diálogo **Nova Conexão de Consulta** na opção de menu **SQL** -> **Transact\-Editor SQL** para se conectar a um banco de dados e iniciar o Editor Transact\-SQL.  
  
O Editor Transact\-SQL contém um painel **T-SQL** principal onde é possível gravar e editar scripts Transact\-SQL. O editor dá suporte a IntelliSense assim como a codificação de cor de sintaxe para melhorar a legibilidade de instruções complexas. Ele também dá suporte a localizar e substituir, comentários em lote, fontes e cores personalizadas, e numeração de linha. Você também pode alterar o banco de dados no qual o script no editor será executado. Para obter mais informações, confira [Como clonar um banco de dados existente](../ssdt/how-to-clone-an-existing-database.md). O painel **Resultados** exibe os resultados da consulta em uma grade ou texto. Você também pode redirecionar resultados da consulta para um arquivo. O painel **Mensagem** exibe erros, avisos e mensagens informativas que são retornados quando um script é executado. Quando as estatísticas de cliente estão habilitadas, o painel **Estatísticas** exibe informações sobre a execução de consulta agrupada em categorias. O painel **Plano de Execução** exibe os métodos de recuperação de dados escolhidos pelo SQL Server e mostra o custo de execução de instruções e consultas específicas.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|---------|---------------|  
|[Como: estruturar tópicos e adicionar snippets a scripts Transact-SQL](../ssdt/how-to-outline-and-add-snippets-to-transact-sql-script.md)|Use o Selecionador de Snippet para inserir código Transact\-SQL pronto para codificar a sua consulta.|  
|[Como: navegar entre scripts](../ssdt/how-to-navigate-between-scripts.md)|Use a Ir para Definição e Localizar todas as referências para navegar entre scripts.|  
|[Como: usar renomeação e refatoração para fazer alterações em seus objetos de banco de dados](../ssdt/how-to-use-rename-and-refactoring-to-make-changes-to-your-database-objects.md)|Renomeie um objeto em todos os scripts e visualize as alterações.|  
|[Como: executar uma consulta parcial](../ssdt/how-to-execute-a-partial-query.md)|Realce um segmento específico do script e execute-o como uma única consulta.|  
|[Como: Depurar Procedimentos Armazenados](../ssdt/how-to-debug-stored-procedures.md)|Crie e depure um procedimento armazenado Transact\-SQL passo a passo.|  
|[Analisar o desempenho do script](../ssdt/analyze-script-performance.md)|Use planos de execução, estatísticas de cliente e análise de código para determinar se você pode melhorar o desempenho de sua consulta, procedimentos armazenados ou scripts.|  
  
## <a name="see-also"></a>Consulte Também  
[Como: Criar novos objetos de banco de dados usando consultas](../ssdt/how-to-create-new-database-objects-using-queries.md)  
  
