---
title: "Guia de Introdução ao aprendizado de máquina no SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 11/09/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: b61de3dcbe239ec1bffdabc734e8e5d624519df6
ms.sourcegitcommit: ec5f7a945b9fff390422d5c4c138ca82194c3a3b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2017
---
# <a name="getting-started-with-machine-learning-in-sql-server"></a>Guia de Introdução ao aprendizado de máquina no SQL Server

Microsoft fornece um conjunto integrado, escalonável e de soluções de aprendizado de máquina para o local e a nuvem:

+ **Integrado**, pois você pode executar R ou Python no SQL Server. Isso lhe permite facilmente dos processos de mesclagem enterprise para ETL e relatórios com dados de tarefas de ciência de como o recurso de engenharia, criação de modelo e pontuação.
+ **Escalonável**, pois o cientista de dados pode desenvolver e testar uma solução em um laptop e, em seguida, implantá-la em várias plataformas para distribuídas ou o processamento paralelo de operações de chave, como modelo de treinamento e pontuação. Plataformas com suporte incluem o SQL Server no Windows, Hadoop e Spark.

Este artigo fornece links para recursos de cada produto na plataforma Microsoft Machine Learning.

## <a name="machine-learning-in-sql-server"></a>No SQL Server de aprendizado de máquina

+ SQL Server 2017

  A partir do SQL Server 2017, agora você pode usar código Python no SQL Server. Para refletir o suporte mais amplo para soluções de vários idiomas (com o mais em breve!) e o nome foi alterado para [!INCLUDE[rsql-productnamenew-md](../includes/rsql-productnamenew-md.md)]. Agora você pode automatizar tarefas de aprendizado de máquina usando ferramentas SQL para executar código R ou Python. Ou, use o computador do SQL Server como o _contexto de computação_ para trabalhos iniciados a partir de um ambiente de desenvolvimento remoto.

    + [Visão geral da arquitetura de Python no SQL Server](/python/architecture-overview-sql-server-python.md)
    + [Configurar o SQL Server R Services ou serviços de aprendizado de máquina](../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

+ SQL Server 2016

  SQL Server 2016 dá suporte a execução de código R usando procedimentos armazenados do SQL Server. Isso facilita automatizar tarefas de aprendizado de máquina usando ferramentas SQL. Ou, você pode executar código R de um laptop remoto ou o ambiente de desenvolvimento de R, ao usar o computador do SQL Server como o _contexto de computação_.

  Essa integração oferece segurança para seus dados e permite gerenciar e equilibrar os recursos usados por R.

    + [Guia de Introdução wth SQL Server R Services](r/getting-started-with-sql-server-r-services.md)
    + [Configurar o SQL Server R Services ou serviços de aprendizado de máquina](../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

## <a name="microsoft-machine-learning-server-microsoft-r-server"></a>Microsoft R (servidor) de aprendizado de máquina do Microsoft

A opção de instalar [!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)] é fornecido no SQL Server 2017 para dar suporte a clientes corporativos que desejam executar trabalhos de aprendizado de máquina distribuída e escalonável, mas que não precisam de integração com o mecanismo de banco de dados do SQL Server, como o uso de computação do SQL contextos.

No SQL Server 2016, use a opção para instalar o [!INCLUDE[rsql-platform-md](../includes/rsql-platformnew-md.md)].
  
  + [Bem-vindo ao servidor de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)
  
Você também pode instalar [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)] ou [!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)] por meio de instaladores específico da plataforma:

  + [Instalar no Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
  + [Instalar no Linux](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-linux-install)
  + [Instalar no Hadoop](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-hadoop-install)

> [!IMPORTANT]
> Se você deseja executar Python usando R Server, certifique-se de instalar a versão mais recente, [!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)], que está disponível apenas por meio de [!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)] instalação:
> 
>    + [Configurar o Microsoft R Server ou o servidor de aprendizado de máquina](../advanced-analytics/r/create-a-standalone-r-server.md)

## <a name="related-products"></a>Produtos relacionados

