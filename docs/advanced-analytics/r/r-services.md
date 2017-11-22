---
title: "Serviços de aprendizado de máquina do Microsoft | Microsoft Docs"
ms.date: 11/09/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 341e80f5-3b59-4122-bbaa-969d7904297d
caps.latest.revision: "23"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9735d257ce81e5b84ea19eeb70be8bef21127c13
ms.sourcegitcommit: ec5f7a945b9fff390422d5c4c138ca82194c3a3b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2017
---
# <a name="microsoft-machine-learning-services"></a>Serviços de aprendizado de máquina da Microsoft

A meta de serviços de aprendizado de máquina do Microsoft é fornecer uma plataforma extensível e escalonável para a integração de ferramentas e tarefas de aprendizado de máquina com os aplicativos que consomem serviços de aprendizado de máquina. A plataforma deve atender às necessidades de todos os usuários envolvidos no processo de análise e desenvolvimento de dados de cientistas de dados para arquitetos e administradores de banco de dados.

Principais benefícios incluem:

+ Análise de escalonável
+ Várias plataformas e contextos de computação para soluções de "código de uma vez, implante em qualquer lugar"
+ Evita a movimentação de dados e o risco de dados, fazendo com que a análise para os dados
+ Os cientistas de dados podem escolher suas próprias ferramentas e linguagens
+ Integra as melhores funcionalidades de código-fonte aberto com os recursos corporativos da Microsoft
+ Administração simplificada
+ Fácil de implantar e consumir os modelos de previsão

## <a name="in-database-analytics-with-sql-server"></a>Análise de no banco de dados com o SQL Server

No SQL Server 2016, a Microsoft lançou duas plataformas de servidor para integrar a linguagem R de código aberto popular com aplicativos de negócios:

+ **SQL Server R Services (no Banco de Dados)**, para integração ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
+ **Microsoft R Server**, para implantações de R de nível corporativo em servidores Windows e Linux

No SQL Server de 2017, o nome tem foi alterado para refletir o suporte para a linguagem Python popular.

+ **Serviços de aprendizado de máquina do SQL Server (no banco de dados)** dá suporte a R e Python para análise no banco de dados.
+ **Servidor de aprendizado de máquina do Microsoft** dá suporte a implantações de R e Python em clusters do Windows, Linux e HDInsight Spark e Hadoop.

### <a name="benefits"></a>Benefícios

Serviços de aprendizado de máquina do Microsoft traz o computação para os dados, permitindo que R ser executado no mesmo computador que o banco de dados. Ele inclui o serviço barra inicial, que é executado fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processar e se comunica com segurança com o tempo de execução de R ou Python.

Usando serviços de aprendizado de máquina do SQL Server, você pode treinar modelos, gerar gráficos, executar pontuação e mover com segurança os dados entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e R ou Python.

Cientistas de dados que estão testando e desenvolvendo soluções podem enviar scripts de um computador de desenvolvimento remoto e executar seu código no servidor sem mover os dados. Os desenvolvedores podem implantar soluções concluídas para o SQL Server, inserindo um código de aprendizado de máquina em procedimentos armazenados do SQL.

Quando você instala o aprendizado de máquina do SQL Server, você obtém uma distribuição de R de software livre ou linguagem Python, bem como as bibliotecas de R e Python escalonáveis fornecidas pela Microsoft. O mecanismo de banco de dados do SQL Server também inclui novos componentes projetados para reforçar a conectividade e mais rápido, garantir uma comunicação mais segura com idiomas externos, como R ou Python.

### <a name="where-to-get-it"></a>Onde obtê-lo

Para começar, consulte estes recursos:

+ [SQL Server R Services](sql-server-r-services.md)
+ [Serviços de Python do SQL Server](../python/sql-server-python-services.md)
+ [Tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md)

> [!NOTE]
> Suporte para Python é fornecido apenas no SQL Server 2017. 

## <a name="machine-learning-server-standalone-and-microsoft-r-server-standalone"></a>Aprendizado de máquina Server (autônomo) e Microsoft R Server (autônomo)

Este sistema de servidor autônomo oferece suporte a soluções R distribuídas e escalonáveis em várias plataformas e usando várias fontes de dados empresariais, como o Linux e HDInsight. Se você não precisa integrar com o SQL Server, você pode instalar o R Server para habilitar o rápido desenvolvimento, implantação e operacionalização de soluções de aprendizado de máquina. Você também pode usar os instaladores de R Server para atualizar os componentes de R associados a uma instância do SQL Server e obter a versão mais recente do R.

Se você instalar o Microsoft Server de aprendizado de máquina usando a instalação do SQL Server 2017, você também pode implantar e consumir aplicativos Python.

