---
title: Cenários de ciência de dados e modelos de solução
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: cb144eb5c766b417884f6f1adb67dc0ac48504a5
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469773"
---
# <a name="data-science-scenarios-and-solution-templates"></a>Cenários de ciência de dados e modelos de solução
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Os modelos são soluções de exemplo que demonstram as práticas recomendadas e fornecem os blocos de construção para ajudá-lo a implementar uma solução rápida. Cada modelo foi projetado para resolver um problema específico, para uma vertical ou setor específico. As tarefas de cada modelo vão desde a preparação de dados, engenharia de recursos até o treinamento e a pontuação do modelo. Use esses modelos para saber como [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] o funciona. Em seguida, sinta-se à vontade para personalizar o modelo de acordo com seu próprio cenário e criar uma solução personalizada. 

Cada solução inclui dados de exemplo, código R ou código Python e procedimentos armazenados do SQL, se aplicável. O código pode ser executado em seu ambiente de desenvolvimento de R ou Python preferido, com cálculos feitos no SQL Server. Em alguns casos, você pode executar o código diretamente usando o T-SQL e qualquer ferramenta de cliente SQL, como SQL Server Management Studio.

> [!TIP]
> 
> A maioria dos modelos vem em várias versões que dão suporte a plataformas locais e na nuvem para aprendizado de máquina. Por exemplo, você pode criar a solução usando apenas SQL Server ou pode criar a solução em Microsoft R Server ou em Azure Machine Learning.

