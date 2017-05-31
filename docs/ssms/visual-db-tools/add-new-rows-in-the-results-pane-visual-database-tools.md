---
title: Adicionar linhas novas ao painel Resultados (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- View Designer, Results pane
- inserting rows
- Query Designer [SQL Server], Results pane
- Results pane
- adding rows
- row additions [SQL Server], Results pane
ms.assetid: 59891c84-3f54-4ab9-8b86-72c59627b480
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0ba11f05536a52023c382e040738b8d9f9a4a215
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="add-new-rows-in-the-results-pane-visual-database-tools"></a>Adicionar linhas novas ao painel Resultados (Visual Database Tools)
Você pode adicionar dados novos digitando-os ou colando-os a partir de outro programa como o Bloco de Notas ou o Excel. Uma linha a ser colada deve ter exatamente o mesmo número e tipos de colunas que a tabela em que você está colando. Você pode colar várias linhas de uma vez no painel Resultados.  
  
Para obter informações sobre como inserir dados, consulte [Regras para atualizar resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-updating-results-visual-database-tools.md).  
  
### <a name="to-add-a-new-data-row"></a>Para adicionar uma nova linha de dados  
  
1.  Navegue até a parte inferior do painel Resultados, onde tiver uma linha em branco disponível para adicionar uma nova linha de dados.  
  
    Os valores iniciais para todas as colunas serão *NULL*.  
  
    > [!TIP]  
    > Para ir diretamente para a primeira linha em branco utilize a barra de navegação na parte inferior do painel Resultados.  
  
2.  Se você estiver colando linhas a partir da Área de Transferência, selecione a nova linha clicando no botão à sua esquerda.  
  
    > [!NOTE]  
    > Se uma ou mais linhas que você estiver colando não puderem ser confirmadas no banco de dados, você receberá uma mensagem indicando quais linhas não puderam ser confirmadas.  
  
3.  Insira os dados da linha nova. Se estiver colando, escolha **Colar** no menu **Editar** .  
  
4.  Deixe essa linha para confirmá-la no banco de dados.  
  
Se ocorrer um erro quando você salvar a linha, o Designer de Consulta e Exibição exibirá uma mensagem e o levará à linha que você estava editando. Em seguida, você pode:  
  
-   Resolver o erro fazendo mais edições na linha.  
  
-   Cancelar a edição pressionando ESC. Se você pressionar ESC enquanto estiver em uma célula alterada, as alterações daquela célula serão canceladas. Se você pressionar ESC enquanto estiver em uma célula que ainda não foi alterada, as alterações de toda a linha serão canceladas.  
  
## <a name="see-also"></a>Consulte também  
[Trabalhar com dados no painel de resultados &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
[Executar operações básicas com consultas &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  

