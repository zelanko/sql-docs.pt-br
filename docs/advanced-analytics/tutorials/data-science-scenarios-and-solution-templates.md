---
title: Cenários de ciência de dados e modelos de solução – Machine Learning do SQL Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1c98f6110aa6cc0bbb86f04a685211d7dc58447a
ms.sourcegitcommit: 671370ec2d49ed0159a418b9c9ac56acf43249ad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2019
ms.locfileid: "58072150"
---
# <a name="data-science-scenarios-and-solution-templates"></a>Cenários de ciência de dados e modelos de solução
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Os modelos são soluções de exemplo que demonstram as práticas recomendadas e fornecem os blocos de construção para ajudá-lo a implementar uma solução rápida. Cada modelo é projetado para resolver um problema específico, para um vertical específico ou do setor. As tarefas de cada modelo vão desde a preparação de dados, engenharia de recursos até o treinamento e a pontuação do modelo. Use esses modelos para saber como [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] funciona. Em seguida, fique à vontade para personalizar o modelo para ajustar seu cenário e criar uma solução personalizada. 

Cada solução inclui dados de exemplo, o código R ou o código do Python e procedimentos armazenados do SQL se aplicável. O código pode ser executado no ambiente de desenvolvimento preferido R ou Python, com cálculos feitos no SQL Server. Em alguns casos, você pode executar o código diretamente usando o T-SQL e qualquer ferramenta de cliente SQL, como SQL Server Management Studio.

> [!TIP]
> 
> A maioria dos modelos são fornecidos em várias versões que dão suporte a ambos os locais e plataformas para o machine learning na nuvem. Por exemplo, você pode criar a solução usando somente o SQL Server, ou você pode compilar a solução no Microsoft R Server ou no Azure Machine Learning.

