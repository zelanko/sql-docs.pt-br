---
title: Editor de consulta de mineração de dados avançado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 27e7fc46-689d-43a4-9647-1c27d182bdd6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4973ea427cea99d6e3c4527e8686e322a97efe48
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72313605"
---
# <a name="advanced-data-mining-query-editor"></a>Editor de Consulta Avançada de Mineração de Dados
  A **Editor avançado de consulta de mineração de dados** é uma ferramenta para ajudá-lo a criar modelos e consultas personalizados.  
  
 O editor fornece um conjunto de modelos com links clicáveis. Basta clicar em cada link e usar as caixas de diálogo para selecionar objetos ou valores, e criar instruções DMX complexas. Você pode alternar a exibição para o modelo de edição de texto para modificar manualmente a instrução DMX.  
  
 Para acessar o **Editor avançado de consulta de mineração de dados**, clique em **consulta** e, em seguida, clique em **avançado**.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Painel Consulta DMX**  
 Aqui você pode consultar a instrução DMX atual.  
  
 Clique com o botão direito do mouse no painel para copiar a instrução DMX atual.  
  
 Também é possível clicar em qualquer parte destacada da instrução para obter opções específicas dessa cláusula. Por exemplo, para excluir, adicionar ou editar uma saída, clique com o botão direito do mouse no link ** \<>de saída** .  
  
 **Editar Consulta/Construtor de Consultas**  
 Use esse botão para alternar o editor entre um editor de texto, no qual você pode escrever instruções DMX diretamente; e o **Construtor de consultas**, que ajuda a criar uma instrução DMX.  
  
> [!NOTE]  
>  **AVISO:** Se você alternar entre exibições antes da execução da consulta, será exibida uma mensagem informando que você pode perder algumas alterações. Se a instrução DMX for válida, em muitos casos a **Construtor de consultas** poderá converter essas alterações com êxito. No entanto, se criar uma instrução DMX particularmente complexa, você deverá salvar seu trabalho antes de alternar exibições.  
  
 **Modelos DMX**  
 Clique e selecione em uma lista de modelos que contenha exemplos de DMX. Os modelos oferecem todo tipo de modelo ou consulta de previsão que você possa precisar, inclusive consultas que usam tabelas aninhadas e instruções DMX para gerenciar modelos. Mesmo que você tenha algum conhecimento de DMX, os modelos poderão economizar tempo ao usar a sintaxe correta.  
  
 **Escolher modelo**  
 Clique para exibir uma lista de modelos de mineração de dados disponíveis na conexão atual.  
  
 Você também pode exibir uma lista de modelos disponíveis clicando no nome do modelo na instrução DMX no painel de **consulta DMX** . O nome do modelo normalmente é realçado em vermelho.  
  
 **Selecione a entrada**  
 Clique para escolher os dados a serem usados como entrada para o modelo de mineração. Se nenhuma fonte de dados tiver sido especificada, você também poderá clicar ** \<** no link>de entrada, que é realçado em vermelho no painel de **consulta DMX** .  
  
 Selecione ** \@InputRowset** na lista suspensa para abrir a caixa de diálogo **substituir InputRowset** e modificar uma entrada existente.  
  
 Selecione **Adicionar entrada** para abrir a caixa de diálogo **Adicionar entrada** e especifique uma nova fonte de dados.  
  
 Você também pode modificar uma entrada existente clicando no ** \@link InputRowset** , que é realçado em vermelho no painel de consulta DMX.  
  
 **Mapear Colunas**  
 Selecione colunas do modelo de mineração e mapeie-as para colunas na fonte de dados externa.  
  
 Você também pode clicar no link realçado ** \<>** no painel consulta DMX.  
  
 **Adicionar Saída**  
 Clique para escolher as colunas que devem ser incluídas na saída como parte de uma consulta de previsão.  
  
 Você também pode clicar no link ** \<adicionar saída>** realçado no painel consulta DMX.  
  
 **Colunas do Modelo**  
 Lista as colunas no modelo de mineração selecionado. Um losango ao lado do nome da coluna indica que ela é uma coluna previsível.  
  
 **Colunas de Entrada**  
 Lista as colunas da fonte de dados externa que foram adicionadas como entradas.  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;de consulta SQL Server suplementos de mineração de dados&#41;](query-sql-server-data-mining-add-ins.md)  
  
  
