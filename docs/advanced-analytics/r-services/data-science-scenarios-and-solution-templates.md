---
title: "Cen&#225;rios de ci&#234;ncia de dados e modelos da solu&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "04/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 49e54fa9-9b28-44ba-b256-06dad4e8dece
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# Cen&#225;rios de ci&#234;ncia de dados e modelos da solu&#231;&#227;o
Os modelos são soluções de exemplo que demonstram as práticas recomendadas e fornecem os blocos de construção para ajudá-lo a implementar uma solução rápida. Cada modelo foi desenvolvido para resolver um problema específico e inclui dados de exemplo, código do R (Microsoft R Server) e procedimentos armazenados do SQL. As tarefas de cada modelo vão desde a preparação de dados, engenharia de recursos até o treinamento e a pontuação do modelo. O código pode ser executado em um IDE do R, com cálculos feitos no SQL Server, ou usando uma ferramenta cliente do SQL, como SQL Server Management Studio.  
  
Você pode usar esses modelos para saber como o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] funciona, criar e implantar sua própria solução personalizando o modelo para que ele se ajuste ao seu cenário.  
  
Para obter o download e instruções de instalação, consulte [Como usar os modelos](#bkmk_HowTo) ao final deste tópico.  
  
## Detecção de fraudes  
[Modelo de detecção de fraudes online (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)  
  
Uma das tarefas importantes de empresas online é detectar transações fraudulentas e identificar as transações feitas por instrumentos ou credenciais de pagamento roubados, a fim de reduzir perdas de encargo retroativo. Quando transações fraudulentas são descobertas, as empresas normalmente tomam medidas para bloquear determinadas contas assim que possível, para evitar um número maior de perdas. Neste cenário, você aprenderá a usar dados de transações de compra online para identificar possíveis fraudes. Esta metodologia pode ser aplicada facilmente à detecção de fraudes em outros domínios.  
  
Neste modelo, você aprenderá a usar dados de transações de compra online para identificar possíveis fraudes. A detecção de fraudes é resolvida como um problema de classificação binária. A metodologia usada neste modelo pode ser facilmente aplicada à detecção de fraudes em outros domínios.    
  
## Variação de cliente  
[Modelo de previsão de variação de cliente (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)  
  
É importante analisar e prever a variação de cliente em qualquer setor no qual seja necessário gerenciar e impedir a perda de clientes para concorrentes: serviços bancários, telecomunicações e varejo, para citar alguns. O objetivo da análise de variação é identificar quais clientes têm a probabilidade de variação e tomar medidas apropriadas para manter esses clientes e seus negócios.  
  
Este modelo o ajudará na prevenção de variação com a formulação do problema de variação como um problema de **classificação binária**. Ele usa dados de exemplo de duas fontes, dados demográficos de clientes e transações de clientes, para classificar os clientes como estando sujeitos a uma variação provável ou improvável.   
  
## Manutenção preditiva  
[Modelo de manutenção preditiva (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/Introduction.md)  
  
O objetivo da manutenção preditiva “controlada por dados” é aumentar a eficiência das tarefas de manutenção capturando falhas passadas e usar essas informações para prever quando ou onde um dispositivo poderá falhar. A capacidade de prever a obsolescência do dispositivo é particularmente importante para aplicativos que dependem de dados distribuídos ou sensores, como exemplificado pela IoT (Internet das Coisas).  
  
Esse modelo se concentra em responder à pergunta: “Quando um computador em serviço falhará?” Os dados de entrada representam medidas de sensor simuladas para mecanismos de aeronave. Os dados obtidos do monitoramento das condições de operação atuais do mecanismo, como o ciclo de trabalho atual, as configurações, as medidas de sensor e assim por diante, são usadas para criar três tipos de modelos preditivos:  
  
-   **Modelos de regressão**, para prever a duração de um mecanismo antes de sua falha. O modelo de exemplo prevê a métrica RUL (Vida Útil Restante), também chamada de TTF (Tempo de Falha).  
  
-   **Modelos de classificação**, para prever se um mecanismo tem a probabilidade de falhar.  
  
    O **modelo de classificação binária** prevê se um mecanismo falhará em determinado período (número de dias).  
  
    O **modelo de classificação de várias classes** prevê se determinado mecanismo falhará, e se ele falhar, fornecerá uma janela de tempo provável da falha. Por exemplo, para um dia específico, você pode prever se um dispositivo tem a probabilidade de falhar em determinado dia ou em um período após o dia especificado.  
      
      
## Previsão de demanda de energia  
[Modelo de previsão de demanda de energia com o SQL Server R Services](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast_Template_with_SQL-Server-R-Services-1)  
  
Este modelo demonstra como usar o SQL Server R Services para prever a demanda de energia elétrica. A solução inclui um simulador de demanda, todo o código do R e T-SQL necessário para treinar um modelo e procedimentos armazenados que podem ser usados para gerar e relatar as previsões.   
  
## <a name="bkmk_HowTo"></a>Como usar os modelos  
Para baixar os arquivos incluídos em cada modelo, você pode usar comandos do GitHub ou abrir o link e clicar em **Baixar Zip** para salvar todos os arquivos no computador.  Após o download, normalmente, a solução conterá estas pastas:  
  
-   **Dados**: contém os dados de exemplo de cada aplicativo.  
  
-   **R**: contém todo o código de desenvolvimento do R necessário para a solução. A solução exige as bibliotecas fornecidas pelo Microsoft R Server, mas pode ser aberta e editada em qualquer IDE do R. O código do R foi otimizado para que os cálculos sejam feitos “no banco de dados”, definindo o contexto de computação como uma instância do SQL Server.  
  
-   **SQLR**: contém vários arquivos .sql que podem ser executados em um ambiente SQL como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar procedimentos armazenados que executam tarefas relacionadas, como processamento de dados, engenharia de recursos e implantação de modelo.  
  
    A pasta também contém um script do PowerShell que pode ser executado para invocar todos os scripts e criar o ambiente de ponta a ponta.  
  
    Lembre-se de editar o script para se adequar ao seu ambiente.  
  
  
## Consulte também  
[Tutoriais do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
[Comunicando os modelos no Azure ML](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)  
[Novo modelo de manutenção preditiva](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)  
  
  
  
