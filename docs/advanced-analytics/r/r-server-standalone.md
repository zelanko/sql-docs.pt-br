---
title: Instalação autônoma do R Server ou do Machine Learning Server
description: Visão geral da introdução ao R Server e Machine Learning Server autônomos na instalação do SQL Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: overview
author: dphansen
ms.author: davidph
ms.openlocfilehash: f50049b1b93068748da84342d68ab6cb319c5d98
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344892"
---
# <a name="r-server-standalone-and-machine-learning-server-standalone-in-sql-server"></a>R Server (autônomo) e Machine Learning Server (autônomo) no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server fornece suporte à instalação para um servidor R ou Machine Learning Server autônomo que é executado independentemente do SQL Server. Dependendo de sua versão do SQL Server, um servidor autônomo tem uma base de R de software livre e, possivelmente, Python, sobreposto com bibliotecas de alto desempenho da Microsoft que adicionam análise estatística e preditiva em escala. As bibliotecas também habilitam tarefas de aprendizado de máquina com script em R ou Python. 

No SQL Server 2016, esse recurso é chamado de **r Server (autônomo)** e é somente R. No SQL Server 2017, ele é chamado de **Machine Learning Server (autônomo)** e inclui R e Python.  

> [!Note]
> Conforme instalado pela instalação do SQL Server, um servidor autônomo é funcionalmente equivalente às versões sem marca SQL do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), dando suporte aos mesmos cenários de usuário, incluindo execução remota, operacionalização e Web serviços e a coleção completa de bibliotecas de R e Python.

## <a name="components"></a>Componentes

SQL Server 2016 é somente R. O SQL Server 2017 oferece suporte às linguagens R e Python. A tabela a seguir descreve os recursos em cada versão.

