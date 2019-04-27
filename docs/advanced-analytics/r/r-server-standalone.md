---
title: Instalação Standalone R Server ou Machine Learning Server – serviços do SQL Server Machine Learning
description: Visão geral introdução ao R Server autônomo e Machine Learning Server na instalação do SQL Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: overview
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 47edd434445d57c5ca25373b5dc15fa328f94019
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642593"
---
# <a name="r-server-standalone-and-machine-learning-server-standalone-in-sql-server"></a>R Server (autônomo) e Machine Learning Server (autônomo) no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server fornece suporte à instalação de um R Server autônomo ou Machine Learning Server que é executado independentemente do SQL Server. Dependendo da sua versão do SQL Server, um servidor autônomo tem uma base de R de código-fonte aberto e, possivelmente, Python, sobreposta com bibliotecas de alto desempenho da Microsoft que adicionar a análise preditiva e estatística em grande escala. Bibliotecas também permitem que tarefas de aprendizado de máquina de scripts em R ou Python. 

No SQL Server 2016, esse recurso é chamado **R Server (autônomo)** e é somente para R. No SQL Server 2017, ele é chamado **Machine Learning Server (autônomo)** e inclui o R e Python.  

> [!Note]
> Como instalado pela instalação do SQL Server, um servidor autônomo é funcionalmente equivalente às versões do SQL sem marca [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), os mesmos cenários de usuário, incluindo a execução remota de suporte operacionalização e os serviços web e a coleção completa de bibliotecas de R e Python.

## <a name="components"></a>Componentes

SQL Server 2016 é apenas o R. O SQL Server 2017 oferece suporte às linguagens R e Python. A tabela a seguir descreve os recursos em cada versão.

