---
title: "Tutoriais de aprendizado de máquina do SQL Server | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- Python
ms.assetid: 5ccc75f6-6703-47d9-b879-9a740569b45e
caps.latest.revision: 32
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0ebeae12d6987154baa7ccb7c9417e9f92b2bbe0
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-machine-learning-tutorials"></a>Tutoriais de aprendizado de máquina do SQL Server

Este artigo fornece uma lista abrangente de aplicativos de exemplo que usam recursos de aprendizado de máquina no SQL Server 2016 ou o SQL Server 2017, tutoriais e demonstrações. Comece aqui aprender a executar R ou Python do T-SQL, usar os contextos de computação local e remoto e otimizar seu código R e Python para um ambiente de produção do SQL.

## <a name="start-here"></a>Comece aqui

+ [Tutoriais do Python](../tutorials/sql-server-python-tutorials.md)

+ [Tutoriais de R](../tutorials/sql-server-r-tutorials.md)

Para obter mais informações sobre como configurar e requisitos, consulte [pré-requisitos](#bkmk_prerequisites).

## <a name="samples-and-solutions"></a>Exemplos e soluções

+ [Exemplos](#bkmk_samples) 

    Esses cenários do mundo real da equipe de desenvolvimento do SQL Server demonstram como inserir o aprendizado de máquina em aplicativos. Todos os exemplos incluem o código que você pode baixar, modificar e usar em produção.

+ [Soluções](#bkmk_solutions) 

    Modelos da equipe de ciência de dados da Microsoft são personalizáveis, para começar rapidamente com o aprendizado de máquina. Cada solução personalizada para uma tarefa específica ou um problema de setor; Além disso, a maioria das soluções são projetados para ser executado no SQL Server ou em um ambiente de nuvem como o aprendizado de máquina do Azure. Outra solução pode executar em clusters Microsoft R Server ou HDI Spark.

### <a name ="bkmk_samples"></a>Exemplos de produto do SQL Server

Esses exemplos e demonstrações fornecidas pela equipe de desenvolvimento do SQL Server e o R Server realce maneiras que você pode usar a análise incorporada em aplicativos do mundo real.

+ [Executar o cliente clustering usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/)

  Use o aprendizado sem supervisão aos clientes de segmento, com base em dados de vendas. Este exemplo usa o algoritmo rxKmeans escalável do Microsoft R para criar o modelo de clustering. 
  
  Aplica-se a: SQL Server 2016 ou o SQL Server de 2017

+ [NOVO! Executar o cliente clustering usando Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Saiba como usar o algoritmo Kmeans para executar o cluster sem supervisão de clientes. Este exemplo usa o Python idioma no banco de dados. 
    
    Aplica-se a: SQL Server de 2017

+ [Criar um modelo de previsão usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

  Saiba como uma empresa de aluguel ski pode usar o aprendizado de máquina para prever locações futuras, que ajuda a equipe e plano de negócios para atender às demandas futuras. Este exemplo usa os algoritmos Microsoft R para criar um modelo de árvores de decisão e regressão logística. 
  
  Aplica-se a: SQL Server 2016 ou o SQL Server de 2017

+ [Criar um modelo de previsão usando Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

   Crie o aplicativo de análise de aluguel ski usando Python, para ajudar a planejar demandas futuras. Este exemplo usa a nova biblioteca do Python, **revoscalepy**, para criar um modelo de regressão linear. 
   
   Aplica-se a: SQL Server de 2017

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

+ [Tutoriais e dados de exemplo para o Microsoft R](https://docs.microsoft.com/r-server/r/tutorial-introduction)

    Saiba mais sobre o Microsoft R, e que o pacote RevoScaleR oferece nesta coleção dos tutoriais rápidos. Saiba como escrever código R uma vez e implantar em qualquer lugar, usando o RevoScaleR fontes de dados e contextos de computação remota.

+ [Introdução ao MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

  Saiba como usar os novos algoritmos no pacote MicrosoftML para modelagem avançada e transformações de dados escalonáveis, otimizadas para vários contextos de computação.

## <a name="bkmk_Prerequisites"></a>Pré-requisitos

Para executar esses tutoriais, você deve baixar e instalar a componentes de aprendizado de máquina do SQL Server, conforme descrito aqui:

+ [Configurar o SQL Server R Services](../r/set-up-sql-server-r-services-in-database.md)
+ [Configurar os serviços do SQL Server Python](../python/setup-python-machine-learning-services.md)

Com o SQL Server 2017, você pode instalar o R ou Python ou ambos. Caso contrário, o processo de instalação, arquitetura e requisitos gerais são as mesmas.

Depois de executar a instalação do SQL Server, não se esqueça destas etapas importantes:

1. Habilitar o recurso de execução do script externo executando `sp_configure 'external scripts enabled', 1`. Siga as instruções para reconfigurar e reinicie o SQL Server.
2. Certifique-se de que o serviço Launchpad é executado e que o trabalhador contas ele usa podem se conectar à instância do SQL Server.
3. Examine as permissões associadas a contas de usuário do Windows que serão executados scripts de R ou Python e logons do SQL Server. Todos os precisam de permissão para executar scripts R ou Python e para conectar-se à instância. Dependendo do exemplo, eles também talvez precise de permissões para ler e gravar dados e criar objetos de banco de dados.

Para obter detalhes, consulte este artigo para alguns problemas comuns de instalação e configuração: [Solucionando problemas de serviços de aprendizado de máquina](../machine-learning-troubleshooting-faq.md)

> [!NOTE]
> Não é possível executar esses tutoriais usando outra ferramenta de software livre R ou Python. Ambiente de desenvolvimento e o computador do SQL Server com o aprendizado de máquina devem ter os R ou Python bibliotecas fornecidas pela Microsoft, que oferecem suporte à integração com o SQL Server e o uso de contextos de computação remota.

