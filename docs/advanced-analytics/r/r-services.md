---
title: "Serviços de aprendizado de máquina do Microsoft | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 341e80f5-3b59-4122-bbaa-969d7904297d
caps.latest.revision: 23
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 246ea9f306c7d99b835c933c9feec695850a861b
ms.openlocfilehash: ddc9b3f17afe1f9d4c811e4a5871f48a3a08de7f
ms.contentlocale: pt-br
ms.lasthandoff: 10/13/2017

---
# <a name="microsoft-machine-learning-services"></a>Serviços de aprendizado de máquina da Microsoft

A meta de serviços de aprendizado de máquina do Microsoft é fornecer uma plataforma extensível e escalonável para a integração de ferramentas e tarefas de aprendizado de máquina com os aplicativos que consomem serviços de aprendizado de máquina. A plataforma deve atender às necessidades de todos os usuários envolvidos no processo de análise e desenvolvimento de dados de cientistas de dados para arquitetos e administradores de banco de dados.

Principais benefícios incluem:

+ Análise de escalonável
+ Várias plataformas e contextos de computação para soluções "escrever uma vez, implante em qualquer lugar"
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
+ **Servidor de aprendizado de máquina do Microsoft** dá suporte a implantações de R e Python em servidores Windows, com a expansão para outras plataformas com suporte planejado para o final de 2017.

### <a name="benefits"></a>Benefícios

Serviços de aprendizado de máquina do Microsoft traz o computação para os dados, permitindo que R ser executado no mesmo computador que o banco de dados. Ele inclui o serviço Launchpad confiável, que é executado fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processar e se comunica com segurança com o tempo de execução de R ou Python.

Usando serviços de aprendizado de máquina do SQL Server, você pode treinar modelos, gerar gráficos, executar pontuação e mover facilmente os dados entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e R ou Python.

Cientistas de dados que estão testando e desenvolvendo soluções podem enviar scripts de um computador de desenvolvimento remoto para executar o código com segurança no servidor, ou eles podem implantar soluções concluídas para o SQL Server, inserindo um código de aprendizado de máquina em procedimentos armazenados do SQL.

Quando você instala o aprendizado de máquina do SQL Server, você obtém uma distribuição de R de software livre ou linguagem Python, bem como as bibliotecas de R e Python escalonáveis fornecidas pela Microsoft. O mecanismo de banco de dados do SQL Server também inclui novos componentes projetados para reforçar a conectividade e mais rápido, garantir uma comunicação mais segura com idiomas externos, como R ou Python.

### <a name="where-to-get-it"></a>Onde obtê-lo

Para começar, consulte estes recursos:

+ [SQL Server R Services](sql-server-r-services.md)
+ [Serviços de Python do SQL Server](../python/sql-server-python-services.md)
+ [Tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md)

> [!NOTE]
> Suporte para Python é fornecido apenas no SQL Server 2017. 

## <a name="machine-learning-server-standalone-and-microsoft-r-server-standalone"></a>Aprendizado de máquina Server (autônomo) e Microsoft R Server (autônomo)

Este sistema de servidor autônomo oferece suporte a soluções R distribuídas e escalonáveis em várias plataformas e usando várias fontes de dados empresariais, como o Linux e HD Insight. Se você não precisa integrar com o SQL Server, você pode instalar o R Server para habilitar o rápido desenvolvimento, implantação e operacionalização de soluções de aprendizado de máquina. Você também pode usar os instaladores de R Server para atualizar os componentes de R associados a uma instância do SQL Server e obter a versão mais recente do R.

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

Quando você cria seu próprio espaço de trabalho no estúdio de aprendizado de máquina do Azure, você terá acesso a mais de 400 pacotes R pré-carregados. Você também pode escolher ao criar uma experiência que usa R, para implantar R usando uma distribuição CRAN R padrão ou Microsoft R Open. Você ainda pode criar seus próprios pacotes de R e carregá-los no Azure para executar como módulos personalizados.

Para obter mais informações, consulte estes recursos:

+ [Estender seu experimento com o R](https://docs.microsoft.com/azure/machine-learning/machine-learning-extend-your-experiment-with-r)
+ [Crie módulos R personalizados no aprendizado de máquina do Azure](https://docs.microsoft.com/azure/machine-learning/machine-learning-custom-r-modules)

Muitos dos algoritmos fornecidos no Azure ML agora estão incluídos nos serviços de aprendizado de máquina do Microsoft, como parte do pacote MicrosoftML. Para obter mais informações, consulte [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package).

O aprendizado de máquina do Azure é outra plataforma conveniente para cientista de dados e os desenvolvedores que precisam criar, treinar e implantar modelos usando serviços Web. Você pode publicar soluções para o [Marketplace do aprendizado de máquina](http://datamarket.azure.com/browse/data?category=machine-learning).

### <a name="data-science-virtual-machines"></a>Máquinas virtuais de ciência de dados

É possível implantar uma versão pré-instalada e pré-configurada do [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] no Microsoft Azure, facilitando a introdução à exploração de dados e modelagem imediatamente na nuvem, sem a necessidade de um sistema local totalmente configurado.

O Azure Marketplace contém várias máquinas virtuais que dão suporte à ciência de dados:

+ A **Máquina Virtual de Ciência de Dados da Microsoft** é configurada com o Microsoft R Server, bem como o Python (distribuição Anaconda), um servidor de bloco de notas Jupyter, o Visual Studio Community Edition, o Power BI Desktop, o SDK do Azure e o SQL Server Express Edition.

+ O**Microsoft R Server 2016 para Linux** contém a última versão do R Server (versão 9.0.1). Máquinas virtuais separadas estão disponíveis para o CentOS versão 7.2 e Ubuntu versão 16.04.

+ O **R Server somente SQL Server 2016 Enterprise** máquina virtual inclui um instalador autônomo para R Server 9.0.1 que suporta o novo modelo de licenciamento do ciclo de vida do Software moderno.

> [!TIP]
> O novo [dados ciência da VM para Windows Server 2016](http://aka.ms/dsvm/win2016) fornece versões GPU de estruturas de aprendizado populares, como CNTK. Ferramentas pré-instalados incluem os drivers de GPU NVIDIA CUDA Toolkit 8.0 e a biblioteca de cuDNN NVIDIA para cargas de trabalho GPU. Em apenas alguns minutos, você pode ter um ambiente completo para a criação de modelos de aprendizado que podem ser executados na CPU ou da CPU e GPU.

## <a name="next-steps"></a>Próximas etapas

[Introdução aos serviços de aprendizado de máquina](getting-started-with-sql-server-r-services.md)

[Guia de Introdução ao servidor de aprendizado de máquina](getting-started-with-microsoft-r-server-standalone.md)

[Instalar o mecanismo de banco de dados do SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md)

