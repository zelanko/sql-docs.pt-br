---
title: O que é Machine Learning Server ou Microsoft R Server autônomo?
description: Introdução com uma visão geral do Microsoft R Server e do Machine Learning Server autônomos na instalação do SQL Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/13/2019
ms.topic: overview
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 2412bfb8bcd3cacc2db2702879353b92e328b09a
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727390"
---
# <a name="what-are-standalone-machine-learning-server-or-r-server-in-sql-server"></a>O que é Machine Learning Server ou Microsoft R Server autônomo no SQL Server?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O SQL Server fornece suporte à instalação de um Microsoft R Server ou Machine Learning Server autônomo que é executado independentemente do SQL Server. Dependendo de sua versão do SQL Server, um servidor autônomo tem uma base de R de software livre e, possivelmente, Python, sobreposto com bibliotecas de alto desempenho da Microsoft que adicionam análise estatística e preditiva em escala. As bibliotecas também habilitam tarefas de aprendizado de máquina com script em R ou Python. 

No SQL Server 2016, esse recurso é chamado **Microsoft R Server (autônomo)** e inclui apenas R. No SQL Server 2017, é chamado **Machine Learning Server (autônomo)** e inclui R e Python.  

> [!Note]
> Conforme instalado pela instalação do SQL Server, um servidor autônomo é funcionalmente equivalente às versões sem marca SQL do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), compatível com os mesmos cenários de usuário, incluindo execução remota, operacionalização e serviços Web, bem como a coleção completa de bibliotecas de R e Python.

## <a name="components"></a>Componentes

O SQL Server 2016 inclui apenas o R. O SQL Server 2017 oferece suporte às linguagens R e Python. A tabela a seguir descreve os recursos de cada versão.

