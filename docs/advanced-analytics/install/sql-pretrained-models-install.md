---
title: Instalar os modelos de aprendizado de máquina pré-treinado no SQL Server | Microsoft Docs
description: Adicione modelos previamente treinados para personalização de imagem e análise de sentimento para SQL Server 2017 serviços Machine Learning (R ou Python) ou SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/18/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 53bffd17ee225cf3e1d10ec4a0cd813ec7688989
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174993"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>Instalar previamente treinado modelos de machine learning no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como adicionar livre previamente treinado modelos de machine learning para *análise de sentimento* e *personalização de imagem* para uma instância do mecanismo de banco de dados do SQL Server com integração de R ou Python. Os modelos previamente treinados são criados pela Microsoft e prontos para uso, facilmente adicionados a uma instância existente usando um script do PowerShell. Para obter mais informações sobre esses modelos, consulte o [recursos](#bkmk_resources) seção deste artigo.

Uma vez instalado, os modelos previamente treinados são considerados um detalhe de implementação que potencializam a funções específicas do MicrosoftML (R) e bibliotecas do microsoftml (Python). Você não deve (e não pode) exibir, personalizar ou readaptar os modelos, nem você tratá-los como um recurso independente no código personalizado ou emparelhado outras funções. 

Funções invocar os modelos pré-treinados são listadas na tabela a seguir.

