---
title: "O servidor de aprendizado de máquina do SQL Server (autônomo) e R Server (autônomo) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
vms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: eb30dbfdfd03f5a6515d0559d7f60cdde7b9223c
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/21/2018
---
# <a name="sql-server-machine-learning-server-standalone-and-r-server-standalone"></a>O servidor de aprendizado de máquina do SQL Server (autônomo) e R Server (autônomo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Um servidor autônomo é uma instalação de componentes de aprendizado de máquina, articulada como recursos de R e Python, que são executados independentemente das instâncias de mecanismo de banco de dados do SQL Server. Você pode instalar um servidor autônomo por si só, sem nenhuma dependência no SQL Server. Como um servidor autônomo é independente do SQL Server, configuração e tarefas de administração e ferramentas são mais semelhantes a uma versão de não-SQL do servidor de aprendizado de máquina, que você pode ler sobre [neste artigo](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server).

O objetivo de um servidor de aprendizado de máquina autônomo é proporcionar um ambiente de desenvolvimento sofisticado, com processamento paralelo e distribuído de cargas de trabalho de R e Python em pequenas a grandes conjuntos de dados, usando os pacotes proprietários e os mecanismos de cálculo instalado com o servidor. Os pacotes de R e Python em um servidor autônomo são os mesmos fornecido em uma instalação do SQL Server (no banco de dados), permitindo a portabilidade de código e [alternância de contexto de computação](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).

Os desenvolvedores de motivo principal escolham que um servidor de aprendizado de máquina autônomo é mover além as restrições de memória e processamento de R de código-fonte aberto e Python. Servidores autônomos podem carregar e processar grandes quantidades de dados em vários núcleos e agregar os resultados em uma única saída consolidada. As funções e os algoritmos são projetados para escala e o utilitário: entregar análise preditiva, modelo estatístico, visualizações de dados e algoritmos em um produto de servidor comercial de aprendizado de máquina de ponta engenharia e suporte Microsoft.

Em geral, recomendamos que você trate (autônomo) e (no banco de dados) instalações como mutuamente exclusivos para evitar contenção de recursos, mas se houver recursos suficientes, há proibição instalando-no mesmo computador físico.

Você só pode ter um servidor autônomo no computador: o [servidor do aprendizado de máquina 2017 SQL Server (autônomo)](../install/sql-machine-learning-standalone-windows-install.md) ou [servidor do SQL Server 2016 R (autônomo)](../install/sql-r-standalone-windows-install.md). Você deve desinstalar manualmente uma versão antes de instalar uma versão diferente.

## <a name="components-of-a-standalone-server"></a>Componentes de um servidor autônomo

SQL Server 2016 é R somente. O SQL Server 2017 oferece suporte às linguagens R e Python. A tabela a seguir descreve os recursos em cada versão.

