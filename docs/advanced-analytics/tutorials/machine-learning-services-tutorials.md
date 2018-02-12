---
title: "Tutoriais de serviços de aprendizado de máquina do SQL Server | Microsoft Docs"
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- Python
- R
ms.assetid: 5ccc75f6-6703-47d9-b879-9a740569b45e
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 2d15f47fd148cb7b1f0edf399e94502c3570eabd
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="tutorials-for-sql-server-machine-learning-services"></a>Tutoriais para serviços de aprendizado de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece uma lista abrangente de aplicativos de exemplo que usam recursos de aprendizado de máquina no SQL Server 2016 ou o SQL Server 2017, tutoriais e demonstrações. Comece aqui saber como otimizar seu código R e Python para um ambiente de produção do SQL, a execução de R ou Python do T-SQL e como usar os contextos de computação local e remoto.

## <a name="start-here"></a>Comece aqui

+ [Tutoriais do Python](../tutorials/sql-server-python-tutorials.md)

+ [Tutoriais de R](../tutorials/sql-server-r-tutorials.md)

Para obter mais informações sobre como configurar e requisitos, consulte [pré-requisitos](#bkmk_prerequisites).

## <a name="samples-and-solutions"></a>Exemplos e soluções

+ [Exemplos](#bkmk_samples) 

    Esses cenários do mundo real da equipe de desenvolvimento do SQL Server demonstram como inserir o aprendizado de máquina em aplicativos. Todos os exemplos incluem o código que você pode baixar, modificar e usar em produção.

+ [Soluções](#bkmk_solutions) 

    Modelos da equipe de ciência de dados da Microsoft são personalizáveis, para começar rapidamente com o aprendizado de máquina. Cada solução é adaptada para um problema específico da tarefa ou do setor. A maioria das soluções é desenvolvida para executar no SQL Server ou em um ambiente de nuvem como o aprendizado de máquina do Azure. Outras soluções podem executar no Linux ou em clusters de Hadoop ou Spark, usando o Microsoft R Server ou o servidor de aprendizado de máquina.

### <a name ="bkmk_samples"></a>Exemplos de produto do SQL Server

Esses exemplos e demonstrações fornecidas pela equipe de desenvolvimento do SQL Server e o R Server realce maneiras que você pode usar a análise incorporada em aplicativos do mundo real.

+ [Executar o cliente clustering usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/)

  Use o aprendizado sem supervisão aos clientes de segmento, com base em dados de vendas. Este exemplo usa o algoritmo rxKmeans escalável do Microsoft R para criar o modelo de clustering. 
  
  Aplica-se a: SQL Server 2016 ou o SQL Server de 2017

+ [NOVO! Executar o cliente clustering usando Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Saiba como usar o algoritmo Kmeans para executar o cluster sem supervisão de clientes. Este exemplo usa o Python idioma no banco de dados.
    
    Aplica-se a: SQL Server de 2017

+ [Criar um modelo de previsão usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

  Saiba como uma empresa de aluguel ski pode usar o aprendizado de máquina para prever locações futuras, que ajuda a equipe e plano de negócios para atender às demandas futuras. Este exemplo usa os algoritmos da Microsoft para criar modelos de árvores de decisão e regressão logística. 
  
  Aplica-se a: SQL Server 2016 ou o SQL Server de 2017

+ [Criar um modelo de previsão usando Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

   Crie o aplicativo de análise de aluguel ski usando Python, para ajudar a planejar demandas futuras. Este exemplo usa a nova biblioteca do Python, **revoscalepy**, para criar um modelo de regressão linear.
   
   Aplica-se a: SQL Server de 2017

+ [Como usar Tableau com serviços de aprendizado de máquina do SQL Server](https://blogs.msdn.microsoft.com/mlserver/2017/12/14/how-to-use-tableau-with-sql-server-machine-learning-services-with-r-and-python/)

    Analisar a mídia social e criar gráficos Tableau, usando o SQL Server e R.

### <a name="bkmk_solutions"></a>Modelos de solução

A equipe de ciência de dados da Microsoft fornece modelos de solução que podem ser usados para impulsionar soluções em cenários comuns. Todo o código é fornecido, junto com instruções sobre como treinar e implantar um modelo de pontuação usando procedimentos armazenados do SQL Server.

+ [Detecção de fraudes](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [Previsão de variação personalizada](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [Manutenção preditiva](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [Prever a duração do hospital de permanência](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

Para obter mais informações, consulte [Modelos de aprendizado de máquina com o SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/).

## <a name="more-resources-and-reading"></a>Mais recursos e leitura

+ [Por que criamos-lo?](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/01/10/sql-server-r-services-why-did-we-build-it/)

    Deseja saber a verdadeira história por trás do R Services? Leia este artigo de desenvolvimento e a equipe de PM que explica a origem e metas do SQL Server R Services.

+ [Tutoriais e dados de exemplo para o Microsoft R](https://docs.microsoft.com/machine-learning-server/r/tutorial-introduction)

    Saiba mais sobre o Microsoft R, e que o pacote RevoScaleR oferece nesta coleção dos tutoriais rápidos. Saiba como escrever código R uma vez e implantar em qualquer lugar, usando o RevoScaleR fontes de dados e contextos de computação remota.

+ [Introdução ao MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)

  Saiba como usar os novos algoritmos no pacote MicrosoftML para modelagem avançada e transformações de dados escalonáveis, otimizadas para vários contextos de computação.

## <a name="bkmk_Prerequisites"></a>Pré-requisitos

Para executar esses tutoriais, você deve baixar e instalar a componentes de aprendizado de máquina do SQL Server, conforme descrito aqui:

+ [Configurar serviços de aprendizado de máquina do SQL Server 2017 ou SQL Server 2016 R Services](../r/set-up-sql-server-r-services-in-database.md)
+ [Configurar os serviços do SQL Server de 2017 Python](../python/setup-python-machine-learning-services.md)

Com o SQL Server 2017, você pode instalar o R ou Python ou ambos. Caso contrário, o processo de instalação, arquitetura e requisitos gerais são as mesmas.

Depois de executar a instalação do SQL Server, não se esqueça destas etapas importantes:

1. Habilitar o recurso de execução do script externo executando `sp_configure 'external scripts enabled', 1`. Siga as instruções para reconfigurar e reinicie o SQL Server.
2. Certifique-se de que o serviço barra inicial está em execução e se as contas de trabalho da barra inicial podem se conectar à instância do SQL Server.
3. Examine as permissões associadas com os usuários que executam scripts de R ou Python. Independentemente de você usar contas de usuário do Windows ou logons do SQL Server, o usuário deve ter permissão para executar scripts R ou Python e deve ser capaz de se conectar à instância. Dependendo do tutorial, o usuário também pode exigir permissão para gravar dados, criar objetos de banco de dados ou fazer uma massa importação de dados.

Para obter detalhes, consulte este artigo para alguns problemas comuns de instalação e configuração: [Solucionando problemas de serviços de aprendizado de máquina](../machine-learning-troubleshooting-faq.md)

> [!NOTE]
> Não é possível executar esses tutoriais usando outra ferramenta de software livre R ou Python. Ambiente de desenvolvimento e o computador do SQL Server com o aprendizado de máquina devem ter os R ou Python bibliotecas fornecidas pela Microsoft, que oferecem suporte à integração com o SQL Server e o uso de contextos de computação remota.
