---
title: Cluster Assistente (Data Mining Add-ins para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [data mining]
ms.assetid: 85b25625-a7ab-4960-9f9c-df22e8ecae37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d93f676aec67b5d791924cbbda8f71a966d5bbc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087804"
---
# <a name="cluster-wizard-data-mining-add-ins-for-excel"></a>Assistente de Cluster (Suplementos de Mineração de Dados para Excel)
  ![Assistente de cluster na faixa de opções mineração de dados](media/dmc-cluster.gif "Assistente de Cluster na faixa de opções mineração de dados")  
  
 O assistente de Cluster ajuda a criar um modelo que detecta as linhas que têm características semelhantes e as agrupa para maximizar a distância entre grupos. Esse assistente é útil para localizar padrões em todos os tipos de dados.  
  
 O assistente de Cluster usa o algoritmo do Microsoft Clustering e pode ser extensivamente personalizado. Ele funciona nos dados existentes de uma tabela do Excel, um intervalo do Excel ou uma consulta do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Uma funcionalidade semelhante é fornecida pelos [detectar categorias](detect-categories-table-analysis-tools-for-excel.md) ferramenta, fornecida nas ferramentas de análise de tabela para Excel. No entanto, a ferramenta Detectar Categorias não pode ser personalizada e deve usar dados nas tabelas do Excel.  
  
## <a name="using-the-cluster-wizard"></a>Usando o assistente de Cluster  
  
1.  Na faixa de opções mineração de dados, clique em **Cluster**e, em seguida, clique em **próxima**.  
  
2.  No **Selecionar fonte de dados** , selecione uma tabela do Excel ou um intervalo. Ou especifique uma fonte de dados externa.  
  
     Se você usar uma fonte de dados externa, poderá criar exibições personalizadas ou colar um texto de consulta personalizada e salvar o conjunto de dados como uma fonte de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  Sobre o **Clustering** página, você pode personalizar a maneira que o modelo é criado.  
  
    -   Para **número de segmentos**, você pode informar ao Assistente para criar um número fixo de categorias ou deixá-lo detectar automaticamente o número ideal de agrupamentos.  
  
    -   Examine a lista de colunas na **colunas de entrada** listar e desmarque as colunas que não são úteis na criação de padrões. As colunas que você deve excluir incluem números de identificação, nomes de clientes e assim por diante.  
  
4.  Opcionalmente, clique em **parâmetros** para alterar os parâmetros de algoritmo e personalizar o comportamento do modelo de clustering.  
  
5.  No **dividir dados em conjuntos de teste e treinamento** , especifique a quantidade de dados será mantida para teste. O restante é sempre usado para treinar o modelo.  
  
     A configuração padrão é de 30% de dados para teste e 70% de dados para treinamento.  
  
6.  Sobre o **concluir** página, forneça um nome descritivo para o conjunto de dados e o modelo e defina as seguintes opções que controlam como você trabalha com o modelo finalizado:  
  
    -   **Procurar modelo**. Quando essa opção é selecionada, assim que o assistente tiver concluído o processamento do modelo, ele abre uma **procurar** janela para ajudá-lo a explorar os resultados. O conteúdo do visualizador depende do tipo de modelo que você criou. Para obter mais informações, consulte [procurando um modelo de Clustering](browsing-a-clustering-model.md).  
  
    -   **Habilitar o detalhamento**. Selecione esta opção para visualizar os dados subjacentes do modelo finalizado. Essa opção estará disponível somente se você criar um modelo de Árvore de Decisão.  
  
    -   **Usar modelo temporário**. Se você selecionar esta opção, o modelo não será salvo no servidor. Os modelos temporários serão excluídos quando você fechar o Excel.  
  
## <a name="more-about-clustering-models"></a>Mais informações sobre modelos de Clustering  
 Você pode alterar o algoritmo de clustering usado por esse assistente clicando **Advanced** e usando o **parâmetros de algoritmo** caixa de diálogo.  
  
 O algoritmo Clustering da Microsoft fornece estes métodos de clustering:  
  
-   K-means - evolutivo ou não evolutivo.  
  
-   Maximização de Expectativa (EM) - evolutiva ou não evolutiva.  
  
 Você também pode usar o parâmetro CLUSTER_SEED para controlar o valor inicial e garantir que os modelos repetidos que usam o mesmo conjunto de dados tenham os mesmos resultados.  
  
### <a name="requirements"></a>Requisitos  
 Para usar o assistente de Cluster, você deve estar conectado a um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obter mais informações, consulte [conectar-se a fonte de dados &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar um modelo de mineração de dados](creating-a-data-mining-model.md)   
 [Detectar categorias &#40;ferramentas de análise de tabela para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
  