+ [Configurar um cliente de ciência de dados](../advanced-analytics/r/set-up-a-data-science-client.md)

  Se você já instalou um a produtos de servidor de aprendizado de máquina, este artigo fornece informações sobre como configurar um computador separado para desenvolvimento e teste de soluções, incluindo ferramentas e bibliotecas necessárias.

+ [Máquinas virtuais de ciência de dados](../advanced-analytics/r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

  Impulsione sua entrada fazendo com que essa solução do Azure Marketplace de aprendizado de máquina completa de aprendizado de máquina. A máquina virtual de ciência de dados (frequentemente abreviada para "DSVM") inclui o SQL Server, Microsoft Server de aprendizado de máquina e todas as ferramentas de desenvolvimento.
  
  A versão mais recente da máquina Virtual de ciência de dados (DSVM) é executado no Windows 2016 Preview Edition, para fornecer a aparência de limpeza personalizável do Windows 10. Ela vem pré-configurada com drivers NVIDIA, CUDA Toolkit 8.0 e a biblioteca de cuDNN NVIDIA para cargas de trabalho GPU.

## <a name="resources-for-learning"></a>Recursos de aprendizagem

+ [Tutoriais de aprendizado de máquina](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)

  Comece aqui obter uma lista de todos os recursos de aprendizagem sobre soluções de aprendizado de máquina usando [!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)] ou [!INCLUDE[sssql15-md](../includes/sssql15-md.md)].

### <a name="r-tutorials"></a>Tutoriais de R

+ [Tutoriais do SQL Server R](../advanced-analytics/tutorials/sql-server-r-tutorials.md)

   Saiba como executar R no SQL Server, criar e usar contextos de computação remota ou executar simulações em R usando o SQL Server.
   
   Inclui tutoriais "todo o código fornecido" para que você possa executar uma solução completa de R no SQL Server Management Studio, sem abrir uma IDE de R!

+ [Explorar o R e ScaleR em 25 funções curtas](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

   Você é novo no R? Se perguntando como Microsoft R (ou RevoScaleR) se compara ao R padrão? Consulte esses início rápido para R Server.

### <a name="python-tutorials"></a>Tutoriais do Python

+ [Tutoriais do SQL Server Python](../advanced-analytics/tutorials/sql-server-r-tutorials.md)

  Saiba como executar Python [!INCLUDE[ssnoversion](../includes/ssnoversion.md)]. Criar um modelo usando Python e usá-lo para classificar os dados do SQL Server.

   Uma solução de ponta a ponta para desenvolvedores em SQL fornece todo o código que você precisa executar Python no SQL Server Management Studio.

+ [Publicar e consumir o código Python](../advanced-analytics/python/publish-consume-python-code.md)

  Este passo a passo vem com todos os códigos necessários para implantar um modelo em um serviço web usando o servidor de aprendizado de máquina.

### <a name="product-samples-with-code"></a>Exemplos de produto com o código

Essas soluções da equipe de desenvolvimento do SQL Server executada em R ou Python e demonstram cenários comuns para a integração de aprendizado de máquina com aplicativos de negócios.

+ [Compilar um aplicativo inteligente com o SQL Server e R](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

+ [Criar um aplicativo inteligente com o SQL Server e Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

### <a name="data-science-solution-templates"></a>Modelos de solução de ciência de dados

Os modelos de solução da equipe do Microsoft ciência de dados representam soluções de exemplo completo adaptados para áreas específicas ou cenários. Eles se destinam para servir como blocos de construção para ajudá-lo a implementar uma solução rápida ou para demonstrar as práticas recomendadas. Cada modelo inclui dados de exemplo e código personalizável.

+ [Modelos de solução](../advanced-analytics/tutorials/data-science-scenarios-and-solution-templates.md)

## <a name="next-steps"></a>Próximas etapas

[Introdução ao serviços de aprendizado de máquina do SQL Server](../advanced-analytics/r/getting-started-with-sql-server-r-services.md)

[Introdução ao servidor de aprendizado de máquina da Microsoft](../advanced-analytics/r/getting-started-with-microsoft-r-server-standalone.md)
