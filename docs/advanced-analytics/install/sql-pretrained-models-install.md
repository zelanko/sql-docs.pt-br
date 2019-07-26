---
title: Instalar modelos de aprendizado de máquina pré-treinados
description: Adicione modelos pré-treinados para análise de sentimentos e personalização de imagem a SQL Server 2017 Serviços de Machine Learning (R ou Python) ou SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f89e638b6b9486b17974a04af6076e6c7154fa88
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470342"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>Instalar modelos de aprendizado de máquina pré-treinados no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo explica como usar o PowerShell para adicionar modelos de aprendizado de máquina pré-treinados gratuitos para *análise de sentimentos* e *personalização de imagem* a uma instância SQL Server com integração de R ou Python. Os modelos pré-treinados são criados pela Microsoft e prontos para uso, adicionados a uma instância do como uma tarefa pós-instalação. Para obter mais informações sobre esses modelos, consulte a seção [recursos](#bkmk_resources) deste artigo.

Depois de instalados, os modelos pré-treinados são considerados um detalhe de implementação que capacita funções específicas nas bibliotecas MicrosoftML (R) e MicrosoftML (Python). Você não deve (e não pode) exibir, personalizar ou treinar novamente os modelos nem pode tratá-los como um recurso independente em código personalizado ou emparelhar outras funções. 

Para usar os modelos pretreinados, chame as funções listadas na tabela a seguir.

| Função R (MicrosoftML) | Função Python (microsoftml) | Uso |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | Gera uma pontuação de sentimentos positiva negativa sobre entradas de texto. |
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Extrai informações de texto de entradas de arquivo de imagem. |

## <a name="prerequisites"></a>Pré-requisitos

Os algoritmos de aprendizado de máquina são computacionalmente intensivas. Recomendamos 16 GB de RAM para cargas de trabalho de baixo para moderado, incluindo a conclusão das instruções passo a passos do tutorial usando todos os dados de exemplo.

Você deve ter direitos de administrador no computador e SQL Server adicionar modelos pré-treinados.

Os scripts externos devem ser habilitados e SQL Server serviço LaunchPad deve estar em execução. As instruções de instalação fornecem as etapas para habilitar e verificar esses recursos. 

O pacote [MicrosoftML R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) ou o [pacote Python MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) contém os modelos pré-treinados.

+ [SQL Server 2017 serviços de Machine Learning](sql-machine-learning-services-windows-install.md) inclui versões de idioma da biblioteca do Machine Learning, portanto, esse pré-requisito é atendido sem nenhuma ação adicional de sua parte. Como as bibliotecas estão presentes, você pode usar o script do PowerShell descrito neste artigo para adicionar os modelos pré-treinados a essas bibliotecas.

+ [SQL Server o 2016 r Services](sql-r-services-windows-install.md), que é somente R, não inclui o [pacote MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) pronto. Para adicionar o MicrosoftML, você deve fazer uma [atualização de componente](../install/upgrade-r-and-python.md). Uma vantagem da atualização do componente é que você pode adicionar simultaneamente os modelos pré-treinados, o que torna a execução desnecessária do script do PowerShell. No entanto, se você já fez a atualização, mas perdeu a adição dos modelos pré-treinados na primeira vez, você pode executar o script do PowerShell, conforme descrito neste artigo. Funciona para ambas as versões do SQL Server. Antes de fazer isso, confirme se a biblioteca MicrosoftML existe em C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\library.


<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>Verificar se os modelos pré-treinados estão instalados

Os caminhos de instalação dos modelos R e Python são os seguintes:

+ Para o R:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ Para Python:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

Os nomes de arquivos de modelo são listados abaixo:

+ AlexNet\_atualizado. modelo
+ ImageNet1K\_mean.xml
+ pretreinado. modelo
+ ResNet\_101\_Updated.model
+ ResNet\_18\_Updated.model
+ ResNet\_50\_Updated.model

Se os modelos já estiverem instalados, pule para a [etapa de validação](#verify) para confirmar a disponibilidade.

## <a name="download-the-installation-script"></a>Baixar o script de instalação

Clique [https://aka.ms/mlm4sql](https://aka.ms/mlm4sql) para baixar o arquivo **install-MLModels. ps1**.

## <a name="execute-with-elevated-privileges"></a>Executar com privilégios elevados

1. Inicie o PowerShell. Na barra de tarefas, clique com o botão direito do mouse no ícone do programa PowerShell e selecione **Executar como administrador**.
2. Insira um caminho totalmente qualificado para o arquivo de script de instalação e inclua o nome da instância. Supondo que a pasta downloads e uma instância padrão, o comando pode ser assim:

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**Saída**

Em uma instância padrão conectada à Internet SQL Server 2017 Machine Learning com R e Python, você deverá ver mensagens semelhantes às seguintes.

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

Primeiro, verifique os novos arquivos na [pasta mxlibs](#file-location) Em seguida, execute o código de demonstração para confirmar se os modelos estão instalados e funcionando. 

### <a name="r-verification-steps"></a>Etapas de verificação de R

1. Inicie o **RGUI. EXE** em C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\bin\x64.

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

3. Pressione Enter para exibir as pontuações de sentimentos. A saída deve ser a seguinte:

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

1. Inicie o **Python. exe** em C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES.

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

3. Pressione Enter para imprimir as pontuações. A saída deve ser a seguinte:

    ```python
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> Se os scripts de demonstração falharem, verifique o local do arquivo primeiro. Em sistemas com várias instâncias do SQL Server, ou para instâncias que são executadas lado a lado com versões autônomas, é possível que o script de instalação Leia o ambiente incorretamente e coloque os arquivos no local errado. Normalmente, copiar os arquivos manualmente para a pasta mxlib correta corrige o problema.

## <a name="examples-using-pre-trained-models"></a>Exemplos usando modelos pré-treinados

O link a seguir inclui o código de exemplo que invoca os modelos pretreinados.

+ [Exemplo de código: Análise de Sentimento usando Featurizer de texto](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>Pesquisa e recursos

Atualmente, os modelos disponíveis são modelos de rede neural profunda (DNN) para análise de sentimentos e classificação de imagem. Todos os modelos pré-treinados foram treinados usando o [Kit de ferramentas de computação de rede](https://cntk.ai/Features/Index.html)da Microsoft ou **CNTK**.

A configuração de cada rede foi baseada nas seguintes implementações de referência:

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

Para obter mais informações sobre os algoritmos usados nesses modelos de aprendizado profundo e como eles são implementados e treinados usando o CNTK, consulte estes artigos:

+ [O algoritmo dos pesquisadores da Microsoft define o Marco ImageNet Challenge](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [O kit de ferramentas de rede computacional da Microsoft oferece um desempenho computacional de aprendizado profundo distribuído mais eficiente](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>Confira também

+ [SQL Server 2016 R Services](sql-r-services-windows-install.md)
+ [SQL Server 2017 Serviços de Machine Learning](sql-machine-learning-services-windows-install.md)
+ [Atualizar os componentes do R e do Python em instâncias de SQL Server](../install/upgrade-r-and-python.md)
+ [Pacote MicrosoftML para R](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [pacote microsoftml para Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
