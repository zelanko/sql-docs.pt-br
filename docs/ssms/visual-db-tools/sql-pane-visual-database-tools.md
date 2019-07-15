---
title: Painel SQL (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], SQL pane
- View Designer, SQL pane
- SQL pane [Visual Database Tools]
ms.assetid: dbabab18-0614-415b-a2ef-9bcd0d320d5c
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 84c55898c5aefd30fda0caef49436a02953bab03
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67689761"
---
# <a name="sql-pane-visual-database-tools"></a>Painel SQL (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você pode usar o painel SQL para criar sua própria instrução SQL, ou pode usar os painéis de Critérios e Diagrama para criar a instrução, caso em que as instruções SQL serão criadas no painel SQL. À medida que você cria a consulta, o painel SQL é atualizado e reformatado automaticamente para ser lido com facilidade.  
  
Para abrir o painel SQL, primeiro abra o Designer de Consulta e Exibição (com um objeto de banco de dados selecionado no Gerenciador de Servidores, no menu **Banco de Dados** , clique em **Nova Consulta**). Em seguida, no menu **Designer de Consultas** , aponte para o **Painel** e clique em **SQL**.  
  
No painel SQL você pode:  
  
-   Criar novas consultas entrando as instruções SQL.  
  
-   Modificar a instrução SQL criada pelo Designer de Consulta e Exibição baseado nas configurações que você faz nos painéis de Diagrama e Critérios.  
  
-   Digitar as instruções que tiram proveito de recursos específicos para o banco de dados você está usando.  
  
> [!NOTE]  
> Certifique-se de que você saiba as regras para identificar os objetos de banco de dados no banco de dados que você está usando. Para obter detalhes, veja a documentação para seu sistema de administração de banco de dados.  
  
## <a name="statements-in-the-sql-pane"></a>Instruções no painel SQL  
Você pode editar a consulta atual diretamente no painel SQL. Quando você vai para outro painel, o Designer de Consulta e Exibição automaticamente formata sua instrução, e então altera os painéis Diagrama e Critérios para corresponder a sua instrução.  
  
Se sua instrução não puder ser representada nos painéis Diagrama e Critérios, e se esses painéis estiverem visíveis, o Designer de Consulta e Exibição exibirá um erro e então lhe oferecerá duas opções:  
  
-   Ignorar que a instrução não pode ser representada nos painéis Diagrama e Critérios.  
  
-   Desfazer a mudança que não pode ser representada e reverter à versão mais recente versão da instrução SQL.  
  
Se você escolher ignorar que a instrução não pode ser representada nos painéis Diagrama e Critérios, o Designer de Consulta e Exibição escurecerá os outros painéis para indicar que eles já não refletem o conteúdo do painel SQL.  
  
Você pode continuar editando a instrução e executá-la como você faria com qualquer instrução SQL.  
  
> [!NOTE]  
> Se você inserir uma instrução SQL, mas depois fizer mais alterações na consulta alterando os painéis Diagrama e Critérios, o Designer de Consulta e Exibição recria e exibe novamente a instrução SQL. Em alguns casos, esta ação resulta em uma instrução SQL que é construída de forma diferente daquela que você inseriu originalmente (embora vá sempre render os mesmos resultados). Esta diferença é particularmente possível quando você estiver trabalhando com critérios de pesquisa que envolvam várias cláusulas associadas a AND e OR.  
  
## <a name="see-also"></a>Consulte Também  
[Criar consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[Executar consultas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Painel Diagrama &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[Painel Critérios &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[Painel de Resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)  
  
