---
title: Modelos de solução de ciência de dados
description: Este artigo descreve modelos específicos do setor que demonstram as melhores práticas e fornecem os blocos de construção para ajudar você a implementar uma solução de machine learning.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 241affaea232fcc916456b96ff724655b9289618
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178826"
---
# <a name="data-science-scenarios-and-solution-templates"></a>Cenários de ciência de dados e modelos de solução
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este artigo descreve uma série de modelos de solução de machine learning do SQL Server. Esses modelos demonstram as práticas recomendadas e fornecem os blocos de construção para ajudar você a implementar uma solução de machine learning rapidamente. Cada modelo foi projetado para resolver um problema de ciência de dados específico, para um vertical ou um setor específico.
As tarefas de cada modelo vão desde a preparação de dados, engenharia de recursos até o treinamento e a pontuação do modelo. 

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Use esses modelos para saber como funciona o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Em seguida, sinta-se à vontade para personalizar o modelo de acordo com seu próprio cenário e criar uma solução personalizada.
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Use esses modelos para saber como os serviços de Machine Learning do SQL Server funcionam. Em seguida, sinta-se à vontade para personalizar o modelo de acordo com seu próprio cenário e criar uma solução personalizada.
::: moniker-end

Cada solução inclui dados de exemplo, código R ou código Python e procedimentos armazenados SQL, se aplicável. O código pode ser executado em seu ambiente de desenvolvimento preferido do R ou do Python, com os cálculos feitos no SQL Server. Em alguns casos, você pode executar o código diretamente usando o T-SQL e qualquer ferramenta de cliente do SQL, como o SQL Server Management Studio.

> [!TIP]
> 
> A maioria dos modelos é fornecida em várias versões que dão suporte a plataformas locais e na nuvem para aprendizado de máquina. Por exemplo, você pode criar a solução usando só o SQL Server ou criar a solução no Microsoft R Server ou no Azure Machine Learning.

