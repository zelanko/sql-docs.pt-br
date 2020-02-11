---
title: Assistente de cluster (suplementos de mineração de dados para Excel) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087804"
---
# <a name="cluster-wizard-data-mining-add-ins-for-excel"></a>Assistente de Cluster (Suplementos de Mineração de Dados para Excel)
  ![Assistente de Cluster na faixa de opções Mineração de Dados](media/dmc-cluster.gif "Assistente de Cluster na faixa de opções Mineração de Dados")  
  
 O assistente de Cluster ajuda a criar um modelo que detecta as linhas que têm características semelhantes e as agrupa para maximizar a distância entre grupos. Esse assistente é útil para localizar padrões em todos os tipos de dados.  
  
 O assistente de Cluster usa o algoritmo do Microsoft Clustering e pode ser extensivamente personalizado. Ele funciona nos dados existentes de uma tabela do Excel, um intervalo do Excel ou uma consulta do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. A funcionalidade semelhante é fornecida pela ferramenta [detectar categorias](detect-categories-table-analysis-tools-for-excel.md) , fornecida nas ferramentas de análise de tabela para Excel. No entanto, a ferramenta Detectar Categorias não pode ser personalizada e deve usar dados nas tabelas do Excel.  
  
## <a name="using-the-cluster-wizard"></a>Usando o assistente de Cluster  
  
1.  Na faixa de de mineração de dados, clique em **cluster**e em **Avançar**.  
  
2.  Na página **selecionar dados de origem** , selecione uma tabela ou um intervalo do Excel. Ou especifique uma fonte de dados externa.  
  
     Se você usar uma fonte de dados externa, poderá criar exibições personalizadas ou colar um texto de consulta personalizada e salvar o conjunto de dados como uma fonte de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  Na página **clustering** , você pode personalizar a maneira como o modelo é criado.  
  
    -   Para o **número de segmentos**, você pode instruir o assistente a criar um número fixo de categorias ou permitir que ele detecte automaticamente o número ideal de agrupamentos.  
  
    -   Examine a lista de colunas na lista **colunas de entrada** e desmarque as colunas que não são úteis na criação de padrões. As colunas que você deve excluir incluem números de identificação, nomes de clientes e assim por diante.  
  
4.  Opcionalmente, clique em **parâmetros** para alterar os parâmetros do algoritmo e personalizar o comportamento do modelo de clustering.  
  
5.  Na página **dividir os dados em conjuntos de treinamento e teste** , especifique a quantidade de dados a serem retidos para teste. O restante é sempre usado para treinar o modelo.  
  
     A configuração padrão é de 30% de dados para teste e 70% de dados para treinamento.  
  
6.  Na página **concluir** , forneça um nome descritivo para seu conjunto de dados e modelo e defina as seguintes opções que controlam como você trabalha com o modelo concluído:  
  
    -   **Procurar modelo**. Quando essa opção é selecionada, assim que o assistente termina de processar o modelo, ele abre uma janela de **procura** para ajudá-lo a explorar os resultados. O conteúdo do visualizador depende do tipo de modelo que você criou. Para obter mais informações, consulte [navegando em um modelo de clustering](browsing-a-clustering-model.md).  
  
    -   **Habilitar detalhamento**. Selecione esta opção para visualizar os dados subjacentes do modelo finalizado. Essa opção estará disponível somente se você criar um modelo de Árvore de Decisão.  
  
    -   **Use o modelo temporário**. Se você selecionar esta opção, o modelo não será salvo no servidor. Os modelos temporários serão excluídos quando você fechar o Excel.  
  
## <a name="more-about-clustering-models"></a>Mais sobre modelos de clustering  
 Você pode alterar o algoritmo de clustering usado por esse assistente clicando em **avançado** e usando a caixa de diálogo **parâmetros de algoritmo** .  
  
 O algoritmo Clustering da Microsoft fornece estes métodos de clustering:  
  
-   K-means - evolutivo ou não evolutivo.  
  
-   Maximização de Expectativa (EM) - evolutiva ou não evolutiva.  
  
 Você também pode usar o parâmetro CLUSTER_SEED para controlar o valor inicial e garantir que os modelos repetidos que usam o mesmo conjunto de dados tenham os mesmos resultados.  
  
### <a name="requirements"></a>Requisitos  
 Para usar o assistente de Cluster, você deve estar conectado a um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obter mais informações, consulte [conectar-se a dados de origem &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um modelo de mineração de dados](creating-a-data-mining-model.md)   
 [Detectar categorias &#40;ferramentas de análise de tabela para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
  