| Componente | Descrição |
|-----------|-------------|
| Pacotes do R | [**RevoScaleR** ](ref-r-revoscaler.md) é a biblioteca principal para o R escalonável com funções de manipulação de dados, transformação, visualização e análise.  <br/>[**MicrosoftML** ](ref-r-microsoftml.md) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de sentimento, análise de imagem e análise de texto. <br/>[**sqlRUtils** ](ref-r-sqlrutils.md) fornece funções auxiliares para colocar os scripts do R em um procedimento armazenado T-SQL, registrando um procedimento armazenado com um banco de dados e executar o procedimento armazenado de um ambiente de desenvolvimento de R.<br/>[**mrsdeploy** ](operationalization-with-mrsdeploy.md) ofertas da web de implantação do serviço (no SQL Server 2017 somente). <br/>[**olapR** ](ref-r-olapr.md) é para especificar consultas MDX em R.|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open) é a distribuição do código-fonte aberto da Microsoft do R. O pacote e o interpretador são incluídos. Sempre use a versão do MRO agrupado em instalação. |
| Ferramentas do R | Janelas do console de R e prompts de comando são ferramentas padrão em uma distribuição de R. Para encontrá-los em \Program files\Microsoft Server\140\R_SERVER\bin\x64 SQL. |
| Exemplos de R e scripts |  Pacotes de R e RevoScaleR do código-fonte aberto incluem conjuntos de dados internos para que você pode criar e executar o script usando os dados previamente instalados. Examine para que eles \Program files\Microsoft SQL Server\140\R_SERVER\library\datasets e \library\RevoScaleR. |
| Pacotes do Python | [**revoscalepy** ](../python/ref-py-revoscalepy.md) é a biblioteca principal para o Python escalonável com funções de manipulação de dados, transformação, visualização e análise. <br/>[**microsoftml** ](../python/ref-py-microsoftml.md) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de sentimento, análise de imagem e análise de texto.  |
| Ferramentas do Python | A ferramenta de linha de comando interna do Python é útil para testar ad hoc e tarefas. Encontre a ferramenta em \Program files\Microsoft Server\140\PYTHON_SERVER\python.exe SQL. |
| Anaconda | O anaconda é uma distribuição de software livre de Python e pacotes essenciais. |
| Scripts e exemplos de Python | Assim como acontece com R, Python inclui conjuntos de dados internos e scripts. Encontre os dados revoscalepy em \Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data. |
| Modelos previamente treinados em R e Python | Modelos previamente treinados são criados para casos de uso específicos e mantidos pela equipe de engenharia de ciência de dados na Microsoft. Você pode usar os modelos previamente treinados como-é a pontuação de sentimento negativo positivo em texto ou detectar recursos em imagens usando as novas entradas de dados que você fornecer. Modelos previamente treinados são suportados e pode ser usado em um servidor autônomo, mas você não pode instalá-los por meio da instalação do SQL Server. Para obter mais informações, consulte [Install pré-treinado modelos de aprendizado de máquina no SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-a-standalone-server"></a>Usando um servidor autônomo

Normalmente, os desenvolvedores do R e Python escolher um servidor autônomo para ultrapassar as restrições de memória e processamento de software livre R e Python. Bibliotecas de R e Python em execução em um servidor autônomo podem carregar e processar grandes quantidades de dados em vários núcleos e agregar os resultados em uma única saída consolidada. Funções de alto desempenho são projetadas para escala e o utilitário: fornecimento de modelagem estatística, análise preditiva, visualizações de dados e algoritmos em um produto de servidor comercial de aprendizado de máquina de ponta com engenharia e suporte Microsoft.

Como um servidor independente dissociado do SQL Server, o ambiente de R e Python está configurado, protegido e acessados usando o sistema operacional subjacente e ferramentas padrão fornecidas no servidor autônomo, não o SQL Server. Não há nenhum suporte interno para dados relacionais do SQL Server. Se você quiser usar dados do SQL Server, você pode criar objetos de fonte de dados e conexões, como você faria de qualquer cliente.

Como um suplemento do SQL Server, um servidor autônomo também é útil como um ambiente de desenvolvimento avançado se você precisar de computação local e remoto. Os pacotes de R e Python em um servidor autônomo são as mesmas que as fornecidas com uma instalação do mecanismo de banco de dados, permitindo a portabilidade do código e [alternância de contexto de computação](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).

## <a name="how-to-get-started"></a>Como começar

Iniciar com a instalação, anexar os binários a ferramenta de desenvolvimento favorita e escrever seu primeiro script.

### <a name="step-1-install-the-software"></a>Etapa 1: Instalar o software

Instale uma dessas versões:

+ [SQL Server 2017 Machine Learning Server (autônomo)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (autônomo) - R somente](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>Etapa 2: Configurar uma ferramenta de desenvolvimento

Em um servidor autônomo, é comum para trabalhar localmente usando um desenvolvimento instalado no mesmo computador.

+ [Configurar ferramentas R](set-up-a-data-science-client.md)
+ [Configurar ferramentas Python](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>Etapa 3: Escrever seu primeiro script

Escreva script de R ou Python usando funções de RevoScaleR e revoscalepy os algoritmos de aprendizado de máquina.
  
  + [Explorar R e RevoScaleR em 25 funções](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): Comece com os comandos básicos do R e, em seguida, Avançar para as RevoScaleR funções analíticas distribuíveis que proporciona alto desempenho e dimensionamento para soluções de R. Inclui versões paralelizáveis de muitos dos pacotes mais populares de modelagem do R, como clustering k-means, árvores de decisão e florestas de decisão, bem como as ferramentas para a manipulação de dados.

  + [Guia de início rápido: Um exemplo de classificação binária com o pacote do Python microsoftml](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): Crie um modelo de classificação binária usando as funções do microsoftml e o conjunto de dados de câncer de mama bem conhecidos.

Escolha a melhor linguagem para a tarefa. R é melhor para cálculos estatísticos que são difíceis de implementar usando SQL. Para operações baseadas em conjunto em dados, aproveite o poder do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para alcançar desempenho máximo. Use o mecanismo de banco de dados na memória para cálculos muito rápidos nas colunas.

### <a name="step-4-operationalize-your-solution"></a>Etapa 4: Colocar sua solução

Servidores autônomos podem usar o [operacionalização](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) funcionalidade do sem SQL-marca [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server). Você pode configurar um servidor autônomo para operacionalização, que oferece estes benefícios: implantar e hospede seu código, como serviços da web, executados o diagnóstico, capacidade de serviço web de teste.

### <a name="step-5-maintain-your-server"></a>Etapa 5: Manter seu servidor

SQL Server libera atualizações cumulativas regularmente. Aplicar as atualizações cumulativas adiciona aprimoramentos funcionais e segurança a uma instalação existente. 

Descrições das funcionalidades novas ou alteradas podem ser encontradas na [Downloads do CAB](../install/sql-ml-cab-downloads.md) artigo e nas páginas da web para [atualizações cumulativas do SQL Server 2016](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions) e [atualizações cumulativas do SQL Server 2017 ](https://support.microsoft.com/help/4047329). 

Para obter mais informações sobre como aplicar atualizações a uma instância existente, consulte [aplicar as atualizações](../install/sql-machine-learning-standalone-windows-install.md#apply-cu) nas instruções de instalação.

## <a name="see-also"></a>Confira também

 [Instalar o R Server (autônomo) ou Machine Learning Server (autônomo)](../install/sql-machine-learning-standalone-windows-install.md)

