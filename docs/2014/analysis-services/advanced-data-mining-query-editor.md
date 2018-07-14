---
title: Advanced Editor de consulta de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 27e7fc46-689d-43a4-9647-1c27d182bdd6
caps.latest.revision: 9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 75347810fafa87828dd09653059e9a403a1892ef
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167663"
---
# <a name="advanced-data-mining-query-editor"></a>Editor de consulta de mineração de dados avançados
  O **Data Mining Editor de consulta avançada** é uma ferramenta para ajudar você a criar modelos e consultas personalizadas.  
  
 O editor fornece um conjunto de modelos com links clicáveis. Basta clicar em cada link e usar as caixas de diálogo para selecionar objetos ou valores, e criar instruções DMX complexas. Você pode alternar a exibição para o modelo de edição de texto para modificar manualmente a instrução DMX.  
  
 Para obter o **Data Mining Editor de consulta avançada**, clique em **consulta** e, em seguida, clique em **avançado**.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Painel consulta DMX**  
 Aqui você pode consultar a instrução DMX atual.  
  
 Clique com o botão direito do mouse no painel para copiar a instrução DMX atual.  
  
 Também é possível clicar em qualquer parte destacada da instrução para obter opções específicas dessa cláusula. Por exemplo, para excluir, adicionar ou editar uma saída, clique com botão direito do  **\<saída >** link.  
  
 **Editar consulta/construtor de consultas**  
 Use esse botão para alternar o editor entre um editor de texto, onde você pode escrever instruções DMX diretamente; e o **construtor de consultas**, que ajuda a você cria uma instrução DMX.  
  
> [!NOTE]  
>  **Aviso:** se você alternar exibições antes da execução de consulta, será exibida uma mensagem informando que você pode perder algumas alterações. Se a instrução DMX for válida, em muitos casos as **construtor de consultas** pode converter com êxito essas alterações. No entanto, se criar uma instrução DMX particularmente complexa, você deverá salvar seu trabalho antes de alternar exibições.  
  
 **Modelos DMX**  
 Clique e selecione em uma lista de modelos que contenha exemplos de DMX. Os modelos oferecem todo tipo de modelo ou consulta de previsão que você possa precisar, inclusive consultas que usam tabelas aninhadas e instruções DMX para gerenciar modelos. Mesmo que você tenha algum conhecimento de DMX, os modelos poderão economizar tempo ao usar a sintaxe correta.  
  
 **Escolha o modelo**  
 Clique para exibir uma lista de modelos de mineração de dados disponíveis na conexão atual.  
  
 Você também pode exibir uma lista de modelos disponíveis clicando no nome do modelo na instrução do DMX a **consulta DMX** painel. O nome do modelo normalmente é realçado em vermelho.  
  
 **Selecione a entrada**  
 Clique para escolher os dados a serem usados como entrada para o modelo de mineração. Se nenhuma fonte de dados tiver sido especificado, você também pode clicar de  **\<entrada >** link, que é realçado em vermelho na **consulta DMX** painel.  
  
 Selecione **@InputRowset** na lista suspensa para abrir o **substituir InputRowset** caixa de diálogo caixa e modificar uma entrada existente.  
  
 Selecione **Adicionar entrada** para abrir o **Adicionar entrada** caixa de diálogo caixa e especifique uma nova fonte de dados.  
  
 Você também pode modificar uma entrada existente clicando o **@InputRowset** link, que é realçado em vermelho no painel consulta DMX.  
  
 **Mapear colunas**  
 Selecione colunas do modelo de mineração e mapeie-as para colunas na fonte de dados externa.  
  
 Você também pode clicar em destacada  **\<mapeamento >** link no painel consulta DMX.  
  
 **Adicionar Saída**  
 Clique para escolher as colunas que devem ser incluídas na saída como parte de uma consulta de previsão.  
  
 Você também pode clicar em destacada  **\<adicionar saída >** link no painel consulta DMX.  
  
 **Colunas do modelo**  
 Lista as colunas no modelo de mineração selecionado. Um losango ao lado do nome da coluna indica que ela é uma coluna previsível.  
  
 **Colunas de Entrada**  
 Lista as colunas da fonte de dados externa que foram adicionadas como entradas.  
  
## <a name="see-also"></a>Consulte também  
 [Consulta &#40;suplementos de mineração de dados do SQL Server&#41;](query-sql-server-data-mining-add-ins.md)  
  
  
