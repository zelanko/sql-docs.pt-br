---
title: "Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados
Neste passo a passo, você vai desenvolver uma solução de ponta a ponta para modelagem preditiva usando o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
Este passo a passo baseia-se em um conjunto de dados público conhecido, o conjunto de dados de táxi de Nova York. Você usará uma combinação de código do R, dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e funções SQL personalizadas para criar um modelo de classificação que indica a probabilidade de o motorista receber uma gorjeta em uma corrida de táxi específica. Você também vai implantar seu modelo do R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usar dados do servidor para gerar pontuações com base no modelo.  
  
Este exemplo foi escolhido porque é possível ser estendido facilmente para todas as espécies de problemas reais, como prever as respostas dos clientes a campanhas de vendas ou prever gastos dos visitantes em eventos. Como o modelo pode ser invocado por meio de um procedimento armazenado, você pode inseri-lo facilmente em um aplicativo.  
  
**Público-alvo**  
  
Este passo a passo é destinado a desenvolvedores do R. Você também deverá estar um pouco familiarizado com as operações básicas de banco de dados, como criar bancos de dados, criar tabelas, importar dados em tabelas e consultar as tabelas usando o [!INCLUDE[tsql](../../includes/tsql-md.md)].  Você receberá os scripts SQL e do R para execução.  
  
Se você não estiver familiarizado com o R, mas tiver um bom conhecimento de bancos de dados, este tutorial fornecerá uma introdução à forma como o R pode ser integrado em fluxos de trabalho empresariais com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Nenhuma codificação em R é necessária; todos os scripts são fornecidos. Você precisa ter alguma espécie de IDE do R instalada para executar os comandos.  
  
**Pré-requisitos**  
  
Para seguir este tutorial, você deve ter acesso a uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] instalado. Para o ambiente local, prepare uma estação de trabalho de ciência de dados que pode se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e instale as bibliotecas do R necessárias.  
  
Para obter mais informações, consulte [Pré-requisitos para o passo a passo da ciência de dados #40;SQL Server R Services&#41;](../../advanced-analytics/r-services/prerequisites-for-data-science-walkthroughs-sql-server-r-services.md).  
  
## <a name="overview"></a>Visão geral  
Este passo a passo ilustra uma solução típica de ponta a ponta para análise avançada. Você precisa concluir as lições na ordem.  
  
||Tempo estimado para concluir|  
|-|------------------------------|  
|[Lição 1: Preparar os dados &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)<br /><br />O processo analítico começa com a obtenção dos dados usados para criar um modelo. Você baixará um conjunto de dados público e o salvará em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|30 minutos|  
|[Lição 2: Exibir e explorar os dados &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)<br /><br />Geralmente, um cientista de dados gasta um tempo considerável explorando os dados e preparando-os para modelagem, criando novos recursos ou transformando os dados, conforme necessário.  Você usará o SQL e o R para explorar os dados e gerar resumos.|20 minutos|  
|[Lição 3: Criar recursos de dados &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)<br /><br />Você criará novos recursos de dados usando funções personalizadas no R e no [!INCLUDE[tsql](../../includes/tsql-md.md)].|10 minutos|  
|[Lição 4: Criar e salvar o modelo &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)<br /><br />Quando os dados estiverem prontos, o cientista de dados treinará e ajustará o modelo, avaliando seu desempenho e testando parâmetros diferentes. Neste passo a passo, você criará um modelo de classificação e usará os dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para gerar previsões. Você também plotará a precisão do modelo usando o R.|15 minutos|  
|[Lição 5: Implantar e usar o modelo &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough.md)<br /><br />Por fim, você implantará o modelo em produção, salvando-o em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e chamará o modelo por meio de um procedimento armazenado para gerar previsões.|10 minutos|  
  
## <a name="notes"></a>Observações  
Como o passo a passo foi projetado para apresentar o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]aos desenvolvedores do R, o maior número possível de ações são executadas com o R. Isso não significa que o R seja necessariamente a melhor ferramenta para cada tarefa. Em muitos casos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá fornecer um desempenho melhor, especialmente para tarefas como agregação de dados e engenharia de recursos. Essas tarefas podem se beneficiar particularmente dos novos recursos do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], como índices columnstore com otimização de memória.  
  
## <a name="next-step"></a>Próxima etapa  
[Lição 1: Preparar os dados &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
