---
title: Instalar modelos pré-treinados
description: Adicione modelos pré-treinados para análise de sentimento e personalização de imagens aos Serviços de Machine Learning do SQL Server (R ou Python) ou ao SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 97da2ed795d002fa47900eb21ead90b48b525387
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81118229"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>Instalar modelos de machine learning pré-treinados no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo explica como usar o PowerShell para adicionar modelos de aprendizado de máquina gratuitos pré-treinados para *análise de sentimento* e *personalização de imagens* a uma instância de SQL Server que tenha integração com R ou Python. Os modelos pré-treinados são criados pela Microsoft e prontos para uso, adicionados a uma instância do como uma tarefa pós-instalação. Para obter mais informações sobre esses modelos, confira a seção [Recursos](#bkmk_resources) deste artigo.

Depois de instalados, os modelos pré-treinados são considerados um detalhe de implementação que capacita funções específicas nas bibliotecas MicrosoftML (R) e microsoftml (Python). Você não deve (e não pode) exibir, personalizar nem treinar novamente modelos, tampouco tratá-los como um recurso independente em código personalizado ou emparelhado com outras funções. 

Para usar os modelos pré-treinados, chame as funções listadas na tabela a seguir.

| Função do R (MicrosoftML) | Função do Python (microsoftml) | Uso |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | Gera uma pontuação de sentimentos positiva/negativa sobre entradas de texto. |
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Extrai informações de texto de entradas de arquivo de imagem. |

## <a name="prerequisites"></a>Pré-requisitos

Os algoritmos de aprendizado de máquina fazem uso de computação intensiva. Recomendamos 16 GB de RAM para cargas de trabalho baixas a moderadas, incluindo a conclusão das instruções passo a passo do tutorial usando todos os dados de exemplo.

Você deve ter direitos de administrador no computador e no SQL Server para adicionar modelos pré-treinados.

Os scripts externos precisam estar habilitados e o serviço SQL Server LaunchPad precisa estar em execução. As instruções de instalação fornecem as etapas para habilitar e verificar essas funcionalidades. 

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
O [pacote MicrosoftML do R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) ou o [pacote MicrosoftML do Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) contém os modelos pré-treinados.

Os [Serviços de Machine Learning do SQL Server](sql-machine-learning-services-windows-install.md) incluem versões da biblioteca de aprendizado de máquina em ambas as linguagens de programação, portanto, esse pré-requisito é atendido sem que você realize nenhuma ação adicional. Já que as bibliotecas estão presentes, você pode usar o script do PowerShell descrito neste artigo para adicionar os modelos pré-treinados a essas bibliotecas.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
O [pacote MicrosoftML do R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) contém os modelos pré-treinados.

O [SQL Server R Services](sql-r-services-windows-install.md), que é somente em R, não inclui o [pacote MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) pronto para uso. Para adicionar o MicrosoftML, você precisa fazer uma [atualização de componente](../install/upgrade-r-and-python.md). Uma vantagem da atualização do componente é que você pode adicionar simultaneamente os modelos pré-treinados, o que torna desnecessária a execução do script do PowerShell. No entanto, se você já fez a atualização, mas não adicionou os modelos pré-treinados na primeira vez, você ainda pode executar o script do PowerShell, conforme descrito neste artigo. Ele funciona para ambas as versões do SQL Server. Antes de fazer isso, confirme se a biblioteca MicrosoftML existe em `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`.
::: moniker-end

<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>Verificar se os modelos pré-treinados estão instalados

Os caminhos de instalação dos modelos do R e do Python são os seguintes:

+ Para o R: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ Para o Python: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

Os nomes de arquivos de modelo estão listados abaixo:

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.model
+ ResNet\_101\_Updated.model
+ ResNet\_18\_Updated.model
+ ResNet\_50\_Updated.model