Para obter mais informações, consulte [Microsoft Server de aprendizado de máquina](https://docs.microsoft.com/r-server/index).

## <a name="related-technologies"></a>Tecnologias relacionadas

Microsoft fornece amplo suporte para ecossistemas de aprendizado de máquina, incluindo ferramentas, provedores, pacotes aprimorados de R e Python, um desenvolvimento em nuvem e plataforma de serviços e um ambiente de desenvolvimento integrado.

### <a name="r-tools-for-visual-studio"></a>Ferramentas de R para o Visual Studio

O Visual Studio fornece um ambiente de desenvolvimento completo para a linguagem R. O plug-in inclui editor, janela interativa, plotagem, depurador e muito mais. Você pode usar linguagens .NET de R ou invocar R do .NET por meio de bibliotecas de software livre, como R.NET e rClr.

Visual Studio também tem um ambiente de desenvolvimento do Python excelente. Não há nenhuma maneira mais fácil de trabalhar com idiomas de aprendizado de máquina sem deixar de aproveitar o acesso a ferramentas de desenvolvimento de banco de dados do SQL.

Para obter mais informações, consulte:

+ [Ferramentas de R para o Visual Studio](https://www.visualstudio.com/vs/rtvs/)
+ [Python - Visual Studio](https://www.visualstudio.com/vs/python/)

### <a name="azure-machine-learning"></a>Aprendizado de máquina do Azure

Quando você cria seu próprio espaço de trabalho no estúdio de aprendizado de máquina do Azure, você tem acesso a mais de 400 pacotes R pré-carregados. Você também pode escolher ao criar uma experiência que usa R, para implantar R usando uma distribuição CRAN R padrão ou Microsoft R Open. Você ainda pode criar seus próprios pacotes de R e carregá-los no Azure para executar como módulos personalizados.

Muitos dos algoritmos fornecidos no Azure ML agora estão incluídos nos serviços de aprendizado de máquina do Microsoft, como parte do pacote MicrosoftML. Para obter mais informações, consulte [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package).

O aprendizado de máquina do Azure é outra plataforma conveniente para cientista de dados e os desenvolvedores que precisam criar, treinar e implantar modelos usando serviços Web. Você pode publicar soluções para o [Marketplace do aprendizado de máquina](http://datamarket.azure.com/browse/data?category=machine-learning).

Para obter mais informações sobre as coisas interessantes alterações no serviço de aprendizado de máquina do Azure, para dar suporte a cientistas de dados profissionais, consulte estes recursos:

+ [O que é o aprendizado de máquina do Azure?](https://docs.microsoft.com/azure/machine-learning/preview/overview-what-is-azure-ml)
+ [Recursos de gerenciamento de modelo](https://docs.microsoft.com/azure/machine-learning/preview/model-management-overview)

### <a name="data-science-virtual-machines"></a>Máquinas virtuais de ciência de dados

É possível implantar uma versão pré-instalada e pré-configurada do [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] no Microsoft Azure, facilitando a introdução à exploração de dados e modelagem imediatamente na nuvem, sem a necessidade de um sistema local totalmente configurado.

O Azure Marketplace contém várias máquinas virtuais que oferecem suporte a ciência de dados.

+ O **máquina de Virtual de ciência de dados do Microsoft** está configurado com o servidor de aprendizado de máquina, bem como Python (distribuição Anaconda), um servidor de notebook Jupyter, Visual Studio Community Edition, Power BI Desktop, SDK do Azure e SQL Servidor.

    O novo [dados ciência da VM para Windows Server 2016](http://aka.ms/dsvm/win2016) fornece versões GPU de estruturas de aprendizado populares, como CNTK. Ferramentas pré-instalados incluem os drivers de GPU NVIDIA CUDA Toolkit 8.0 e a biblioteca de cuDNN NVIDIA para cargas de trabalho GPU. Em apenas alguns minutos, você pode ter um ambiente completo para a criação de modelos de aprendizado que podem ser executados na CPU ou da CPU e GPU.

+ R Server ou servidor de aprendizado de máquina, recomendamos a Microsoft Machine Learning servidor 2017 para Linux ou Windows Server de 2016.

+ Para obter uma imagem do Azure com o aprendizado de máquina do SQL Server, recomendamos que qualquer uma das ofertas de máquina virtual incluem **SQL Server 2017**. Quando você seleciona a imagem, siga as recomendações adicionais sobre o nível de serviço e de camada, para garantir que a VM pode oferecer suporte a cargas de trabalho de aprendizado de máquina.

## <a name="next-steps"></a>Próximas etapas

[Introdução aos serviços de aprendizado de máquina](getting-started-with-sql-server-r-services.md)

[Guia de Introdução ao servidor de aprendizado de máquina](getting-started-with-microsoft-r-server-standalone.md)

[Instalar o mecanismo de banco de dados do SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md)
