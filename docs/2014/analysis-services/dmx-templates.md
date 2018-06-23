---
title: Modelos DMX | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2a577e52-821d-4bd3-ba35-075a6be285c9
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d0f29e0c000477ec705111f433c31370edc0d973
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120906"
---
# <a name="dmx-templates"></a>Modelos DMX
  Os modelos de mineração de dados o ajudam a criar rapidamente consultas sofisticadas. Embora a sintaxe geral para consultas DMX seja bem-documentada, usar os modelos torna mais fácil criar consultas clicando e apontando para argumentos e fontes de dados.  
  
## <a name="using-the-templates"></a>Usando os modelos  
  
1.  No cliente mineração de dados para Excel, clique em **consulta**.  
  
2.  No Assistente de **iniciar** , clique em **próximo**.  
  
3.  Na página, **Selecionar modelo**, clique em **avançado**.  
  
     **Dica:** se você pretende criar uma consulta de previsão em um modelo, selecione o modelo primeiro e, em seguida, clique em **avançado**para pré-popular o modelo com o nome do modelo.  
  
4.  No **Editor mineração de dados avançado consulta**, clique em **modelos DMX**e selecione um modelo.  
  
5.  Pressione ENTER para carregar o modelo no painel Consulta DMX.  
  
6.  Continue clicando nos links no modelo e, quando a caixa de diálogo for exibida, selecione uma saída, um modelo ou um parâmetro apropriado.  
  
     Para consultas de previsão, escolha o conjunto de dados de entrada primeiro e depois mapeie as colunas.  
  
7.  Clique em **Editar consulta** para alternar para a exibição do editor de texto e alterar manualmente a consulta.  
  
     Saiba que, se você alternar exibições ao trabalhar no editor de consulta, quaisquer informações contidas na exibição anterior serão limpas. Antes de alterar as exibições, salve seu trabalho copiando e colando as instruções DMX em um arquivo separado.  
  
8.  Clique em **Concluir**. No **Escolher destino** caixa de diálogo, especifique onde deseja salvar os resultados. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Se você executou uma instrução com êxito, a instrução DMX que você enviou para o servidor também será registrada no **rastreamento** janela. Para obter mais informações sobre como usar o recurso de rastreamento, consulte [rastreamento &#40;cliente de mineração de dados para Excel&#41;](trace-data-mining-client-for-excel.md).  
  
 Para obter mais informações sobre como usar o Data Mining Editor de consulta avançada, consulte [consulta &#40;suplementos de mineração de dados do SQL Server&#41; ](query-sql-server-data-mining-add-ins.md) e [Editor de consulta de mineração de dados avançada](advanced-data-mining-query-editor.md).  
  
## <a name="list-of-dmx-templates"></a>Lista de modelos DMX  
 Os seguintes modelos DMX são incluídos no Cliente de Mineração de Dados para Excel.  
  
 **previsão**  
  
 Use esses modelos para criar consultas de previsão avançadas, inclusive as consultas sem suporte dos assistentes nos suplementos, como as consultas que usam tabelas aninhadas ou fontes de dados externas.  
  
-   Previsões filtradas  
  
-   Previsões aninhadas filtradas  
  
-   Previsões aninhadas  
  
-   Previsões singleton  
  
-   Previsões padrão  
  
-   Previsões de série temporal  
  
-   Consulta de previsão TOP  
  
-   Consulta de previsão TOP em tabela aninhada  
  
 **Criar**  
  
 Use esses modelos para criar modelos ou estruturas de dados personalizados. Você não está limitado aos modelos com suporte dos assistentes – é possível usar qualquer algoritmo de mineração de dados com suporte da instância de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a qual você está conectado, inclusive algoritmos de plug-in.  
  
-   modelo de mineração  
  
-   Estrutura de mineração  
  
-   Estrutura de mineração com controle  
  
-   Modelo temporário  
  
-   Estrutura temporária  
  
 **Propriedades de modelo**  
  
 Use esses modelos para criar consultas que obtêm metadados sobre o modelo e o conjunto de treinamento. Você também pode recuperar detalhes do conteúdo do modelo ou obter um perfil estatístico dos dados de treinamento.  
  
-   Conteúdo do modelo de mineração  
  
-   Valores mínimo e máximo de coluna  
  
-   Casos de teste/treinamento da estrutura de mineração  
  
-   Valores discretos de coluna  
  
 **Gerenciamento**  
  
 Use esses modelos para executar qualquer tarefa de gerenciamento com suporte no DMX, o que inclui importar e exportar modelos, excluir modelos e limpar modelos e estruturas de dados.  
  
-   Limpar modelo de mineração  
  
-   Limpar estrutura e modelos  
  
-   Limpar estrutura de mineração  
  
-   Excluir modelo de mineração  
  
-   Excluir estrutura de mineração  
  
-   Renomear modelo de mineração  
  
-   Renomear estrutura de mineração  
  
-   Treinar modelo de mineração  
  
-   Treinar estrutura de mineração aninhada  
  
-   Treinar estrutura de mineração  
  
### <a name="requirements"></a>Requisitos  
 Dependendo do modelo usado, talvez você precise de permissões administrativas para acessar o servidor [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e executar a consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um modelo de mineração de dados](creating-a-data-mining-model.md)  
  
  