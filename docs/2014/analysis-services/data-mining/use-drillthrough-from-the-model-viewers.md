---
title: Usar o detalhamento dos visualizadores do modelo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: e5e065ad-c688-4c2c-8c82-7f3038e04915
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ad62600c6ae48f156049cdae6078df37de0b330
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732588"
---
# <a name="use-drillthrough-from-the-model-viewers"></a>Usar detalhamento dos visualizadores do modelo
  Dependendo do tipo de modelo, você pode usar o detalhamento dos visualizadores de procura na guia **Visualizador de Modelo de Mineração** de Designer de Mineração de Dados para explorar os casos usados no modelo de mineração ou consultar colunas adicionais na estrutura de mineração. Embora muitos tipos de modelos não ofereçam suporte ao detalhamento porque os padrões no modelo não podem ser vinculados diretamente a casos específicos, os tipos de modelos a seguir oferecem suporte ao detalhamento.  
  
 Note que esse detalhamento deve ter sido habilitado no modelo e você deve ter as permissões apropriadas. A opção de detalhamento também pode ser desabilitada se o estado do modelo é não processado, independentemente de o modelo ter sido processado anteriormente e de ter conteúdo. Para recuperar dados de caso de modelo usando o detalhamento, o cache da estrutura e o modelo devem ser atuais.  
  
### <a name="use-drillthrough-in-the-microsoft-tree-viewer"></a>Usar o detalhamento no Visualizador de Árvores da Microsoft  
  
1.  No Designer de Mineração de Dados, selecione o modelo de árvores de decisão e selecione **Procurar Modelo** para abrir o modelo no **Visualizador de Árvores da Microsoft**. No SQL Server Management Studio, clique com o botão direito do mouse no modelo e selecione **Procurar**  
  
2.  Clique com o botão direito do mouse em qualquer nó no gráfico de árvore e selecione **Detalhar**.  
  
3.  Selecione uma das opções a seguir: **Colunas de modelo somente** ou **modelar e estruturar colunas**. Se você não tiver permissões, talvez uma opção não esteja disponível.  
  
4.  A caixa de diálogo **Detalhar** é aberta, exibindo os dados de caso e/ou os dados de estrutura. A barra de título da caixa de diálogo também contém uma descrição que identifica o nó do qual a consulta de detalhamento foi executada.  
  
5.  Clique com o botão direito do mouse em qualquer ponto nos resultados e selecione **Copiar Tudo** para salvar os resultados na Área de Transferência.  
  
### <a name="use-drillthrough-in-the-microsoft-cluster-viewer"></a>Usar o detalhamento no Visualizador de Cluster da Microsoft  
  
1.  No Designer de Mineração de Dados, selecione um modelo de clustering e selecione **Procurar Modelo** para abrir o modelo no **Visualizador de Cluster da Microsoft**. No SQL Server Management Studio, clique com o botão direito do mouse no modelo e selecione **Procurar**.  
  
2.  Na guia **Cluster** , clique com o botão direito do mouse em qualquer nó.  
  
3.  Selecione **drill-through**e, em seguida, selecione uma das seguintes opções: **Colunas de modelo somente** ou **modelar e estruturar colunas**. Se você não tiver permissões, talvez uma opção não esteja disponível.  
  
4.  A caixa de diálogo **Detalhar** é aberta, exibindo os dados de caso e/ou os dados de estrutura. A barra de título da caixa de diálogo também contém uma descrição que identifica o cluster para os casos.  
  
5.  Clique com o botão direito do mouse em qualquer ponto nos resultados e selecione **Copiar Tudo** para salvar os resultados na Área de Transferência.  
  
### <a name="use-drillthrough-in-the-microsoft-association-rules-viewer"></a>Usar o detalhamento no Visualizador de Regras de Associação da Microsoft  
  
1.  No Designer de Mineração de Dados, selecione um modelo de associação e selecione **Procurar Modelo** para abrir o modelo no **Visualizador de Regras de Associação da Microsoft**. No SQL Server Management Studio, clique com o botão direito do mouse no modelo e selecione **Procurar**  
  
2.  Na guia **Regras** , clique com o botão direito do mouse em qualquer linha que represente uma regra. Na guia **Conjuntos de itens** , clique em qualquer linha que contenha um conjunto de itens.  
  
3.  Selecione **drill-through**e, em seguida, selecione uma das seguintes opções: **Colunas de modelo somente** ou **modelar e estruturar colunas**. Se você não tiver permissões, talvez uma opção não esteja disponível.  
  
4.  A caixa de diálogo **Detalhar** é aberta, exibindo os dados de caso e/ou os dados de estrutura. A barra de título da caixa de diálogo também contém uma descrição que identifica o nome da regra.  
  
5.  Clique com o botão direito do mouse em qualquer ponto nos resultados e selecione **Copiar Tudo** para salvar os resultados de casos completos na Área de Transferência. Você também pode selecionar **Copiar** para copiar apenas o caso selecionado. Se o modelo contiver uma coluna de tabela aninhada, só o nome da coluna de tabela aninhada será colado; para recuperar os valores de dados dentro da coluna de tabela aninhada para cada caso, crie uma consulta no conteúdo modelo.  
  
### <a name="use-drillthrough-in-the-microsoft-sequence-cluster-viewer"></a>Usar o detalhamento no Visualizador de Cluster de Sequência da Microsoft  
  
1.  No Designer de Mineração de Dados, selecione um modelo de clustering e selecione **Procurar Modelo** para abrir o modelo no **Visualizador de Cluster da Microsoft**. No SQL Server Management Studio, clique com o botão direito do mouse no modelo e selecione **Procurar**.  
  
2.  Na **guia Diagrama de Cluster**, clique com o botão direito do mouse em qualquer nó que represente um cluster. Na guia **Perfis de Cluster** , clique em qualquer ponto em um perfil de cluster ou no cluster que representa a população modelo total.  
  
3.  Selecione **drill-through**e, em seguida, selecione uma das seguintes opções: **Colunas de modelo somente** ou **modelar e estruturar colunas**. Se você não tiver permissões, talvez uma opção não esteja disponível.  
  
4.  A caixa de diálogo **Detalhar** é aberta, exibindo os dados de caso e/ou os dados de estrutura. A barra de título da caixa de diálogo também contém uma descrição que identifica o cluster para os casos.  
  
5.  Clique com o botão direito do mouse em qualquer ponto nos resultados e selecione **Copiar Tudo** para salvar os resultados na Área de Transferência. Se o modelo contiver uma coluna de tabela aninhada, só o nome da coluna de tabela aninhada será colado; para recuperar os valores de dados dentro da coluna de tabela aninhada para cada caso, crie uma consulta no conteúdo modelo.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do visualizador do modelo de mineração](mining-model-viewer-tasks-and-how-tos.md)   
 [Detalhamento em modelos de mineração](drillthrough-on-mining-models.md)   
 [Detalhamento em estruturas de mineração](drillthrough-on-mining-structures.md)  
  
  
