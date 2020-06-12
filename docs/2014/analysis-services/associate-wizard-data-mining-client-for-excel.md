---
title: Assistente de associação (cliente de mineração de dados para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- nested tables, in association models
- association [data mining]
ms.assetid: 4db6462f-93c7-443f-8ff7-39474dc7029e
author: minewiskan
ms.author: owend
ms.openlocfilehash: 52542ac1b15b59ecebca4ea26ba530298157ed50
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527937"
---
# <a name="associate-wizard-data-mining-client-for-excel"></a>Assistente para Associação (Cliente de Mineração de Dados para Excel)
  ![Assistente para Associação na faixa de opções Mineração de Dados](media/dmc-associate.gif "Assistente para Associação na faixa de opções Mineração de Dados")  
  
 O assistente para Associação o ajuda a criar um modelo de mineração de dados usando o algoritmo Regras de Associação da [!INCLUDE[msCoName](../includes/msconame-md.md)]. Esses modelos de mineração são particularmente úteis para a criação de *sistemas de recomendação*.  
  
 Eles funcionam da seguinte maneira: o algoritmo de Regras de Associação da [!INCLUDE[msCoName](../includes/msconame-md.md)] verifica um conjunto de dados composto de transações ou eventos, e localiza as combinações que aparecem frequentemente juntas. Pode haver milhares de combinações, mas o algoritmo pode ser personalizado para obter mais ou menos, e para reter apenas as combinações mais prováveis.  
  
 Você pode aplicar a análise da associação a vários problemas. A aplicação mais popular desse método é a análise da cesta de compras, que localiza produtos individuais que são geralmente comprados juntos. Você pode usar essas informações para recomendar produtos para os clientes com base nos itens que eles já compraram.  
  
## <a name="using-the-associate-wizard"></a>Usando o Assistente para Associação  
  
1.  Na faixa de faixas de **mineração de dados** , clique em **associar**.  
  
2.  Na página **selecionar dados de origem** , escolha uma tabela ou intervalo de dados do Excel e clique em **Avançar**.  
  
     A pasta de trabalho de dados de exemplo contém um exemplo, na guia Associar, de como os dados da transação são normalmente organizados se, por exemplo, você tem vários produtos em cada transação ou vários registros de compra por cliente que você quer analisar.  
  
     Se você quiser usar dados externos para criar um modelo de associação usando o assistente associado, será necessário adicionar os dados ao Excel primeiro e *mesclar* os dados. Para obter mais informações sobre como preparar dados para modelagem de associação, consulte [tabelas aninhadas &#40;Analysis Services de mineração de dados&#41;](data-mining/nested-tables-analysis-services-data-mining.md), em manuais online do SQL Server.  
  
3.  Na página **Associação** , escolha a coluna que identifica a transação.  
  
     Para modelos da cesta de compras, esse identificador representa a unidade que você deseja modelar. Você deseja analisar os itens individuais que os clientes compraram ao longo do tempo ou deseja analisar muitas transações que envolvem vários clientes? No primeiro caso, você escolheria a ID do cliente; no último, você escolheria a ordem de compra ou outra ID da transação  
  
4.  Para **Item**, selecione a coluna que contém as coisas entre as quais você precisa localizar associações.  
  
     Por exemplo, em um modelo de cesta de compras, você escolheria um campo de produtos, para analisar quais produtos são geralmente comprados juntos. Se houver muitos produtos individuais para correlacionar com eficiência, você poderá escolher um campo de categoria ou subcategoria de produto.  
  
5.  Em **limites**, você pode definir valores que controlam ou afetam a saída do modelo:  
  
    -   **Suporte mínimo.** Especifica quantas vezes um grupo de itens deve aparecer para ser considerado importante. O algoritmo ignorará todas as combinações de itens que não satisfaçam esse critério. Por exemplo, você pode querer ver apenas os conjuntos de itens que aparecem juntos pelo menos 10 vezes no total.  
  
    -   **Probabilidade de regra mínima**. Especifica o valor da probabilidade mínima exigida para uma regra ser salva. O conjunto de dados inteiro é analisado para localizar todas as combinações e, em seguida, a probabilidade é calculada. Se o limite for baixo, o assistente poderá associar os itens que tiverem apenas pouca correlação. Se o limite for muito alto, algumas associações poderão ser omitidas porque não tem dados de suporte suficientes.  
  
     Em geral, alterar esses valores tem os seguintes efeitos:  
  
    -   À medida que você reduz o valor do suporte, aumenta o número de combinações encontradas.  
  
    -   À medida que você diminui o suporte máximo, filtra os itens que ocorrem com tanta frequência que significam muito pouco.  
  
    -   À medida que você reduz a probabilidade de uma regra, diminui os requisitos que uma combinação precisa atender para ser considerara importante no contexto do conjunto de dados total.  
  
     **Dica:** É uma boa ideia criar vários modelos de mineração usando diferentes combinações de suporte e probabilidade. Para controlar quais configurações você usou para cada modelo, você pode usar o assistente de **modelo de documento** , disponível no cliente de mineração de dados para Excel, e usar a opção de relatório **detalhado** . Para obter mais informações, consulte [documentando modelos de mineração &#40;suplementos de mineração de dados para Excel&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md).  
  
6.  Opcionalmente, clique em **parâmetros** para alterar os parâmetros do algoritmo e personalizar o comportamento do modelo de mineração.  
  
     A caixa de diálogo Parâmetros de Algoritmo inclui todos os parâmetros que você define no assistente, mais alguns que são usados com menor frequência, como MAXIMUM_SUPPORT. Para obter informações sobre como usar esses parâmetros, consulte [referência técnica do algoritmo de associação da Microsoft](data-mining/microsoft-association-algorithm-technical-reference.md).  
  
7.  Na página **concluir** , digite um nome exclusivo para o conjunto de dados e o modelo.  
  
8.  Em **Opções**, você define como deseja trabalhar com o modelo após sua conclusão:  
  
    -   **Procurar**.  Quando o modelo já estiver criado, o assistente abre uma janela que exibe as regras, os conjuntos de itens e um gráfico de rede de dependências que representa as associações.  
  
         Para obter mais informações sobre como interpretar os dados no Visualizador do modelo de associação, consulte [navegando em um modelo de regras de associação](browsing-an-association-rules-model.md).  
  
    -   **Habilitar detalhamento**. Selecione esta opção para obter acesso aos dados subjacentes, por meio do modelo.  
  
         O detalhamento é útil, por exemplo, se você quiser clicar em um determinado conjunto de itens e ver os dados de origem.  
  
    -   **Use o modelo temporário**. Selecione esta opção se você não quiser que o modelo seja salvo no servidor. Os modelos temporários serão excluídos quando você fechar o Excel.  
  
9. O assistente analisa todas as combinações possíveis e cria um relatório que contém os conjuntos de itens e as regras.  
  
## <a name="more-about-association-models"></a>Mais sobre modelos de associação  
 O algoritmo Regras de Associação da [!INCLUDE[msCoName](../includes/msconame-md.md)] examina os dados de treinamento para encontrar itens que aparecem juntos em uma transação. Cada grupo de itens constitui um *conjunto*. Em seguida, o algoritmo conta o número de vezes que cada conjunto de itens aparece e calcula a importância relativa de cada conjunto de itens em todas as transações.  
  
 O algoritmo usa essas informações sobre conjuntos de itens para gerar regras que podem ser usadas para prever associações ou fazer recomendações. Por exemplo, uma regra pode ser "se o usuário comprou um livro do Autor 1 e um livro do Autor 2, provavelmente também comprará um livro do Autor 3". Cada recomendação recebe uma probabilidade, com base na intensidade das associações.  
  
### <a name="requirements"></a>Requisitos  
 Para usar o assistente para Associação, você deve estar conectado a um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 A fonte de dados deve estar organizada como uma tabela de transação. A fonte de dados deve conter uma coluna com o identificador da transação. Essa coluna identifica cada grupo de itens. Essa coluna de transação deve estar em uma relação um-para-muitos com a segunda coluna, a ID do item, que armazena nomes ou números de ID para os itens individuais no grupo.  
  
 Em tese, isso talvez seja mais fácil entender isso relembrando o exemplo do carrinho de compras. Se o carrinho de compras tiver uma ID, essa ID servirá como identificador da transação. Cada item no carrinho de compras, como batatas ou leite, é membro dessa transação. O algoritmo Associação pode rastrear os itens nas transações: por exemplo, para determinar quantas vezes batatas e leite aparecem em qualquer transação única.  
  
 A fonte de dados deve ser classificada pela coluna de identificador da transação.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um modelo de mineração de dados](creating-a-data-mining-model.md)   
 [Navegando em um modelo de regras de associação](browsing-an-association-rules-model.md)   
 [Análise de cesta de compras &#40;tabela AnalysisTools para Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)   
 [Orientações de diagrama de rede de dependência &#40;suplementos de mineração de dados&#41;](dependency-network-diagram-walkthrough-data-mining-add-ins.md)  
  
  