| Componente | Description |
|-----------|-------------|
| Pacotes de R | [RevoScaleR](revoscaler-overview.md) é a biblioteca principal para R escalonável com funções de manipulação de dados, transformação, visualzation e análise.  <br/>[MicrosoftML (R)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) adiciona algoritmos de aprendizagem de máquina para criar modelos personalizados para análise de sentimento, análise de imagem e análise de texto. <br/>[mrsdeploy](operationalization-with-mrsdeploy.md) ofertas da web de implantação do serviço (no SQL Server de 2017 somente). <br/>[olapR](how-to-create-mdx-queries-using-olapr.md) é para especificar consultas MDX em R.|
| Microsoft R Open (MRO) | [MRO](https://mran.microsoft.com/open) é a distribuição de código-fonte aberto da Microsoft de R. O pacote e o interpretador são incluídos. Sempre use a versão do MRO incluído na instalação. |
| Ferramentas de R | Janelas do console de R e prompts de comando são ferramentas padrão em uma distribuição de R. Encontrá-los no \Program files\Microsoft Server\140\R_SERVER\bin\x64 SQL. |
| Exemplos de R e scripts |  Pacotes de R e o RevoScaleR do código-fonte aberto incluem conjuntos de dados internos para que você pode criar e executar o script usando dados previamente instalados. Procure-los no \Program files\Microsoft SQL Server\140\R_SERVER\library\datasets e \library\RevoScaleR. |
| Pacotes do Python | [revoscalepy](../python/what-is-revoscalepy.md) é a biblioteca principal para Python e escalonável com funções de manipulação de dados, transformação, visualzation e análise. <br/>[microsoftml (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) adiciona algoritmos de aprendizagem de máquina para criar modelos personalizados para análise de sentimento, análise de imagem e análise de texto.  |
| Ferramentas do Python | A ferramenta de linha de comando interna do Python é útil para teste ad hoc e tarefas. Localize a ferramenta em \Program files\Microsoft Server\140\PYTHON_SERVER\python.exe SQL. |
| Anaconda | Anaconda é uma distribuição de software livre de Python e pacotes essenciais. |
| Exemplos de Python e scripts | Assim como R, Python inclui conjuntos de dados internos e scripts. Localize os dados revoscalepy em \Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site de packages\revoscalepy\data\sample de dados. |
| Modelos previamente treinados em R e Python | Modelos previamente treinados são com suporte e pode ser usado em um servidor autônomo, mas não é possível instalá-los por meio de instalação do SQL Server. O programa de instalação para o servidor de aprendizado de máquina do Microsoft fornece os modelos, que você pode instalar gratuitamente. Para obter mais informações, consulte [instalação classificação modelos de aprendizado de máquina no SQL Server](install-pretrained-models-sql-server.md). |

## <a name="get-started-step-by-step"></a>Introdução passo a passo

Iniciar a instalação, anexar os binários a ferramenta de desenvolvimento favorita e criar o primeiro script.

### <a name="step-1-install-the-software"></a>Etapa 1: Instalar o software

Instale qualquer uma dessas versões:

+ [Servidor do aprendizado de máquina 2017 SQL Server (autônomo)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (autônomo) - R somente](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>Etapa 2: Configurar uma ferramenta de desenvolvimento

Configure as ferramentas de desenvolvimento para usar os binários do servidor de aprendizado de máquina. Para obter mais informações sobre o Python, consulte [binários de Python de Link](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools). Para obter instruções sobre como conectar-se no Studio R, consulte [usando diferentes versões de R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R) e a ferramenta para C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64. Você também pode tentar [ferramentas R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation). 

### <a name="step-3-write-your-first-script"></a>Etapa 3: Criar o script primeiro

Crie script de R ou Python usando funções de RevoScaleR, revoscalepy e a algoritmos de aprendizado de máquina.
  
  + [Explorar o R e o RevoScaleR em 25 funções](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): iniciar com comandos básicos do R e, em seguida, progresso para as funções de analíticos distribuíveis RevoScaleR que fornecem alto desempenho e escalabilidade para soluções de R. Inclui versões paralelizáveis de muitos dos pacotes mais populares de modelagem do R, como clustering k-means, árvores de decisão e florestas de decisão, bem como as ferramentas para a manipulação de dados.

  + [Início rápido: Um exemplo de classificação binária com o pacote do Python microsoftml](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): criar um modelo de classificação binária usando as funções de microsoftml e o conjunto de dados de câncer de mama bem conhecidos.

Escolha a melhor linguagem para a tarefa. R é melhor para cálculos estatísticos que são difíceis de implementar usando SQL. Para operações baseadas em conjunto de dados, aproveite a potência do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para alcançar desempenho máximo. Use o mecanismo de banco de dados na memória para cálculos muito rápidos sobre colunas.

### <a name="step-4-operationalize-your-solution"></a>Etapa 4: Colocar sua solução

Servidores autônomos podem usar o [operacionalização](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) funcionalidade do sem SQL-marca [Microsoft Server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). Você pode configurar um servidor autônomo para operacionalização, que oferece esses benefícios: implantar e hospedar seu código, como serviços web, executados o diagnóstico, teste a capacidade de serviço da web.

## <a name="see-also"></a>Consulte também

 [Serviços (no banco de dados) de aprendizado de máquina do SQL Server](sql-server-r-services.md)

