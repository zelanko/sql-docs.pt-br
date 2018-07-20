---
title: SQL Server Machine Learning Server (autônomo) e o R Server (autônomo) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a8cdceabc26c55b6eade57712fa610d3e84808f5
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174783"
---
# <a name="sql-server-machine-learning-server-standalone-and-r-server-standalone"></a>SQL Server Machine Learning Server (autônomo) e o R Server (autônomo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Um servidor autônomo é uma instalação de componentes de aprendizado de máquina, articulada como recursos de R e Python, que são executados independentemente das instâncias do mecanismo de banco de dados do SQL Server. Você pode instalar um servidor autônomo por si só, sem nenhuma dependência do SQL Server. Como um servidor autônomo é independente do SQL Server, configuração e administração de tarefas e ferramentas são mais semelhantes a uma versão de não-SQL do Machine Learning Server, você pode ler sobre [deste artigo](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server).

O objetivo de um servidor de aprendizado de máquina autônomo é fornecer um ambiente de desenvolvimento sofisticado, com processamento paralelo e distribuído de cargas de trabalho de R e Python em pequenas a grandes conjuntos de dados, usando os pacotes de proprietários e os mecanismos de cálculo instalado com o servidor. Os pacotes de R e Python em um servidor autônomo são os mesmos que os fornecidos em uma instalação do SQL Server (no banco de dados), permitindo a portabilidade do código e [alternância de contexto de computação](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).

Os desenvolvedores de motivo principal para escolher que um servidor autônomo do machine learning é se mover além as restrições de memória e processamento de software livre R e Python. Servidores autônomos podem carregar e processar grandes quantidades de dados em vários núcleos e agregar os resultados em uma única saída consolidada. As funções e os algoritmos são projetados para escala e o utilitário: fornecimento de modelagem estatística, análise preditiva, visualizações de dados e algoritmos em um produto de servidor comercial de aprendizado de máquina de ponta com engenharia e suporte Microsoft.

Em geral, é recomendável que você trate (autônomo) e (no banco de dados) instalações como mutuamente exclusivos para evitar a contenção de recursos, mas se você tiver recursos suficientes, há proibição instalar ambos no mesmo computador físico.

Você só pode ter um servidor autônomo no computador: ambos [Machine Learning Server (autônomo) do SQL Server 2017](../install/sql-machine-learning-standalone-windows-install.md) ou [SQL Server 2016 R Server (autônomo)](../install/sql-r-standalone-windows-install.md). Você deve desinstalar manualmente uma versão antes de instalar uma versão diferente.

## <a name="components-of-a-standalone-server"></a>Componentes de um servidor autônomo

SQL Server 2016 é apenas o R. O SQL Server 2017 oferece suporte às linguagens R e Python. A tabela a seguir descreve os recursos em cada versão.

