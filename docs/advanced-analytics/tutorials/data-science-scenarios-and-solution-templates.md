---
title: "Cenários de ciência de dados e modelos de solução | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 49e54fa9-9b28-44ba-b256-06dad4e8dece
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dabce30d55a38f4ecd93a88f3cebf01e53a0335e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="data-science-scenarios-and-solution-templates"></a>Cenários de ciência de dados e modelos de solução

Os modelos são soluções de exemplo que demonstram as práticas recomendadas e fornecem os blocos de construção para ajudá-lo a implementar uma solução rápida. Cada modelo é projetado para resolver um problema específico, para um vertical específico ou mercado. As tarefas de cada modelo vão desde a preparação de dados, engenharia de recursos até o treinamento e a pontuação do modelo. Use esses modelos para saber como [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] funciona. Em seguida, fique à vontade para personalizar o modelo para ajustar seu próprio cenário e criar uma solução personalizada. 

Cada solução inclui dados de exemplo, o código de R ou o código Python e procedimentos armazenados do SQL se aplicável. O código pode ser executado em seu ambiente de desenvolvimento R ou Python preferencial, com cálculos feitos no SQL Server. Em alguns casos, você pode executar o código diretamente usando o T-SQL e qualquer ferramenta de cliente SQL, como o SQL Server Management Studio.

> [!TIP]
> 
> A maioria dos modelos são fornecidos em várias versões com suporte no local e na nuvem plataformas para o aprendizado de máquina. Por exemplo, você pode criar a solução usando apenas o SQL Server, ou você pode criar a solução no Microsoft R Server ou no aprendizado de máquina do Azure.