Se os modelos já estiverem instalados, vá direto para a [etapa de validação](#verify) para confirmar a disponibilidade.

## <a name="download-the-installation-script"></a>Baixar o script de instalação

Clique em [https://aka.ms/mlm4sql](https://aka.ms/mlm4sql) para baixar o arquivo **Install-MLModels.ps1**.

## <a name="execute-with-elevated-privileges"></a>Executar com privilégios elevados

1. Inicie o PowerShell. Na barra de tarefas, clique com o botão direito do mouse no ícone do programa PowerShell e selecione **Executar como administrador**.
2. Insira um caminho totalmente qualificado para o arquivo de script de instalação e inclua o nome da instância. Se pressupormos a existência da pasta Downloads e de uma instância padrão, o comando teria a seguinte aparência:

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**Saída**

Em uma instância padrão dos Serviços de Machine Learning do SQL Server com R e Python conectada à Internet, você deverá ver mensagens semelhantes às seguintes.

   ```powershell
   MSSQL14.MSSQLSERVER
        Verifying R models [9.2.0.24]
        Downloading R models [C:\Users\<user-name>\AppData\Local\Temp]
        Installing R models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\]
        Verifying Python models [9.2.0.24]
        Installing Python models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\]
   PS C:\WINDOWS\system32>
   ```

<a name="verify"> </a>

## <a name="verify-installation"></a>Verifique a instalação

Primeiro, verifique os novos arquivos na [pasta mxlibs](#file-location). Em seguida, execute o código de demonstração para confirmar se os modelos estão instalados e funcionando. 

### <a name="r-verification-steps"></a>Etapas de verificação do R

1. Inicie o **RGUI.EXE** em C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64.

2. Cole o script R a seguir no prompt de comando.

    ```R
    # Create the data
    CustomerReviews <- data.frame(Review = c(
    "I really did not like the taste of it",
    "It was surprisingly quite good!",
    "I will never ever ever go to that place again!!"),
    stringsAsFactors = FALSE)

    # Get the sentiment scores
    sentimentScores <- rxFeaturize(data = CustomerReviews, 
                                    mlTransforms = getSentiment(vars = list(SentimentScore = "Review")))

    # Let's translate the score to something more meaningful
    sentimentScores$PredictedRating <- ifelse(sentimentScores$SentimentScore > 0.6, 
                                            "AWESOMENESS", "BLAH")

    # Let's look at the results
    sentimentScores
    ```

3. Pressione Enter para exibir as pontuações de sentimentos. A saída deverá ser conforme demonstrado a seguir:

    ```R
    > sentimentScores
                                            Review SentimentScore
    1           I really did not like the taste of it      0.4617899
    2                 It was surprisingly quite good!      0.9601924
    3 I will never ever ever go to that place again!!      0.3103435
    PredictedRating
    1            BLAH
    2     AWESOMENESS
    3            BLAH
    ```

### <a name="python-verification-steps"></a>Etapas de verificação do Python

1. Inicie **Python.exe** em C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES.

2. Cole o script Python a seguir no prompt de comando

    ```python
    import numpy
    import pandas
    from microsoftml import rx_logistic_regression, rx_featurize, rx_predict, get_sentiment

    # Create the data
    customer_reviews = pandas.DataFrame(data=dict(review=[
                "I really did not like the taste of it",
                "It was surprisingly quite good!",
                "I will never ever ever go to that place again!!"]))
                
    # Get the sentiment scores
    sentiment_scores = rx_featurize(
        data=customer_reviews,
        ml_transforms=[get_sentiment(cols=dict(scores="review"))])
        
    # Let's translate the score to something more meaningful
    sentiment_scores["eval"] = sentiment_scores.scores.apply(
                lambda score: "AWESOMENESS" if score > 0.6 else "BLAH")
    print(sentiment_scores)
    ```

3. Pressione Enter para imprimir as pontuações. A saída deverá ser conforme demonstrado a seguir:

    ```python
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> Se os scripts de demonstração falharem, verifique primeiro a localização do arquivo. Em sistemas com várias instâncias do SQL Server ou em instâncias que são executadas lado a lado com versões autônomas, é possível que o script de instalação faça uma leitura incorreta do ambiente e coloque os arquivos na localização errada. Normalmente, copiar os arquivos manualmente para a pasta mxlib correta corrige o problema.

## <a name="examples-using-pre-trained-models"></a>Exemplos usando modelos pré-treinados

O link a seguir inclui o código de exemplo que invoca os modelos pré-treinados.

+ [Exemplo de código: Análise de Sentimento usando o Featurizer de Texto](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>Pesquisa e recursos

Atualmente, os modelos disponíveis são modelos de DNN (rede neural profunda) para análise de sentimentos e classificação de imagem. Todos os modelos pré-treinados foram treinados usando o Microsoft **CNTK** ([Cognitive Toolkit](https://cntk.ai/Features/Index.html)).

A configuração de cada rede foi baseada nas seguintes implementações de referência:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

Para obter mais informações sobre os algoritmos usados nesses modelos de aprendizado profundo e o modo como eles são implementados e treinados usando o CNTK, confira estes artigos:

+ [O algoritmo dos pesquisadores da Microsoft estabelece um marco no desafio da ImageNet](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [O Microsoft CNTK oferece o desempenho computacional mais eficiente em aprendizado profundo distribuído](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>Confira também

+ [Serviços de Machine Learning do SQL Server](sql-machine-learning-services-windows-install.md)
+ [Atualizar componentes de R e Python em instâncias do SQL Server](../install/upgrade-r-and-python.md)
+ [Pacote MicrosoftML para R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [Pacote microsoftml para Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