+ Para obter instruções de download e instalação, consulte [como usar os modelos](#bkmk_HowTo).

## <a name="fraud-detection"></a>Detecção de fraudes

[Modelo de detecção de fraudes online (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**Acontece** A capacidade de detectar transações fraudulentas é importante para empresas online. Para reduzir as perdas de cobrança, as empresas precisam identificar rapidamente as transações feitas usando as credenciais ou instrumentos de pagamento roubado. Quando transações fraudulentas são descobertas, as empresas normalmente tomam medidas para bloquear determinadas contas assim que possível, para evitar um número maior de perdas. Nesse cenário, você aprende a usar dados de transações de compra online para identificar prováveis fraudes.

**Qual**  A detecção de fraudes é resolvida como um problema de classificação binária. A metodologia usada neste modelo pode ser facilmente aplicada à detecção de fraudes em outros domínios.


## <a name="campaign-optimization"></a>Otimização da campanha

[Prever como e quando contatar leads](https://microsoft.github.io/r-server-campaign-optimization/)

**Acontece** Essa solução usa dados do setor de seguros para prever clientes potenciais com base em dados demográficos, históricos de resposta histórica e detalhes específicos do produto.  As recomendações também são geradas para indicar o melhor canal e tempo para abordar os usuários a influenciar o comportamento de compra.

**Qual** A solução cria e compara vários modelos. A solução também demonstra a integração de dados automatizada e a preparação de dados usando procedimentos armazenados. Exemplos paralelos são fornecidos para SQL Server no banco de dados, no Azure e no HDInsight Spark. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>Assistência médica: prever o tempo de permanência no hospital 

[Prevendo o tempo de permanência em hospitais](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**Acontece** Prever com precisão quais pacientes podem exigir hospitalização de longo prazo é uma parte importante do cuidado e do planejamento. Os administradores precisam ser capazes de determinar quais instalações exigem mais recursos, e os profissionais de saúde querem garantir que eles possam atender às necessidades dos pacientes.

**Qual** Essa solução usa o Máquina Virtual de Ciência de Dados e inclui uma instância do SQL Server com o Machine Learning habilitado. Ele também inclui um conjunto de Power BI relatórios que você pode usar para interagir com um modelo implantado.

## <a name="customer-churn"></a>Rotatividade de clientes

[Modelo de previsão de rotatividade de clientes (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**Acontece** Analisar e prever a rotatividade de clientes é importante em qualquer setor em que a perda de clientes para concorrentes deve ser gerenciada e impedida: bancos, telecomunicações e varejo, para citar alguns. O objetivo da análise de variação é identificar quais clientes têm a probabilidade de variação e tomar medidas apropriadas para manter esses clientes e seus negócios.

**Qual** Este modelo Formula o problema de rotatividade como um problema de **classificação binária** . Ele usa dados de exemplo de duas fontes, dados demográficos de clientes e transações de clientes, para classificar os clientes como estando sujeitos a uma variação provável ou improvável.
  
## <a name="predictive-maintenance"></a>Manutenção preditiva

[Modelo de manutenção preditiva (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**Acontece** A manutenção preditiva visa aumentar a eficiência das tarefas de manutenção capturando falhas anteriores e usando essas informações para prever quando ou onde um dispositivo pode falhar. A capacidade de prever a obsolescência do dispositivo é especialmente valiosa para aplicativos que dependem de dados distribuídos ou sensores. Esse método também pode ser aplicado para monitorar ou prever erro em dispositivos IoT (Internet das Coisas).

**Qual** Esta solução se concentra em responder à pergunta "quando uma máquina no serviço falha?" Os dados de entrada representam medidas de sensor simuladas para mecanismos de aeronave. Os dados obtidos do monitoramento das condições de operação atuais do mecanismo, como o ciclo de trabalho atual, as configurações e as medidas do sensor, são usados para criar três tipos de modelos de previsão:

-   **Modelos de regressão**, para prever a duração de um mecanismo antes de sua falha. O modelo de exemplo prevê a métrica "vida útil restante" (RUL), também chamada de "tempo de falha" (TTF).
  
-   **Modelos de classificação**, para prever se um mecanismo tem a probabilidade de falhar.
  
    O **modelo de classificação binária** prevê se um mecanismo falhará em um determinado intervalo de tempo.

    O **modelo de classificação de várias classes** prevê se um mecanismo específico pode falhar e fornece uma janela de tempo provável de falha. Por exemplo, para um dia específico, você pode prever se um dispositivo tem a probabilidade de falhar em determinado dia ou em um período após o dia especificado.

## <a name="energy-demand-forecasting"></a>Previsão de demanda de energia

[Modelo de previsão de demanda de energia com SQL Server R Services](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**O que:** : A previsão de demanda é um problema importante em vários domínios, incluindo energia, varejo e serviços. A previsão de demanda precisa ajuda as empresas a realizar melhor planejamento de produção, alocação de recursos e tomar outras decisões importantes de negócios. No setor de energia, a previsão de demanda é essencial para reduzir o custo de armazenamento de energia e o fornecimento e a demanda de balanceamento.

**Qual** Este modelo usa SQL Server R Services para prever a demanda por eletricidade. O modelo usado para previsão é um modelo de regressão de floresta aleatório baseado em **rxDForest**, um algoritmo de aprendizado de máquina de alto desempenho incluído no Microsoft R Server. A solução inclui um simulador de demanda, todo o código do R e T-SQL necessário para treinar um modelo e procedimentos armazenados que podem ser usados para gerar e relatar as previsões. 


## <a name="bkmk_HowTo"></a>Como usar os modelos

Para baixar os arquivos incluídos em cada modelo, você pode usar comandos do GitHub ou abrir o link e clicar em **Baixar Zip** para salvar todos os arquivos no computador.  Após o download, normalmente, a solução conterá estas pastas:
  
-   **Dados**: Contém os dados de exemplo para cada aplicativo.
  
-   **R**: Contém todo o código de desenvolvimento de R de que você precisa para a solução. A solução exige as bibliotecas fornecidas pelo Microsoft R Server, mas pode ser aberta e editada em qualquer IDE do R. O código do R foi otimizado para que os cálculos sejam feitos “no banco de dados”, definindo o contexto de computação como uma instância do SQL Server.
  
-   **SQLR**: Contém vários arquivos. SQL que podem ser executados em um ambiente SQL, como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , para criar os procedimentos armazenados que executam tarefas relacionadas, como processamento de dados, engenharia de recursos e implantação de modelo.
  
    A pasta também contém um script do PowerShell que pode ser executado para invocar todos os scripts e criar o ambiente de ponta a ponta. Lembre-se de editar o script para se adequar ao seu ambiente.

## <a name="next-steps"></a>Próximas etapas

+ [Tutoriais do SQL Server Machine Learning](machine-learning-services-tutorials.md)