+ Para obter detalhes e atualizações, consulte este anúncio: [Novos modelos no Azure ML](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

+ Para o download e instruções de instalação, consulte [como usar os modelos](#bkmk_HowTo).

## <a name="fraud-detection"></a>Detecção de fraudes

[Modelo de detecção de fraudes online (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**O que:** A capacidade de detectar transações fraudulentas é importante para empresas online. Para reduzir as perdas de devolução, as empresas precisam identificar rapidamente as transações feitas usando o instrumentos de pagamento roubados ou credenciais. Quando transações fraudulentas são descobertas, as empresas normalmente tomam medidas para bloquear determinadas contas assim que possível, para evitar um número maior de perdas. Nesse cenário, você aprenderá como usar dados de transações de compra online para identificar possíveis fraudes.

**Como:**  A detecção de fraudes é resolvida como um problema de classificação binária. A metodologia usada neste modelo pode ser facilmente aplicada à detecção de fraudes em outros domínios.


## <a name="campaign-optimization"></a>Otimização de campanha

[Prever como e quando entrar em contato com clientes potenciais](https://microsoft.github.io/r-server-campaign-optimization/)

**O que:** Essa solução usa dados de setor de seguros para prever os clientes potenciais com base em dados demográficos, dados históricos de resposta e detalhes específicos do produto.  As recomendações também são geradas para indicar o melhor canal e o tempo para os usuários de abordagem para influenciar o comportamento de compra.

**Como:** A solução cria e compara vários modelos. A solução também demonstra a integração de dados automatizada e preparação de dados usando procedimentos armazenados. São fornecidas amostras paralelas para o SQL Server no banco de dados, no Azure e o HDInsight Spark. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>Saúde: prever a duração da permanência em hospital 

[Previsão da duração da permanência em hospitais](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**O que:** Prever com precisão os pacientes podem exigir hospitalização a longo prazo é uma parte importante do planejamento e cuidado. Os administradores precisam ser capaz de determinar quais instalações exigem mais recursos, e deseja que os profissionais de saúde garantir que eles podem atender às necessidades de pacientes.

**Como:** Essa solução usa a máquina Virtual de ciência de dados e inclui uma instância do SQL Server com o machine learning habilitada. Ele também inclui um conjunto de relatórios do Power BI que você pode usar para interagir com um modelo implantado.

## <a name="customer-churn"></a>Rotatividade de clientes

[Modelo de previsão de variação de cliente (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**O que:** Analisar e prever a rotatividade de clientes é importante em qualquer setor em que a perda de clientes para concorrentes deve ser gerenciada e impediu: serviços bancários, telecomunicações e varejo, para citar alguns. O objetivo da análise de variação é identificar quais clientes têm a probabilidade de variação e tomar medidas apropriadas para manter esses clientes e seus negócios.

**Como:** Este modelo Formula o problema de variação como um **classificação binária** problema. Ele usa dados de exemplo de duas fontes, dados demográficos de clientes e transações de clientes, para classificar os clientes como estando sujeitos a uma variação provável ou improvável.
  
## <a name="predictive-maintenance"></a>Manutenção preditiva

[Modelo de manutenção preditiva (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**O que:** Manutenção preditiva tem como objetivo aumentar a eficiência das tarefas de manutenção capturando falhas passadas e usar essas informações para prever quando ou onde um dispositivo poderá falhar. A capacidade de prever a obsolescência do dispositivo é especialmente importante para aplicativos que dependem de dados distribuídos ou sensores. Esse método também pode ser aplicado para monitorar ou prever o erro em dispositivos IoT (Internet das coisas).

Consulte este anúncio para obter mais informações: [Novo modelo de manutenção preditiva](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

**Como:** Essa solução se concentra em responder à pergunta, "Quando um computador em serviço falhará?" Os dados de entrada representam medidas de sensor simuladas para mecanismos de aeronave. Dados obtidos do monitoramento de condições de operação atual do mecanismo, como o ciclo de trabalho atual, as configurações e medidas de sensor, são usados para criar três tipos de modelos de previsão:

-   **Modelos de regressão**, para prever a duração de um mecanismo antes de sua falha. O modelo de exemplo prevê a métrica "restantes" RUL (vida útil), também chamado de "tempo para" Falha (TTF).
  
-   **Modelos de classificação**, para prever se um mecanismo tem a probabilidade de falhar.
  
    O **modelo de classificação binária** prevê se um mecanismo falhará em um determinado intervalo de tempo.

    O **modelo de classificação multiclasse** prevê se determinado mecanismo poderá falhar e fornece uma janela de tempo provável da falha. Por exemplo, para um dia específico, você pode prever se um dispositivo tem a probabilidade de falhar em determinado dia ou em um período após o dia especificado.

## <a name="energy-demand-forecasting"></a>Previsão de demanda de energia

[Modelo com o SQL Server R Services de previsão de demanda de energia](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**O que:**: Previsão de demanda é um problema importante em vários domínios, incluindo serviços, varejo e energia. Previsão de demanda precisa de ajuda as empresas a conduzir um melhor planejamento de produção, alocação de recursos e tomar outras decisões de negócios importantes. No setor de energia, é essencial para reduzir o custo de armazenamento de energia e balanceamento de demanda e fornecimento de previsão de demanda.

**Como:** Este modelo usa o SQL Server R Services para prever a demanda de energia elétrica. O modelo usado para previsão é um modelo de regressão de floresta aleatória com base em **rxDForest**, uma incluídos no Microsoft R Server do algoritmo de aprendizado de máquina de alto desempenho. A solução inclui um simulador de demanda, todo o código do R e T-SQL necessário para treinar um modelo e procedimentos armazenados que podem ser usados para gerar e relatar as previsões. 


## <a name="bkmk_HowTo"></a>Como usar os modelos

Para baixar os arquivos incluídos em cada modelo, você pode usar comandos do GitHub ou abrir o link e clicar em **Baixar Zip** para salvar todos os arquivos no computador.  Após o download, normalmente, a solução conterá estas pastas:
  
-   **Dados**: Contém os dados de exemplo para cada aplicativo.
  
-   **R**: Contém todo o código de desenvolvimento de R que necessários para a solução. A solução exige as bibliotecas fornecidas pelo Microsoft R Server, mas pode ser aberta e editada em qualquer IDE do R. O código do R foi otimizado para que os cálculos sejam feitos “no banco de dados”, definindo o contexto de computação como uma instância do SQL Server.
  
-   **SQLR**: Contém vários arquivos. SQL que podem ser executados em um ambiente SQL como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar os procedimentos armazenados que executam tarefas relacionadas, como processamento de dados, engenharia de recursos e implantação de modelo.
  
    A pasta também contém um script do PowerShell que pode ser executado para invocar todos os scripts e criar o ambiente de ponta a ponta. Lembre-se de editar o script para se adequar ao seu ambiente.

## <a name="next-steps"></a>Próximas etapas

+ [Tutoriais de aprendizado de máquina do SQL Server](machine-learning-services-tutorials.md)