| Componente | Descrição |
|-----------|-------------|
| Pacotes do R | O [**RevoScaleR**](ref-r-revoscaler.md) é a biblioteca principal para R escalonável com funções para transformação, visualização, análise e manipulação de dados.  <br/>O [**MicrosoftML**](ref-r-microsoftml.md) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de texto, análise de imagem e análise de sentimentos. <br/>O [**sqlRUtils**](ref-r-sqlrutils.md) fornece funções auxiliares para colocar scripts de R em um procedimento armazenado do T-SQL, registrando esse procedimento armazenado em um banco de dados e executando o procedimento armazenado em um ambiente de desenvolvimento de R.<br/>O [**mrsdeploy**](operationalization-with-mrsdeploy.md) oferece implantação de serviço Web (somente no SQL Server 2017). <br/>O [**olapR**](ref-r-olapr.md) é para especificar consultas MDX em R.|
| MRO (Microsoft R Open) | O [**MRO**](https://mran.microsoft.com/open) é a distribuição de software livre de R da Microsoft. O pacote e o interpretador estão incluídos. Sempre use a versão do MRO agrupada na instalação. |
| Ferramentas do R | Os prompts de comando e as janelas do console do R são ferramentas padrão em uma distribuição do R. Encontre-os em \Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64. |
| Scripts e exemplos de R |  Os pacotes do R e do RevoScaleR de software livre incluem conjuntos de dados internos para que você possa criar e executar scripts usando dados pré-instalados. Procure por eles em \Program Files\Microsoft SQL Server\140\R_SERVER\library\datasets e \library\RevoScaleR. |
| Pacotes do Python | O [**revoscalepy**](../python/ref-py-revoscalepy.md) é a biblioteca principal para Python escalonável com funções para transformação, visualização, análise e manipulação de dados. <br/>O [**microsoftml**](../python/ref-py-microsoftml.md) adiciona algoritmos de aprendizado de máquina para criar modelos personalizados para análise de texto, análise de imagem e análise de sentimentos.  |
| Ferramentas do Python | A ferramenta de linha de comando interna do Python é útil para tarefas e testes ad hoc. Encontre a ferramenta em \Program Files\Microsoft SQL Server\140\PYTHON_SERVER\python.exe. |
| Anaconda | O Anaconda é uma distribuição de software livre de pacotes do Python e essenciais. |
| Scripts e exemplos de Python | Assim como acontece com o R, o Python inclui scripts e conjuntos de dados internos. Localize os dados do revoscalepy em \Program Files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data. |
| Modelos pré-treinados em R e Python | Os modelos pré-treinados são criados para casos de uso específicos e mantidos pela equipe de engenharia de ciência de dados na Microsoft. Você pode usar os modelos pré-treinados no estado em que se encontram para pontuar sentimentos positivos e negativos no texto ou detectar recursos em imagens, usando novas entradas de dados fornecidas por você. Os modelos pré-treinados são compatíveis e podem ser usados em um servidor autônomo, mas você não pode instalá-los usando a instalação do SQL Server. Para obter mais informações, confira [Instalar os modelos de machine learning pré-treinados do SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-a-standalone-server"></a>Como usar um servidor autônomo

Os desenvolvedores de R e Python normalmente escolhem um servidor autônomo para passar além da memória e das restrições de processamento de R e Python de software livre. As bibliotecas do R e do Python executadas em um servidor autônomo podem carregar e processar grandes quantidades de dados em vários núcleos e agregar os resultados em uma única saída consolidada. As funções de alto desempenho são projetadas para escala e utilitário: entrega de análise preditiva, modelagem estatística, visualizações de dados e algoritmos de aprendizado de máquina de ponta em um produto para servidores comerciais projetado e com suporte da Microsoft.

Como um servidor independente dissociado do SQL Server, o ambiente do R e do Python é configurado, protegido e acessado usando o sistema operacional subjacente e as ferramentas padrão fornecidas no servidor autônomo, não no SQL Server. Não há suporte interno para dados relacionais do SQL Server. Se você quiser usar dados do SQL Server, poderá criar conexões e objetos de fonte de dados como faria usando qualquer cliente.

Como um suplemento para SQL Server, um servidor autônomo também será útil como um ambiente de desenvolvimento avançado se você precisar de computação local e remota. Os pacotes do R e do Python em um servidor autônomo são os mesmos fornecidos com uma instalação do mecanismo de banco de dados, permitindo portabilidade de código e [alternância de contexto de computação](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).

## <a name="how-to-get-started"></a>Como começar a usar

Inicie a instalação, anexe os binários à sua ferramenta de desenvolvimento favorita e escreva seu primeiro script.

### <a name="step-1-install-the-software"></a>Etapa 1: Instalar o software

Instale uma destas versões:

+ [SQL Server 2017 Machine Learning Server (autônomo)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (autônomo) – somente R](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>Etapa 2: Configurar uma ferramenta de desenvolvimento

Em um servidor autônomo, é comum trabalhar localmente usando um desenvolvimento instalado no mesmo computador.

+ [Configurar ferramentas R](set-up-a-data-science-client.md)
+ [Configurar ferramentas Python](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>Etapa 3: Escrever seu primeiro script

Escreva o script do R ou do Python usando funções de RevoScaleR, revoscalepy e algoritmos de aprendizado de máquina.
  
  + [Explorar R e RevoScaleR em 25 funções](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): Comece com comandos básicos do R e progrida para funções analíticas distribuíveis do RevoScaleR que proporcionam alto desempenho e escala para as soluções de R. Inclui versões paralelizáveis de muitos dos pacotes mais populares de modelagem do R, como clustering k-means, árvores de decisão e florestas de decisão, bem como as ferramentas para a manipulação de dados.

  + [Início Rápido: Um exemplo de classificação binária com o pacote microsoftml do Python](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): Crie um modelo de classificação binária usando as funções de microsoftml e o conjunto de dados sobre câncer de mama conhecido.

Escolha a melhor linguagem para a tarefa. A linguagem R é melhor para cálculos estatísticos que podem ser difíceis de implementar usando SQL. Para operações baseadas em conjunto sobre dados, aproveite o poder de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para alcançar o desempenho máximo. Use o mecanismo de banco de dados em memória para computações muito rápidas sobre colunas.

### <a name="step-4-operationalize-your-solution"></a>Etapa 4: Operacionalizar sua solução

Os servidores autônomos podem usar a funcionalidade de [operacionalização](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server) não SQL. Você pode configurar um servidor autônomo para operacionalização, que oferece estes benefícios: implantar e hospedar seu código como serviços Web, executar diagnóstico, testar a capacidade do serviço Web.

### <a name="step-5-maintain-your-server"></a>Etapa 5: Manter seus servidores

O SQL Server libera atualizações cumulativas regularmente. A aplicação das atualizações cumulativas adiciona aprimoramentos funcionais e de segurança a uma instalação existente. 

As descrições de funcionalidades novas ou alteradas podem ser encontradas no artigo [Downloads do CAB](../install/sql-ml-cab-downloads.md) e nas páginas da Web das [Atualizações cumulativas do SQL Server 2016](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions) e das [Atualizações cumulativas do SQL Server 2017](https://support.microsoft.com/help/4047329). 

Para obter mais informações sobre como aplicar atualizações a uma instância existente, confira [Aplicar atualizações](../install/sql-machine-learning-standalone-windows-install.md#apply-cu) nas instruções de instalação.

## <a name="see-also"></a>Confira também

 [Instalar o Microsoft R Server (autônomo) ou o Machine Learning Server (autônomo)](../install/sql-machine-learning-standalone-windows-install.md)

