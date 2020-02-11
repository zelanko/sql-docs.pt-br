---
title: Matriz de classificação (SQL Server suplementos de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- classification matrix
- confusion table
- mining models, testing
ms.assetid: d6f620f4-39af-4714-9628-28ce3c361fca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 78f8581839b6b4bdd761c25a1a207e942ae37f62
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087966"
---
# <a name="classification-matrix-sql-server-data-mining-add-ins"></a>Matriz de classificação (Suplementos de Mineração de Dados do SQL Server)
  ![Botão Matriz de Classificação, faixa de opções Mineração de dados](media/dmc-cmatrix.gif "Botão Matriz de Classificação, faixa de opções Mineração de dados")  
  
 Você pode usar a matriz de classificação para avaliar a precisão de um modelo para previsão. Para gerar uma matriz de classificação, você executar um conjunto de dados de teste através do modelo, e a ferramenta da matriz de classificação compara os valores reais do conjunto de teste com as previsões feitas pelo modelo. Ao examinar a matriz, você pode identificar rapidamente com que frequência o modelo está correto, e a frequência de previsões erradas.  
  
 Nestes suplementos, use o assistente de **matriz de classificação** para selecionar um modelo, especifique os dados de teste e, em seguida, gere uma matriz de resultados.  
  
## <a name="how-to-read-a-classification-matrix"></a>Como ler uma matriz de classificação  
 Vamos supor que seu objetivo é criar um programa de fidelidade do cliente e atribuir os clientes às categorias apropriadas, para que você possa fornecê-los com o nível apropriado de incentivos. Você implementou três níveis para o programa de recompensa--bronze, prata e ouro – e os deu aos clientes em uma fase de avaliação. Você também criou um modelo que analisa clientes e prevê as categorias corretas. Agora você usará a matriz de classificação nos dados de avaliação para determinar quão bom era o modelo em prever a oferta correta para todos os clientes.  
  
 A tabela da matriz de classificação mostra quantos clientes seriam atribuídos a cada categoria com base no modelo, e compara esse resultado ao número de clientes que de fato se inscreveram em cada nível de recompensa.  
  
||Bronze (real)|Ouro (real)|Prata (real)|  
|-|-----------------------|---------------------|-----------------------|  
|Bronze|**94,45%**|15,18%|1,70%|  
|Gold|2,72%|**84,82%**|0.00%|  
|Silver|1,84%|0.00%|**93,80%**|  
|*Correto*|*95,45%*|*84,82%*|*98,30%*|  
|*Classificados incorretamente*|*4,55%*|*15,18%*|*1,70%*|  
  
-   Cada coluna mostra os valores reais no conjunto de dados de teste.  
  
-   Cada linha exibe os valores previstos.  
  
-   Os valores em negrito, executados diagonalmente do canto superior esquerdo para o canto inferior direito da matriz, mostram até que ponto o modelo deu certo.  
  
-   Todos os demais valores fora da diagonal representam erros. Alguns erros são falsos positivos; isso significa que o modelo previu que o cliente se associaria ao programa de ouro, mas ele estava errado.  Dependendo de seu domínio, os falsos positivos podem ser muito dispendiosos.  
  
     Outros são falsos negativos; isso significa que o modelo previu que o cliente não estaria interessado, embora não tivesse se associado ao programa. Novamente, dependendo do domínio do problema, o custo dessa oportunidade perdida pode ser significativo.  
  
## <a name="using-the-classification-matrix-wizard"></a>Usando o Assistente da Matriz de Classificação  
  
1.  Selecione o modelo de mineração no qual basear as previsões.  
  
2.  Selecione uma fonte de novos dados de teste, ou use os dados de teste que foram salvos com a estrutura.  
  
3.  Selecione a coluna cuja precisão você deseja avaliar. Você pode escolher apenas uma coluna ao criar uma matriz, mas a coluna pode ter vários valores.  
  
     Dica: talvez seja difícil interpretar uma matriz de classificação se a coluna previsível tiver muitas colunas a serem comparadas.  
  
     Na página **selecionar colunas a serem previstas** , você também pode especificar se deseja exibir a contagem de valores incorretos e incorretos ou exibir uma porcentagem.  
  
4.  Na página Selecionar Dados de Origem, indique se você está usando dados de teste externos, ou os dados de teste salvos com o modelo.  
  
5.  Se você usar dados de teste externos, será necessário mapear o modelo para as colunas de entrada na página **especificar relação** do assistente.  
  
     Se você usar o conjunto de dados de teste inserido, o mapeamento será realizado para você  
  
6.  Clique em **concluir** para executar previsões em relação ao modelo e gerar a matriz de classificação.  
  
     O assistente cria um relatório que contém a matriz de classificação e outros detalhes sobre a análise. Este relatório é salvo como uma tabela no Excel, com um resumo acima do relatório que indica quantos casos foram previstos corretamente e quantas previsões foram incorretas.  
  
### <a name="requirements"></a>Requisitos  
  
-   Para criar uma matriz de classificação, você deve ter acesso a um modelo de mineração existente que dá suporte à medida de precisão. Modelos de previsão e modelos de associação não podem ser medidos usando essa ferramenta.  
  
-   O modelo que você está medindo precisa prever um valor que seja discreto ou que já tenha sido discretizado.  
  
-   Se você não usou a opção para salvar um conjunto de testes junto com sua estrutura ou modelo, você precisa obter um conjunto de dados de entrada que tenha basicamente o mesmo número de colunas, com tipos de dados correspondentes, como aqueles usados no modelo.  
  
-   O modelo de mineração de dados e os novos dados que você estiver usando para teste deverão conter pelo menos uma coluna que possa ser prevista, e as colunas devem conter o mesmo tipo de dados.  
  
### <a name="known-issues"></a>Problemas conhecidos  
 No SQL Server 2012 e SQL Server 2014, a capacidade de mapear o conjunto de dados de teste interno para o modelo não está funcionando na ferramenta de **matriz de classificação** . No entanto, você pode especificar um conjunto de dados externo, e selecionar o treinamento definido como a entrada para determinar o erro no conjunto de dados original.  
  
## <a name="see-also"></a>Consulte Também  
 [Validando modelos e usando modelos para previsão &#40;suplementos de mineração de dados para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [Explorar dados &#40;SQL Server suplementos de mineração de dados&#41;](explore-data-sql-server-data-mining-add-ins.md)   
 [Detectar categorias &#40;ferramentas de análise de tabela para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
  