| Componente | Description |
|-----------|-------------|
| Pacotes de R | [RevoScaleR](revoscaler-overview.md) é a biblioteca principal para o R escalonável com funções de manipulação de dados, transformação, visualzation e análise.  <br/>[MicrosoftML (R)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de sentimento, análise de imagem e análise de texto. <br/>[mrsdeploy](operationalization-with-mrsdeploy.md) ofertas da web de implantação do serviço (no SQL Server 2017 somente). <br/>[olapR](how-to-create-mdx-queries-using-olapr.md) é para especificar consultas MDX em R.|
| Microsoft R Open MRO) | [MRO](https://mran.microsoft.com/open) é a distribuição do código-fonte aberto da Microsoft do R. O pacote e o interpretador são incluídos. Sempre use a versão do MRO agrupado em instalação. |
| Ferramentas do R | Janelas do console de R e prompts de comando são ferramentas padrão em uma distribuição de R. Para encontrá-los em \Program files\Microsoft Server\140\R_SERVER\bin\x64 SQL. |
| Exemplos de R e scripts |  Pacotes de R e RevoScaleR do código-fonte aberto incluem conjuntos de dados internos para que você pode criar e executar o script usando os dados previamente instalados. Examine para que eles \Program files\Microsoft SQL Server\140\R_SERVER\library\datasets e \library\RevoScaleR. |
| Pacotes do Python | [revoscalepy](../python/what-is-revoscalepy.md) é a biblioteca principal para o Python e escalonável com funções de manipulação de dados, transformação, visualzation e análise. <br/>[microsoftml (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de sentimento, análise de imagem e análise de texto.  |
| Ferramentas do Python | A ferramenta de linha de comando interna do Python é útil para testar ad hoc e tarefas. Encontre a ferramenta em \Program files\Microsoft Server\140\PYTHON_SERVER\python.exe SQL. |
| Anaconda | O anaconda é uma distribuição de software livre de Python e pacotes essenciais. |
| Scripts e exemplos de Python | Assim como acontece com R, Python inclui conjuntos de dados internos e scripts. Encontre os dados revoscalepy em \Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data. |
| Modelos previamente treinados em R e Python | Modelos previamente treinados são suportados e pode ser usado em um servidor autônomo, mas você não pode instalá-los por meio da instalação do SQL Server. O programa de instalação para o Microsoft Machine Learning Server fornece modelos, que pode ser instalada gratuitamente. Para obter mais informações, consulte [Install pré-treinado modelos de aprendizado de máquina no SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="get-started-step-by-step"></a>Introdução ao passo a passo

Iniciar com a instalação, anexar os binários a ferramenta de desenvolvimento favorita e escrever seu primeiro script.

### <a name="step-1-install-the-software"></a>Etapa 1: Instalar o software

Instale uma dessas versões:

+ [SQL Server 2017 Machine Learning Server (autônomo)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (autônomo) - R somente](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>Etapa 2: Configurar uma ferramenta de desenvolvimento

Configure suas ferramentas de desenvolvimento para usar os binários do Machine Learning Server. Para obter mais informações sobre o Python, consulte [binários Python Link](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools). Para obter instruções sobre como conectar-se no R Studio, consulte [usando diferentes versões do R](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R) e apontar a ferramenta para C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64. Você também pode tentar [ferramentas do R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation). 

### <a name="step-3-write-your-first-script"></a>Etapa 3: Escrever seu primeiro script

Escreva script de R ou Python usando funções de RevoScaleR e revoscalepy os algoritmos de aprendizado de máquina.
  
  + [Explorar R e RevoScaleR em 25 funções](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): iniciar com comandos básicos do R e, em seguida, o andamento para os RevoScaleR funções analíticas distribuíveis que fornecem alto desempenho e escala para soluções de R. Inclui versões paralelizáveis de muitos dos pacotes mais populares de modelagem do R, como clustering k-means, árvores de decisão e florestas de decisão, bem como as ferramentas para a manipulação de dados.

  + [Guia de início rápido: Um exemplo de classificação binária com o pacote do Python microsoftml](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): criar um modelo de classificação binária usando as funções do microsoftml e o conjunto de dados de câncer de mama bem conhecidos.

Escolha a melhor linguagem para a tarefa. R é melhor para cálculos estatísticos que são difíceis de implementar usando SQL. Para operações baseadas em conjunto em dados, aproveite o poder do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para alcançar desempenho máximo. Use o mecanismo de banco de dados na memória para cálculos muito rápidos nas colunas.

### <a name="step-4-operationalize-your-solution"></a>Etapa 4: Colocar sua solução

Servidores autônomos podem usar o [operacionalização](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) funcionalidade do sem SQL-marca [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). Você pode configurar um servidor autônomo para operacionalização, que oferece estes benefícios: implantar e hospede seu código, como serviços da web, executados o diagnóstico, capacidade de serviço web de teste.

## <a name="see-also"></a>Confira também

 [(No banco de dados) de serviços de aprendizado de máquina do SQL Server](sql-server-r-services.md)

