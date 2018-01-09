---
title: "Instalar os modelos de aprendizado de máquina pré-treinado no SQL Server | Microsoft Docs"
ms.date: 11/16/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 76b0c3cd2b472b0d4794a171510906cf05e34d5c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>Instalar pré-treinado modelos no SQL Server de aprendizado de máquina

Este artigo descreve como adicionar modelos pré-treinado a uma instância do SQL Server que já tem o R Services ou serviços de aprendizado de máquina instalado.

A opção para instalar modelos pré-treinado está disponível quando você usa o Windows installer separado para o Microsoft R Server ou servidor de aprendizado de máquina. Você pode usar esse instalador para obter apenas os modelos pré-treinado, ou você pode usá-lo para [atualizar a componentes de aprendizado de máquina](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md) em uma instância do SQL Server 2016 ou 2017 do SQL Server.

Depois de baixar os modelos pré-treinado ao executar o instalador, há algumas etapas adicionais para configurar os modelos para uso com o SQL Server. Este artigo descreve o processo.

Para obter um exemplo de como usar os modelos pré-treinado com dados do SQL Server, consulte este blog pela equipe de aprendizado de máquina do SQL Server: 

+ [Análise de sentimento com Python nos serviços de aprendizado de máquina do SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

## <a name="benefits-of-using-pretrained-models"></a>Benefícios do uso de modelos de pré-treinado

Esses modelos previamente treinados foram criados para ajudar os clientes que precisam para executar tarefas como a personalização de imagem ou de análise de sentimento, mas que não possuem os recursos para obter os conjuntos de dados grandes ou treinar um modelo complexo. Usando modelos previamente treinados permite começar em texto e imagem, processamento de forma eficiente.

Atualmente, os modelos que estão disponíveis são modelos de rede neurais profundas (DNN) para classificação de imagem e análise de sentimento. Todos os modelos pré-treinado foram treinados por meio do Microsoft [Kit de ferramentas de rede de computação](https://cntk.ai/Features/Index.html), ou **CNTK**.

A configuração de cada rede baseia as implementações de referência a seguir:

+ ResNet-18
+ 50 ResNet
+ ResNet 101
+ AlexNet

Para obter mais informações sobre esses modelos, consulte [modelos para detecção de imagem e análise de sentimento de aprendizado de máquina previamente treinada](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)

Para obter mais informações sobre redes de aprendizado e sua implementação usando CNTK, consulte estes artigos:

+ [Algoritmo os pesquisadores da Microsoft define marco ImageNet desafio](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Kit de ferramentas de rede computacional Microsoft oferece mais eficiente profundo distribuído desempenho computacional de aprendizado](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-install-the-models-on-sql-server"></a>Como instalar os modelos no SQL Server

1. Execute o instalador separado baseado no Windows para o servidor de aprendizado de máquina. Para locais de download, consulte:

    + [Instalar o servidor para Windows de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
    + [Instalar o R Server 9.1 para Windows](https://docs.microsoft.com/r-server/install/r-server-install-windows)

2. A seleção de recursos para instalação depende se você estiver obtendo apenas os modelos ou executando outras atualizações usando o instalador.
 
    + Se esta é uma nova instalação do servidor de aprendizado de máquina, e você não deseja fazer outras mudanças nos componentes de R ou Python, selecionados **somente** a opção de pré-treinado de modelos. Aceite todos os prompts, incluindo os contratos de licença.

    + Para atualizar os componentes de R ou Python ao mesmo tempo, selecione o idioma (R, Python ou ambos) que você deseja atualizar e selecione a opção de pré-treinado de modelos. Selecione uma ou mais instâncias para aplicar essas alterações.

    + Se você tiver previamente instalado o servidor de aprendizado de máquina e os componentes de R ou Python usando a opção de associação atualizados, deixe todas as seleções anteriores **como**e selecione as opções de pré-treinado de modelos. Não desmarque todas as opções selecionadas anteriormente; Se você fizer isso, o instalador remove os componentes.

3. Quando a instalação for concluída, abra um prompt de comando do Windows **como administrador**e navegue até a pasta de inicialização de instalação do SQL Server, que também contém o instalador do Microsoft R. Em uma instância padrão do SQL Server 2017, a pasta seria:
    
    `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\SQL2017\x64\`

4. Execute RSetup.exe e indicar o componente a ser instalado, a versão e a pasta que contém os arquivos de origem do modelo, usando os argumentos de linha de comando mostrados nestes exemplos:

    + Para usar modelos com **R_SERVICES**:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    Por exemplo, para habilitar o uso da versão mais recente dos modelos de pré-treinado para R em uma instância padrão do SQL Server de 2017, você executaria esta instrução:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    Em uma instância nomeada, o comando seria semelhante a esta:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + Para usar modelos pré-treinado com R Server (autônomo) ou servidor de aprendizado de máquina (autônomo):

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    Por exemplo, para habilitar o uso da versão mais recente dos modelos de pré-treinado para R, em uma instalação padrão do servidor de R com o SQL Server 2016, você executaria esta instrução:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir ‘C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\MicrosoftML\mxLibs\"`
    
    + Para usar modelos pré-treinado com **PYTHON_SERVICES**:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    Por exemplo, para habilitar o uso da versão mais recente dos modelos de pré-treinado para Python em uma instância padrão do SQL Server de 2017, você executaria esta instrução:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    Em uma instância nomeada, o comando seria semelhante a esta:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + Para usar o Python classificação modelos ao servidor de aprendizado de máquina (autônomo):

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<sql_folder>\PYTHON_SERVER\site-packages\microsoftml\mxLibs"`

    Por exemplo, supondo que uma instalação padrão do servidor de aprendizado de máquina (autônomo) usando a instalação do SQL Server 2017, execute esta instrução:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER\Lib\site-packages\microsoftml\mxLibs"`

5. Os valores a seguir têm suporte para o parâmetro version:

    + Versão Release candidate 0: **9.1.0.0**
    + Versão Release candidate 1: **9.2.0.22**
    + NA VERSÃO RTM: **9.2.0.100**
    + A atualização cumulativa 1: **9.2.0.24**

6. Se a instalação for bem-sucedida, os modelos a seguir devem ser adicionados ao seu R\_serviços ou PYTHON\_pastas de serviços:

    - AlexNet\_Updated.model
    - ImageNet1K\_mean.xml
    - pretrained.Model
    - ResNet\_101\_Updated.model
    - ResNet\_18\_Updated.model
    - ResNet\_50\_Updated.model


> [!NOTE]
> 
> Se o caminho para o arquivo de modelo é muito longo, você poderá receber um erro ao chamar o arquivo de modelo de código Python. Isso é devido a uma limitação na implementação atual do Python. Esse problema será corrigido em uma versão futura do serviço.

## <a name="examples"></a>Exemplos

Depois de ter instalado os modelos, você pode usar os modelos chamando-os no seu código.

### <a name="image-featurization-example"></a>Exemplo de personalização de imagem

O modelo pré-treinado para imagens dá suporte a personalização de imagens que você fornecer. Esse modelo específico foi treinado usando [CNTK](https://docs.microsoft.com/cognitive-toolkit/). 

Para usar o modelo, você deve chamar o **featurizeImage** transformação.

+ [featurizeImage: Machine Learning imagem personalização de transformação](https://docs.microsoft.com/r-server/r-reference/microsoftml/featurizeimage)

Neste exemplo, consulte o segundo bloco de código. A imagem é carregada, redimensionadas e featurized pelo modelo DNN convolutional pré-treinado. A saída do recurso de DNN, em seguida, é usada para treinar um modelo linear para classificação de imagem.

A imagem deve ser redimensionada para atender aos requisitos do modelo treinado: as imagens usadas para treinamento foram 224 x 224 px. Se você estiver usando um modelo de AlexNet, a imagem deve ser redimensionada para 227 x 227 px.

```R
 model <- rxFastLinear(
     Label ~ Features,
     data = train,
     mlTransforms = list(
         loadImage(vars = list(Features = "Path")),
         resizeImage(vars = "Features", width = 224, height = 224), 
         extractPixels(vars = "Features"),
         featurizeImage(var = "Features")
         ),
     mlTransformVars = "Path")
```

> [!NOTE]
> Não é possível ler ou modificar os modelos de pré-treinado, porque eles são compactados usando um formato nativo, para melhorar o desempenho.

### <a name="text-analysis-example"></a>Exemplo de análise de texto

Consulte o exemplo a seguir para ver uma demonstração de como usar o modelo de personalização de texto pré-treinado para classificação de texto:

[Análise de sentimento usando o recurso de texto](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)