| Função de R (MicrosoftML) | Função Python (microsoftml) | Uso |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | Gera a pontuação de sentimento negativo positivo sobre entradas de texto. [Saiba mais](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/).|
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Extrai informações de texto de entradas de arquivo de imagem. [Saiba mais](https://blogs.msdn.microsoft.com/mlserver/2017/04/12/image-featurization-with-a-pre-trained-deep-neural-network-model/). |

## <a name="prerequisites"></a>Prerequisites

[Serviços de aprendizado de máquina do SQL Server 2017](sql-machine-learning-services-windows-install.md) com R, Python ou ambos. 

[SQL Server 2016 R Services](sql-r-services-windows-install.md) os clientes podem usar uma abordagem diferente. Para o SQL Server 2016, é necessário atualizar os componentes do R para adicionar o [pacote MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), conforme documentado no [atualizar componentes (R e Python) de aprendizado de máquina](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md). Quando você atualiza os componentes do R, você pode simultaneamente adicionar modelos previamente treinados, que torna a execução do script do PowerShell redundante. No entanto, se você já atualizados, mas perdeu adicionando os modelos previamente treinados na primeira vez, você pode executar o script do PowerShell, conforme descrito neste artigo. Antes de fazer, confirme se a biblioteca MicrosoftML existe em C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library.
  
Scripts externos devem ser habilitados e o serviço LaunchPad do SQL Server deve ser executado. Instruções de instalação fornecem as etapas para verificação e configuração adicional.

Você deve ter direitos de administrador no computador e do SQL Server para adicionar modelos previamente treinados.

Algoritmos de aprendizado de máquina são computacionalmente intensivas. Recomendamos 16 GB de RAM para cargas de trabalho de baixo a moderado, incluindo a conclusão do tutorial passo a passo usando todos os dados de exemplo.

<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>Verifique se os modelos previamente treinados estão instalados

Os caminhos de instalação para os modelos de R e Python são da seguinte maneira:

+ Para r: C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64

+ Para o Python: C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Lib\site packages\microsoftml\mxLibs 

Nomes de arquivo de modelo estão listados abaixo:

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.Model
+ ResNet\_101\_Updated.model
+ ResNet\_18\_Updated.model
+ ResNet\_50\_Updated.model

Se os modelos já estão instalados, pule para a [etapa de validação](#verify) para confirmar a disponibilidade.

## <a name="download-the-installation-script"></a>Baixe o script de instalação

Clique em [ https://aka.ms/mlm4sql ](https://aka.ms/mlm4sql) para baixar o arquivo **Install MLModels.ps1**.

## <a name="execute-with-elevated-privileges"></a>Executar com privilégios elevados

1. Inicie o PowerShell. Na barra de tarefas, clique com botão direito no ícone de programa do PowerShell e selecione **executar como administrador**.
2. Insira um caminho totalmente qualificado para o arquivo de script de instalação e incluem o nome da instância. Supondo que a pasta de Downloads e uma instância padrão, o comando pode parecer com isso:

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**Saída**

Em um conectado à internet aprendizado de máquina do SQL Server 2017 instância padrão com R e Python, você verá mensagens semelhantes à seguinte.

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

Primeiro, verifique os novos arquivos na [mxlibs pasta](#file-location). Em seguida, execute o código de demonstração para confirmar que os modelos serão instalado e funcional. 

### <a name="r-verification-steps"></a>Etapas de verificação de R

1. Iniciar **RGUI. EXE** em C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\bin\x64.

2. Cole o script R a seguir no prompt de comando.

    ```r
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

3. Pressione Enter para visualizar as pontuações de sentimento. Saída deve ser da seguinte maneira:

    ```
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

1. Inicie **Python.exe** em C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES.

2. Cole o seguinte script do Python no prompt de comando

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

3. Pressione Enter para imprimir as pontuações. Saída deve ser da seguinte maneira:

    ```
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> Se os scripts de demonstração falhar, verifique o local do arquivo primeiro. Em sistemas com várias instâncias do SQL Server ou para as instâncias que são executados lado a lado com versões independentes, é possível que o script de instalação ler incorretamente o ambiente e colocar os arquivos no local errado. Geralmente, copiar manualmente os arquivos na pasta correta mxlib corrige o problema.

## <a name="examples-using-pre-trained-models"></a>Exemplos que usam modelos previamente treinados

Os links a seguir incluem o código de exemplo e instruções passo a passo invocar os modelos pré-treinados.

+ [Análise de sentimento com o Python em serviços do SQL Server Machine Learning](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

+ [Personalização de imagem com um modelo de rede neural profunda pré-treinada](https://blogs.msdn.microsoft.com/mlserver/2017/04/12/image-featurization-with-a-pre-trained-deep-neural-network-model/)

  O modelo previamente treinado para imagens dá suporte à personalização de imagens que você fornecer. Para usar o modelo, você chama o **featurizeImage** transformar. A imagem é carregada, redimensionado e destacados pelo modelo treinado. A saída do featurizer de DNN, em seguida, é usada para treinar um modelo linear para classificação de imagem. Para usar esse modelo, todas as imagens devem ser redimensionadas para cumprir os requisitos do modelo treinado. Por exemplo, se você usar um modelo de AlexNet, a imagem deve ser redimensionada para 227 x 227 px.

+ [Exemplo de código: análise de sentimento usando o recurso de texto](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>Pesquisa e recursos

Atualmente, os modelos que estão disponíveis são modelos de rede neural profunda (DNN) para classificação de imagem e análise de sentimento. Todos os modelos previamente treinados foram treinados por meio da Microsoft [Kit de ferramentas de rede de computação](https://cntk.ai/Features/Index.html), ou **CNTK**.

A configuração de cada rede baseia as seguintes implementações de referência:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

Para obter mais informações sobre os algoritmos usados nesses modelos de aprendizado profundo e como eles são implementados e treinado usando CNTK, consulte estes artigos:

+ [Algoritmo os pesquisadores da Microsoft define marco ImageNet desafio](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Toolkit de rede computacional da Microsoft oferece o mais eficiente distribuída de aprendizagem profunda desempenho computacional](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>Confira também

+ [SQL Server 2016 R Services](sql-r-services-windows-install.md)
+ [Serviços de aprendizado de máquina do SQL Server 2017](sql-machine-learning-services-windows-install.md)
+ [Atualizar os componentes de R e Python em instâncias do SQL Server](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)
+ [Pacote MicrosoftML para R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [pacote microsoftml para Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
