---
title: "Instalar os modelos de aprendizado de máquina pré-treinado no SQL Server | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 14789bafd555a4980875de78c85b32f535a8c0fe
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>Instalar pré-treinado modelos no SQL Server de aprendizado de máquina

Este tópico descreve como adicionar modelos pré-treinado a uma instância do SQL Server que já tem o R Services ou serviços de aprendizado de máquina instalado.

Pré-treinado modelos são fornecidos com a atualização para o Microsoft R Server (ou a atualização do Microsoft Server de aprendizado de máquina). Para obter informações sobre como atualizar a instância e obter a versão mais recente do Microsoft R, consulte [atualizar os componentes de R em uma instância dos serviços do R](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

Você pode instalar esses modelos apenas ao executar o instalador de baseados em Windows separado para R Server.
No entanto, há algumas etapas adicionais para usar ao instalar os modelos no SQL Server. Este tópico descreve o processo.

## <a name="benefits-of-using-pretrained-models"></a>Benefícios do uso de modelos de pré-treinado

Modelos previamente treinados estavam disponíveis para dar suporte a clientes que precisam executar tarefas, como análise de sentimento ou personalização de imagem, mas não tiver os recursos para obter os conjuntos de dados grandes ou treinar um modelo complexo. Usando modelos previamente treinados permite começar em texto e imagem, processamento de forma mais eficiente.

Atualmente, os modelos que estão disponíveis são modelos de rede neurais profundas (DNN) para classificação de imagem e análise de sentimento. Todos os quatro modelos pré-treinado foram treinados CNTK. A configuração de cada rede baseia as implementações de referência a seguir:

+ Resnet-18
+ 50 Resnet
+ ResNet 101
+ AlexNet

Para obter mais informações sobre redes profundas residuais e sua implementação usando CNTK, consulte estes artigos:

+ [Algoritmo os pesquisadores da Microsoft define marco ImageNet desafio](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Kit de ferramentas de rede computacional Microsoft oferece mais eficiente profundo distribuído desempenho computacional de aprendizado](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-install-the-models-on-sql-server"></a>Como instalar os modelos no SQL Server

   > [!NOTE]
   > 
   > Se você usar o instalador separado baseado no Windows para instalar o Microsoft R Server ou atualize sua instância do SQL Server, os modelos pré-treinado estão disponíveis do instalador. Consulte [instalar R Server para Windows](https://docs.microsoft.com/en-us/r-server/install/r-server-install-windows).
   > 
   > Algumas etapas adicionais podem ser necessárias para usar os modelos com o Microsoft R Server. Para obter mais informações, consulte [como instalar e implantar previamente treinado modelos de aprendizado de máquina com MicrosoftML](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models)

1. Os modelos pré-treinado não são instalados por padrão quando você instala o SQL Server. Você deve adicioná-los ao executar um utilitário de linha de comando de instalação após a instalação do SQL Server.

2. Abra um prompt de comando com privilégios elevados e navegue até a pasta de inicialização de instalação do SQL Server, que também contém o instalador do Microsoft R.

    Uma instância padrão do SQL Server de 2017 RC 1, isso seria:
    
    `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\SQL2017RC1\x64\`

3. Especifique o componente a ser instalado e a pasta onde os modelos pré-treinado devem ser adicionados, usando os seguintes argumentos:

  + Para usar modelos com **R_SERVICES**

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\R_SERVICES`

    Por exemplo, para permitir o uso dos modelos de pré-treinado usando o R em uma instância padrão do SQL Server 2017, você executaria esta instrução:

    `RSetup.exe /install /component MLM /version 9.2.0.22 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES"`

  + Para usar modelos com **PYTHON_SERVICES**

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\PYTHON_SERVICES`

    Por exemplo, para permitir o uso dos modelos de pré-treinado usando Python, para uma instância padrão do SQL Server de 2017, você executaria esta instrução:

    `RSetup.exe /install /component MLM /version 9.2.0.22 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES"`

4. Para o parâmetro de versão, há suporte para os seguintes valores:

    + Versão Release candidate 0: **9.1.0.0**
    + Versão Release candidate 1: **9.2.0.22**
    + Número de versão final (não lançado): **9.2.0.100**

5. Se a instalação for bem-sucedida, os modelos a seguir devem ser adicionados ao seu R\_serviços ou PYTHON\_pastas de serviços:

    - AlexNet_Updated.model
    - ImageNet1K_mean.xml
    - pretrained.Model
    - ResNet_101_Updated.model
    - ResNet_18_Updated.model
    - ResNet_50_Updated.model

## <a name="examples"></a>Exemplos

Depois de ter instalado os modelos, você pode usar os modelos chamando-los a partir de código R.

### <a name="image-featurization-example"></a>Exemplo de personalização de imagem

O modelo pré-treinado para imagens dá suporte a personalização de imagens que você fornecer. Para usar o modelo, você deve chamar o **featurizeImage** transformação.

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
> 
> Não é possível ler ou modificar o modelo pré-treinado em si. Esse modelo específico se baseia [CNTK](https://docs.microsoft.com/cognitive-toolkit/) de modelo, mas foi compactada usando um formato nativo por motivos de desempenho.

### <a name="text-analysis-example"></a>Exemplo de análise de texto

Este exemplo demonstra o uso do modelo pré-treinado para classificação:

[Análise de sentimento usando o recurso de texto](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)