+ Para obter instruções de download e instalação, confira [Como usar os modelos](#bkmk_HowTo).

## <a name="fraud-detection"></a>Detecção de fraude

[Modelo de detecção de fraudes online (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**O que:** A capacidade de detectar transações fraudulentas é importante para empresas online. Para reduzir as perdas referentes a estornos, as empresas precisam identificar rapidamente as transações feitas usando credenciais ou formas de pagamento roubadas. Quando transações fraudulentas são descobertas, as empresas normalmente tomam medidas para bloquear determinadas contas assim que possível, para evitar um número maior de perdas. Neste cenário, você aprenderá a usar dados de transações de compra online para identificar possíveis fraudes.

**Como:**  A detecção de fraudes é resolvida como um problema de classificação binária. A metodologia usada neste modelo pode ser facilmente aplicada à detecção de fraudes em outros domínios.


## <a name="campaign-optimization"></a>Otimização da campanha

[Prever como e quando contatar clientes potenciais](https://microsoft.github.io/r-server-campaign-optimization/)

**O que:** Esta solução usa dados do setor de seguros para prever clientes potenciais com base em dados demográficos, dados históricos de resposta e detalhes específicos do produto.  As recomendações também são geradas para indicar o melhor canal e horário para abordar os usuários a fim de influenciar o comportamento de compra.

**Como:** A solução cria e compara vários modelos. A solução também demonstra a integração de dados automatizada e a preparação de dados usando procedimentos armazenados. As amostras paralelas são fornecidas para o SQL Server no banco de dados, no Azure e no HDInsight Spark. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>Serviços de saúde: prever o tempo de permanência no hospital 

[Como prever o tempo de permanência em hospitais](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**O que:** Prever com precisão quais pacientes podem exigir hospitalização de longo prazo é uma parte importante do cuidado e do planejamento. Os administradores precisam conseguir determinar quais instalações exigem mais recursos e os cuidadores desejam garantir que possam atender às necessidades dos pacientes.

**Como:** Essa solução usa a Máquina Virtual de Ciência de Dados e inclui uma instância do SQL Server com o aprendizado de máquina habilitado. Também inclui um conjunto de relatórios do Power BI que pode ser usado para interagir com um modelo implantado.

## <a name="customer-churn"></a>Rotatividade de clientes

[Modelo de previsão de rotatividade de clientes (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**O que:** É importante analisar e prever a rotatividade de clientes em qualquer setor no qual seja necessário gerenciar e impedir a perda de clientes para concorrentes: serviços bancários, telecomunicações e varejo, para citar alguns. O objetivo da análise de variação é identificar quais clientes têm a probabilidade de variação e tomar medidas apropriadas para manter esses clientes e seus negócios.

**Como:** Este modelo formula o problema de rotatividade como um **problema de classificação binária**. Ele usa dados de exemplo de duas fontes, dados demográficos de clientes e transações de clientes, para classificar os clientes como estando sujeitos a uma variação provável ou improvável.
  
## <a name="predictive-maintenance"></a>Manutenção preditiva

[Modelo de manutenção preditiva (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**O que:** A manutenção preditiva tem como objetivo aumentar a eficiência das tarefas de manutenção capturando falhas passadas e usar essas informações para prever quando ou onde um dispositivo poderá falhar. A capacidade de prever a obsolescência do dispositivo é especialmente útil para aplicativos que dependem de dados distribuídos ou sensores. Este método também pode ser aplicado para monitorar ou prever erros em dispositivos IoT (Internet das Coisas).

**Como:** Esta solução se concentra em responder à pergunta "Quando um computador em serviço falhará?" Os dados de entrada representam medidas de sensor simuladas para mecanismos de aeronave. Os dados obtidos do monitoramento das condições de operação atuais do mecanismo, como ciclo de trabalho atual, configurações e medidas de sensor, são usados para criar três tipos de modelos preditivos:

-   **Modelos de regressão**, para prever a duração de um mecanismo antes de sua falha. O modelo de exemplo prevê a métrica RUL ("Vida Útil Restante"), também chamada de TTF ("Tempo até a Falha").
  
-   **Modelos de classificação**, para prever se um mecanismo tem a probabilidade de falhar.
  
    O **modelo de classificação binária** prevê se um mecanismo falhará em determinado período.

    O **modelo de classificação de várias classes** prevê se determinado mecanismo falhará e fornece uma janela de tempo provável da falha. Por exemplo, para um dia específico, você pode prever se um dispositivo tem a probabilidade de falhar em determinado dia ou em um período após o dia especificado.

## <a name="energy-demand-forecasting"></a>Previsão de demanda de energia

[Modelo de previsão de demanda de energia com o SQL Server R Services](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**O que:** A previsão de demanda é um problema importante em vários domínios, incluindo energia, varejo e serviços. Uma previsão de demanda precisa ajuda as empresas a realizar melhor o planejamento de produção, a alocação de recurso e tomar outras decisões empresariais importantes. No setor de energia, a previsão de demanda é crítica para reduzir o custo de armazenamento de energia e balancear o fornecimento e a demanda.

**Como:** Este modelo usa o SQL Server R Services para prever a demanda por eletricidade. O modelo usado para previsão é um modelo de regressão de floresta aleatória baseado em **rxDForest**, um algoritmo de aprendizado de máquina de alto desempenho incluído no Microsoft R Server. A solução inclui um simulador de demanda, todo o código do R e T-SQL necessário para treinar um modelo e procedimentos armazenados que podem ser usados para gerar e relatar as previsões. 


## <a name="how-to-use-the-templates"></a><a name="bkmk_HowTo"></a>Como usar os modelos

Para baixar os arquivos incluídos em cada modelo, você pode usar comandos do GitHub ou abrir o link e clicar em **Baixar Zip** para salvar todos os arquivos no computador.  Após o download, normalmente, a solução conterá estas pastas:
  
-   **Dados**: Contém os dados de exemplo de cada aplicativo.
  
-   **R**: Contém todo o código de desenvolvimento do R necessário para a solução. A solução exige as bibliotecas fornecidas pelo Microsoft R Server, mas pode ser aberta e editada em qualquer IDE do R. O código do R foi otimizado para que os cálculos sejam feitos “no banco de dados”, definindo o contexto de computação como uma instância do SQL Server.
  
-   **SQLR**: Contém vários arquivos .sql que podem ser executados em um ambiente SQL, como o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], para criar procedimentos armazenados que executam tarefas relacionadas, como processamento de dados, engenharia de recursos e implantação de modelo.
  
    A pasta também contém um script do PowerShell que pode ser executado para invocar todos os scripts e criar o ambiente de ponta a ponta. Lembre-se de editar o script para se adequar ao seu ambiente.

## <a name="next-steps"></a>Próximas etapas

+ [Tutoriais do Python](sql-server-python-tutorials.md)
+ [Tutoriais do R](sql-server-r-tutorials.md)