+ Para obter detalhes e atualizações, consulte este lançamento: [excitantes novos modelos no Azure ML](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

+ Para download e instruções de instalação, consulte [como usar os modelos](#bkmk_HowTo).

## <a name="fraud-detection"></a>Detecção de fraudes

[Modelo de detecção de fraudes online (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)

**O que:** a capacidade de detectar transações fraudulentas é importante para empresas online. Para reduzir as perdas de devolução, as empresas precisam identificar rapidamente as transações que foram feitas usando instrumentos de pagamento roubado ou credenciais. Quando transações fraudulentas são descobertas, as empresas normalmente tomam medidas para bloquear determinadas contas assim que possível, para evitar um número maior de perdas. Nesse cenário, você aprenderá como usar dados de transações de compra online para identificar fraude provável.

**Como:** detecção de fraudes é resolvida como um problema de classificação binária. A metodologia usada neste modelo pode ser facilmente aplicada à detecção de fraudes em outros domínios.


## <a name="campaign-optimization"></a>Otimização da campanha

[Prever como e quando entrar em contato com clientes potenciais](https://microsoft.github.io/r-server-campaign-optimization/)

**O que:** esta solução usa dados do setor de seguros para prever os clientes potenciais com base em dados demográficos, dados históricos de resposta e detalhes específicos do produto.  As recomendações são também geradas para indicar os melhores canal e tempo para os usuários a abordagem para influenciar o comportamento de compra.

**Como:** a solução cria e compara vários modelos. A solução também demonstra a integração de dados automatizado e preparação de dados usando procedimentos armazenados. São fornecidas amostras paralelas para SQL Server no banco de dados, no Azure e HDInsight Spark. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>Saúde: prever a duração da permanência na hospital 

[Prever a duração da permanência na hospitais](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**O que:** prever com precisão qual pacientes podem exigir a longo prazo hospitalization é uma parte importante do planejamento e cuidado. Os administradores precisam ser capaz de determinar quais recursos exigem mais recursos e profissionais deseja garantir que eles podem atender às necessidades de pacientes.

**Como:** essa solução utiliza a máquina de Virtual de ciência de dados e inclui uma instância do SQL Server com o aprendizado de máquina habilitado. Ele também inclui um conjunto de relatórios do Power BI que você pode usar para interagir com um modelo implantado.

## <a name="customer-churn"></a>Variação de cliente

[Modelo de previsão de rotatividade de cliente (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)

**O que:** analisando e prevendo a variação do cliente é importante em qualquer setor onde a perda de clientes a concorrência deve ser gerenciada e impediu: transações bancárias, telecomunicações e comercial, para citar alguns. O objetivo da análise de variação é identificar quais clientes têm a probabilidade de variação e tomar medidas apropriadas para manter esses clientes e seus negócios.

**Como:** este modelo Formula o problema de variação como um **classificação binária** problema. Ele usa dados de exemplo de duas fontes, dados demográficos de clientes e transações de clientes, para classificar os clientes como estando sujeitos a uma variação provável ou improvável.
  
## <a name="predictive-maintenance"></a>Manutenção preditiva

[Modelo de previsão de manutenção (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/Introduction.md)

**O que:** manutenção preditiva visa aumentar a eficiência das tarefas de manutenção capturando após falhas e usar essas informações para prever quando e onde um dispositivo pode falhar. A capacidade de previsão obsolescência do dispositivo é especialmente útil para aplicativos que dependem de dados distribuídos ou sensores. Esse método também pode ser aplicado para monitorar ou prever erro em dispositivos IoT (Internet das coisas).

Consulte este anúncio para obter mais informações: [novo modelo de manutenção preditiva](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

**Como:** essa solução enfoca responder a pergunta, "Quando um computador em funcionamento falhará?" Os dados de entrada representam medidas de sensor simuladas para mecanismos de aeronave. Dados obtidos do monitoramento de condições de operação atual do mecanismo, como o ciclo de trabalho atual, as configurações e medidas de sensor, são usados para criar três tipos de modelos de previsão:

-   **Modelos de regressão**, para prever a duração de um mecanismo antes de sua falha. O modelo de exemplo prevê a métrica "Restantes vida útil" (regra), também chamado de "Tempo de falha" (TTF).
  
-   **Modelos de classificação**, para prever se um mecanismo tem a probabilidade de falhar.
  
    O **modelo de classificação binária** prevê se um mecanismo falhará em um determinado intervalo de tempo.

    O **modelo de classificação multiclasse** prevê se um determinado mecanismo falhe e fornece uma janela de tempo provável de falha. Por exemplo, para um dia específico, você pode prever se um dispositivo tem a probabilidade de falhar em determinado dia ou em um período após o dia especificado.

## <a name="energy-demand-forecasting"></a>Previsão de demanda de energia

[Modelo com o SQL Server R Services a previsão de demanda de energia](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**O que:**: previsão de demanda é um problema importante em vários domínios, incluindo serviços, varejo e energia. Previsão de demanda precisa de ajuda as empresas a realizar o melhor planejamento de produção, alocação de recursos e outras decisões de negócios importantes. No setor de energia, é essencial para reduzir o custo de armazenamento de energia e balanceamento de compras e previsão de demanda.

**Como:** este modelo usa o SQL Server R Services para prever a demanda de eletricidade. O modelo usado para previsão é um modelo de regressão de floresta aleatório com base em **rxDForest**, um algoritmo incluído no Microsoft R Server de aprendizado de máquina de alto desempenho. A solução inclui um simulador de demanda, todo o código do R e T-SQL necessário para treinar um modelo e procedimentos armazenados que podem ser usados para gerar e relatar as previsões. 


## <a name="bkmk_HowTo"></a>Como usar os modelos

Para baixar os arquivos incluídos em cada modelo, você pode usar comandos do GitHub ou abrir o link e clicar em **Baixar Zip** para salvar todos os arquivos no computador.  Após o download, normalmente, a solução conterá estas pastas:
  
-   **Dados**: contém os dados de exemplo de cada aplicativo.
  
-   **R**: contém todo o código de desenvolvimento do R necessário para a solução. A solução exige as bibliotecas fornecidas pelo Microsoft R Server, mas pode ser aberta e editada em qualquer IDE do R. O código do R foi otimizado para que os cálculos sejam feitos “no banco de dados”, definindo o contexto de computação como uma instância do SQL Server.
  
-   **SQLR**: contém vários arquivos .sql que podem ser executados em um ambiente SQL como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar procedimentos armazenados que executam tarefas relacionadas, como processamento de dados, engenharia de recursos e implantação de modelo.
  
    A pasta também contém um script do PowerShell que pode ser executado para invocar todos os scripts e criar o ambiente de ponta a ponta. Lembre-se de editar o script para se adequar ao seu ambiente.

## <a name="next-steps"></a>Próximas etapas

+ [Tutoriais de aprendizado de máquina do SQL Server](machine-learning-services-tutorials.md)