| Componente | Descrição |
|-----------|-------------|
| Pacotes do R | [**RevoScaleR**](ref-r-revoscaler.md) é a biblioteca principal para R escalonável com funções para manipulação, transformação, visualização e análise de dados.  <br/>O [**MicrosoftML**](ref-r-microsoftml.md) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de texto, análise de imagem e análise de sentimentos. <br/>o [**sqlRUtils**](ref-r-sqlrutils.md) fornece funções auxiliares para colocar scripts R em um procedimento armazenado T-SQL, registrar um procedimento armazenado com um banco de dados e executar o procedimento armazenado de um ambiente de desenvolvimento de R.<br/>o [**mrsdeploy**](operationalization-with-mrsdeploy.md) oferece implantação de serviço Web (somente no SQL Server 2017). <br/>[**olapr**](ref-r-olapr.md) é para especificar consultas MDX em R.|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open) é a distribuição de R de código aberto da Microsoft. O pacote e o intérprete estão incluídos. Sempre use a versão do MRO agrupada na instalação. |
| Ferramentas de R | As janelas do console R e os prompts de comando são ferramentas padrão em uma distribuição do R. Encontre-os em \Program files\Microsoft SQL Server\140\R_SERVER\bin\x64. |
| Scripts e exemplos de R |  Os pacotes R e RevoScaleR de software livre incluem conjuntos de dados internos para que você possa criar e executar scripts usando dados pré-instalados. Procure por eles em \Program files\Microsoft SQL Server\140\R_SERVER\library\datasets e \library\RevoScaleR. |
| Pacotes do Python | [**revoscalepy**](../python/ref-py-revoscalepy.md) é a biblioteca principal para Python escalonável com funções para manipulação, transformação, visualização e análise de dados. <br/>o [**microsoftml**](../python/ref-py-microsoftml.md) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de texto, análise de imagem e análise de sentimentos.  |
| Ferramentas Python | A ferramenta de linha de comando interna do Python é útil para tarefas e testes ad hoc. Encontre a ferramenta em \Program files\Microsoft SQL Server\140\PYTHON_SERVER\python.exe. |
| Anaconda | O Anaconda é uma distribuição de software livre de pacotes do Python e essenciais. |
| Exemplos e scripts do Python | Assim como acontece com o R, o Python inclui conjuntos de dados internos e scripts. Encontre os dados do revoscalepy em \Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data. |
| Modelos pré-treinados em R e Python | Modelos pré-treinados são criados para casos de uso específicos e mantidos pela equipe de engenharia de ciência de dados na Microsoft. Você pode usar os modelos pré-treinados como estão para pontuar sentimentos positivos e negativos no texto ou detectar recursos em imagens, usando novas entradas de dados que você fornecer. Os modelos pré-treinados têm suporte e podem ser usados em um servidor autônomo, mas você não pode instalá-los por meio de SQL Server instalação. Para obter mais informações, consulte [instalar modelos de aprendizado de máquina pré-treinados no SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-a-standalone-server"></a>Usando um servidor autônomo

Os desenvolvedores de r e Python normalmente escolhem um servidor autônomo para passar além da memória e restrições de processamento de R e Python de software livre. As bibliotecas de R e Python executadas em um servidor autônomo podem carregar e processar grandes quantidades de dados em vários núcleos e agregar os resultados em uma única saída consolidada. As funções de alto desempenho são projetadas para escala e utilitário: entrega de análise preditiva, modelagem estatística, visualizações de dados e algoritmos de aprendizado de máquina de ponta em um produto de servidor comercial projetado e com suporte do O.

Como um servidor independente dissociado do SQL Server, o ambiente R e Python é configurado, protegido e acessado usando o sistema operacional subjacente e as ferramentas padrão fornecidas no servidor autônomo, não SQL Server. Não há suporte interno para SQL Server dados relacionais. Se você quiser usar dados de SQL Server, poderá criar objetos de fonte de dados e conexões como faria de qualquer cliente.

Como um suplemento para SQL Server, um servidor autônomo também será útil como um ambiente de desenvolvimento poderoso se você precisar de computação local e remota. Os pacotes R e Python em um servidor autônomo são os mesmos fornecidos com uma instalação do mecanismo de banco de dados, permitindo a portabilidade do código e [a alternância do contexto de computação](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).

## <a name="how-to-get-started"></a>Como começar

Inicie a instalação, anexe os binários à sua ferramenta de desenvolvimento favorita e escreva seu primeiro script.

### <a name="step-1-install-the-software"></a>Etapa 1: Instalar o software

Instale uma destas versões:

+ [SQL Server 2017 Machine Learning Server (autônomo)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (autônomo)-R somente](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>Etapa 2: Configurar uma ferramenta de desenvolvimento

Em um servidor autônomo, é comum trabalhar localmente usando um desenvolvimento instalado no mesmo computador.

+ [Configurar ferramentas R](set-up-a-data-science-client.md)
+ [Configurar ferramentas Python](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>Etapa 3: Escreva seu primeiro script

Escreva o script R ou Python usando funções de RevoScaleR, revoscalepy e algoritmos de aprendizado de máquina.
  
  + [Explore R e RevoScaleR em 25 funções](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): Comece com os comandos básicos do R e, em seguida, progredi para as funções analíticas distribuídas RevoScaleR que fornecem alto desempenho e dimensionamento para soluções de R. Inclui versões paralelizáveis de muitos dos pacotes mais populares de modelagem do R, como clustering k-means, árvores de decisão e florestas de decisão, bem como as ferramentas para a manipulação de dados.

  + [Início Rápido: Um exemplo de classificação binária com o pacote](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml)Python microsoftml: Crie um modelo de classificação binária usando as funções de microsoftml e o conjunto de mama câncer conhecido.

Escolha o melhor idioma para a tarefa. O R é melhor para cálculos estatísticos que são difíceis de implementar usando SQL. Para operações baseadas em conjunto sobre dados, aproveite o poder do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obter o máximo de desempenho. Use o mecanismo de banco de dados na memória para computações muito rápidas sobre colunas.

### <a name="step-4-operationalize-your-solution"></a>Etapa 4: Colocar sua solução em operação

Os servidores autônomos podem usar a funcionalidade de [operacionalização](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)com marca não SQL. Você pode configurar um servidor autônomo para operacionalização, que oferece estes benefícios: implantar e hospedar seu código como serviços Web, executar diagnóstico, testar a capacidade do serviço Web.

### <a name="step-5-maintain-your-server"></a>Etapa 5: Manter seu servidor

SQL Server libera atualizações cumulativas regularmente. A aplicação das atualizações cumulativas adiciona aprimoramentos funcionais e de segurança a uma instalação existente. 

As descrições de funcionalidades novas ou alteradas podem ser encontradas no artigo [downloads do CAB](../install/sql-ml-cab-downloads.md) e nas páginas da Web para atualizações cumulativas do [SQL Server 2016](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions) e [SQL Server atualizações cumulativas 2017](https://support.microsoft.com/help/4047329). 

Para obter mais informações sobre como aplicar atualizações a uma instância existente, consulte [aplicar atualizações](../install/sql-machine-learning-standalone-windows-install.md#apply-cu) nas instruções de instalação.

## <a name="see-also"></a>Confira também

 [Instalar o R Server (autônomo) ou Machine Learning Server (autônomo)](../install/sql-machine-learning-standalone-windows-install.md)

