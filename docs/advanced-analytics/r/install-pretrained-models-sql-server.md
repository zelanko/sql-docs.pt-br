---
title: Instalar os modelos de aprendizado de máquina previamente treinado no SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b21245bd74f59f4ad7fe2370ad3587053e756a03
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>Instalar os modelos no SQL Server de aprendizado de máquina previamente treinada
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como adicionar modelos previamente treinados para uma instância (no banco de dados) do SQL Server que já tem o R Services ou serviços de aprendizado de máquina do SQL Server instalado. 

Existem modelos previamente treinados para ajudar os clientes que precisam para executar tarefas como a personalização de imagem ou de análise de sentimento, mas que não possuem os recursos para obter os conjuntos de dados grandes ou treinar um modelo complexo. A equipe de servidor de aprendizado de máquina criado e treinar esses modelos para ajudá-lo a começar em texto e imagem, processamento de forma eficiente. Para obter mais informações, consulte o [recursos](#bkmk_resources) deste artigo.

Para obter um exemplo de como usar os modelos previamente treinados com dados do SQL Server, consulte este blog pela equipe de aprendizado de máquina do SQL Server: [análise de sentimento com Python nos serviços de aprendizado de máquina do SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

## <a name="pre-trained-model-availability"></a>Disponibilidade do modelo previamente treinado

Modelos previamente treinados são instalados usando a mídia de instalação do servidor de aprendizado de máquina do Microsoft (ou Microsoft R Server, se você estiver adicionando modelos a uma instalação do SQL Server 2016). Você pode usar a edição de desenvolvedor gratuita para instalar os modelos. Não há nenhum extra custo associado à instalação do modelo. 

Modelos previamente treinados funcionam com os seguintes produtos e idiomas. O programa de instalação detecta a biblioteca de integração, MicrosoftML ou microsoftml de idioma e, em seguida, insere os modelos treinados previamente na biblioteca do respectiva. Quando o modelo de instalação for concluído, pode acessar os modelos por meio de funções de biblioteca.

+ SQL Server 2016 R Services (no banco de dados) - R somente com o [MicrosoftML biblioteca](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ SQL Server 2016 R Server (autônomo) - R somente com o [MicrosoftML biblioteca](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ SQL Server 2017 Machine Learning Services (no banco de dados) - R com a [MicrosoftML biblioteca] (https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), Python com o [microsoftml biblioteca](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
+ 2017 Machine Learning servidor do SQL Server (autônomo) - R com a [MicrosoftML biblioteca] (https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), Python com o [microsoftml biblioteca](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)

O processo de instalação difere ligeiramente dependendo de sua versão do SQL Server. Consulte as seções a seguir para obter instruções para cada versão.

> [!NOTE]
> Não é possível ler ou modificar os modelos treinados previamente. Eles são compactados usando um formato nativo para melhorar o desempenho.

## <a name="obtain-files-for-an-offline-installation"></a>Obter arquivos para uma instalação offline

Para instalar os modelos previamente treinados em um servidor que não tem acesso à internet, baixe os instaladores apropriados antecipadamente e copie o instalador para uma pasta local no servidor. 

Consulte esta página para os links de download para todos os instaladores de R Server e o servidor de aprendizado de máquina: [instalação Offline](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)

## <a name="install-pre-trained-models-on-sql-server-2016-r-services"></a>Instalar previamente treinados modelos no SQL Server 2016 R Services

Com o SQL Server 2016, você poderá instalar e usar os modelos R previamente treinados somente se você atualizar primeiro a componentes, em um processo chamado de aprendizado de máquina **associação**. 

Para fazer isso, executando o Windows installer separado para Microsoft R Server ou servidor de aprendizado de máquina em um computador com uma instalação do SQL Server 2016 R Services e, em seguida, selecionando uma instância ou instâncias **associar**. Um meio de instância que a política de suporte associada à instância de associação é alterado para permitir que as atualizações mais frequentes R. 

1. Inicie o instalador baseado no Windows separado para cada uma [R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server) ou [Server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

2. Selecione a instância para atualização e, em seguida, selecione a opção para obter os modelos treinados previamente.

    Para obter mais informações, consulte [atualizar os componentes de aprendizado de máquina usadas pelo SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

    Se você executou anteriormente associação para atualizar os componentes de R e deseja adicionar os modelos treinados previamente, deixe todas as seleções anteriores **como**e selecione a opção de modelos previamente treinado. 
    
    Não desmarque todas as opções selecionadas anteriormente; Se você fizer isso, o instalador remove os componentes.

3. É recomendável que você aceite as configurações padrão para os locais de modelo.

4. Aceite todos os prompts, incluindo os contratos de licença.

Após a associação é concluída, a versão de R e bibliotecas associadas com a instância são substituídas por versões mais recentes fornecidas em R Server ou servidor de aprendizado de máquina. 

Com o SQL Server 2016, você deve executar algumas etapas adicionais para registrar os modelos com a biblioteca de instância do SQL Server 2016. Repita essas etapas para cada instância em que você instalou os modelos treinados previamente.

1. Abra um prompt de comando do Windows **como administrador**.

2. Navegue até a pasta de inicialização de instalação do SQL Server, que também contém o instalador do Microsoft R. Em uma instância padrão do SQL Server 2016, a pasta seria:
    
    `C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\SQL2017\x64\`

3. Execute `RSetup.exe` e indicar o componente a ser instalado, a versão e a pasta que contém os arquivos de origem do modelo, usando a seguinte sintaxe:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\R_SERVICES\library\MicrosoftML\mxLibs\x64"`. 

    Os valores a seguir têm suporte para o parâmetro version:

    + Versão Release candidate 0: **9.1.0.0**
    + Versão Release candidate 1: **9.2.0.22**
    + NA VERSÃO RTM: **9.2.0.100**
    + A atualização cumulativa 1: **9.2.0.24**
    + Atualização cumulativa 4: **9.3.0**

    > [!NOTE]
    > As versões correspondentes do SQL Server são listadas para dar uma ideia da hora em que a atualização foi publicada. Se você não tiver certeza de que a versão instalada com o SQL Server, abra a pasta R_SERVICES para a instância e abra RGui (`~\R_SERVICES\bin\x64`). A tela inicial lista as versões para a versão Microsoft R Open e do servidor de aprendizado de máquina. 

    Por exemplo usar o R previamente treinado modelos com uma instância padrão do **R_SERVICES**, execute este comando:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    Em uma instância nomeada, o comando seria semelhante a esta:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL13.MyInstanceName\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

4. Se a instalação for bem-sucedida, os modelos a seguir devem ser adicionados ao seu `R_SERVICES` pasta:

    + AlexNet\_Updated.model
    + ImageNet1K\_mean.xml
    + pretrained.Model
    + ResNet\_101\_Updated.model
    + ResNet\_18\_Updated.model
    + ResNet\_50\_Updated.model

## <a name="install-pre-trained-models-on-sql-server-machine-learning-services-in-database"></a>Instalar modelos previamente treinados nos serviços de aprendizado de máquina do SQL Server (no banco de dados)

Se você já tiver instalado o SQL Server 2017, você pode obter os modelos treinados previamente de duas maneiras:

+ Atualizar os componentes do Python e R por meio de associação e instalar os modelos treinados previamente ao mesmo tempo
+ Instalar apenas os modelos previamente treinados

As instruções a seguir descrevem o processo para atualizar os componentes de aprendizado de máquina e obter os modelos treinados previamente ao mesmo tempo.

1. Execute o instalador baseado no Windows para o servidor de aprendizado de máquina. Você pode baixar o instalador dos links nesta página: [instalar machine Learning Server para Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

2. Se você estiver instalando os modelos para um servidor que não tem acesso à internet, certifique-se de também baixar o instalador para os modelos treinados previamente nesta página: [instalação Offline para o servidor de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline).

3. Execute o instalador.

4. Para atualizar os componentes de R ou Python ao mesmo tempo, selecione o idioma (R, Python ou ambos) que você deseja atualizar.

    Se você tiver previamente instalado o servidor de aprendizado de máquina e os componentes de R ou Python usando a opção de associação atualizados, deixe todas as seleções anteriores **como**e selecione as opções de modelos previamente treinado. Não desmarque todas as opções selecionadas anteriormente; Se você fizer isso, o instalador remove os componentes.

5. Aceite todos os prompts, incluindo os contratos de licença.

Com o SQL Server 2017, nenhuma configuração adicional é necessária.

> [!NOTE]
> 
> Para modelos de Python, você poderá receber um erro ao chamar o arquivo de modelo de código Python. Isso é devido a uma limitação na implementação atual do Python, que limitam o tamanho do caminho para o arquivo de modelo. Esse problema foi corrigido e estarão disponível em uma versão futura do serviço.

## <a name="install-pre-trained-models-with-sql-server-standalone-r-server"></a>Instalar modelos previamente treinados com R autônomo do SQL server

Se você instalou uma versão anterior do R Server (autônomo) usando a instalação do SQL Server 2016, você pode adicionar a capacidade de usar os modelos treinados previamente atualizando R Server usando o instalador de baseados em Windows mais recente. 

Os modelos treinados previamente foram primeiramente disponibilizados como uma opção com [Microsoft R Server 9.1](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/introducing-microsoft-r-server-9-1-release/), mas as atualizações foram adicionadas a cada versão. É recomendável obter a versão mais recente possível, mas versões anteriores são listadas aqui [libera R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install)

As instruções a seguir descrevem como atualizar os componentes de R e, ao mesmo tempo, adicionar os modelos treinados previamente.

1. Inicie o instalador baseado no Windows separado para cada uma [R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server) ou [Server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

2. Selecione os idiomas que você deseja atualizar e selecione o **Pre-trained modelos** opção.

    > [!TIP]
    > Se você executou anteriormente o instalador para atualizar o R Server (autônomo) e deseja adicionar os modelos treinados previamente, deixe todas as seleções anteriores **como**e selecione apenas a versão anterior**-treinado modelos** opção . **Não** desmarque todas as opções selecionadas anteriormente; se você fizer isso, o instalador remove os componentes.

    É recomendável que você aceite as configurações padrão para os locais de modelo.

3. Clique em **Continuar**. 

4. Aceite todos os prompts, incluindo os contratos de licença.

Após a conclusão da instalação, você deve executar algumas etapas adicionais para registrar os modelos treinados previamente.

1. Abra um prompt de comando do Windows **como administrador**.

2. Navegue até a pasta de inicialização de instalação para R Server (autônomo), que também contém o instalador do Microsoft R. 

3. Execute `RSetup.exe` e indicar o componente a ser instalado, a versão e a pasta que contém os arquivos de origem do modelo, usando a seguinte sintaxe:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    Os valores a seguir têm suporte para o parâmetro version:

    + Versão Release candidate 0: **9.1.0.0**
    + Versão Release candidate 1: **9.2.0.22**
    + NA VERSÃO RTM: **9.2.0.100**
    + A atualização cumulativa 1: **9.2.0.24**
    + Atualização cumulativa 4: **9.3.0**

    Por exemplo, para habilitar o uso da versão mais recente dos modelos previamente treinados para R, em uma instalação padrão do R Server (autônomo), você executaria esta instrução:

    `RSetup.exe /install /component MLM /version 9.3.0 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\MicrosoftML\mxLibs\"`

## <a name="install-pre-trained-models-with-sql-server-2017-standalone-server"></a>Instalar os modelos treinados previamente com o servidor do SQL Server 2017 autônomo

Se você instalou o servidor de aprendizado de máquina usando a instalação do SQL Server 2017, você adicionar os modelos treinados previamente ao executar o instalador baseado no Windows. Você pode selecionar a opção para atualizar os componentes de R ou Python e ao mesmo tempo, adicionar os modelos treinados previamente. 

Nenhuma configuração adicional é necessária após a conclusão da instalação.

## <a name="bkmk_resources"></a> Pesquisa e recursos

Atualmente, os modelos que estão disponíveis são modelos de rede neurais profundas (DNN) para classificação de imagem e análise de sentimento. Todos os modelos previamente treinados foram treinados por meio do Microsoft [Kit de ferramentas de rede de computação](https://cntk.ai/Features/Index.html), ou **CNTK**.

A configuração de cada rede baseia as implementações de referência a seguir:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

Para obter mais informações sobre os algoritmos usados nesses modelos de aprendizado e como eles são implementados e treinado usando CNTK, consulte estes artigos:

+ [Algoritmo os pesquisadores da Microsoft define marco ImageNet desafio](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Kit de ferramentas de rede computacional Microsoft oferece mais eficiente profundo distribuído desempenho computacional de aprendizado](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-use-pre-trained-models-for-text-analysis"></a>Como usar modelos previamente treinados para análise de texto

Consulte o exemplo a seguir para ver uma demonstração de como usar o modelo de personalização do texto previamente treinado para classificação de texto:

[Análise de sentimento usando o recurso de texto](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

## <a name="how-to-use-pre-trained-models-for-image-detection"></a>Como usar modelos previamente treinados para detecção de imagem

O modelo previamente treinado para imagens dá suporte a personalização de imagens que você fornecer. Para usar o modelo, você deve chamar o **featurizeImage** transformação. A imagem é carregada, redimensionadas e featurized pelo modelo treinado. A saída do recurso de DNN, em seguida, é usada para treinar um modelo linear para classificação de imagem.

Para usar esse modelo, todas as imagens devem ser redimensionadas para atender aos requisitos do modelo treinado. Por exemplo, se você usar um modelo de AlexNet, a imagem deve ser redimensionada para 227 x 227 px.

Para obter mais informações, consulte [modelos previamente treinados para detecção de imagem e análise de sentimento](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)
