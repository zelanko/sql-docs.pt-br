---
title: Extensão de Machine Learning (versão prévia)
titleSuffix: Azure Data Studio
description: A extensão de Machine Learning para Azure Data Studio permite que você gerencie pacotes, importe modelos de machine learning, faça previsões e crie notebooks para executar experimentos nos bancos de dados SQL.
ms.date: 05/19/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 5b54ec71ec3debaf39b0788cac0c1534300a4a72
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88745546"
---
# <a name="machine-learning-extension-preview-for-azure-data-studio"></a>Extensão de Machine Learning (versão prévia) para Azure Data Studio

A extensão de Machine Learning para [Azure Data Studio](what-is.md) permite que você gerencie pacotes, importe modelos de machine learning, faça previsões e crie notebooks para executar experimentos nos bancos de dados SQL. Esta extensão está em versão prévia.

## <a name="prerequisites"></a>Pré-requisitos

Os pré-requisitos a seguir precisam ser instalados no computador em que o Azure Data Studio é executado.

- [Python 3](https://www.python.org/downloads/). Depois de instalar o Python, você precisará especificar o caminho local para uma instalação do Python em [Configurações da extensão](#settings). Se você usou um [notebook do kernel do Python](notebooks-tutorial-python-kernel.md) no Azure Data Studio, a extensão usará o caminho do notebook por padrão.

- [Driver ODBC 17 da Microsoft para SQL Server](../connect/odbc/download-odbc-driver-for-sql-server.md) para Windows, macOS ou Linux.

- [R 3.5](https://www.r-project.org/) (opcional). No momento, não há suporte para outra versão diferente da 3.5. Depois de instalar o R 3.5, você precisará habilitar o R e especificar o caminho local para uma instalação do R em [Configurações da extensão](#settings). Isso só será necessário se você quiser gerenciar pacotes do R no banco de dados.

### <a name="trouble-installing-python-3-from-within-ads"></a>Problemas ao instalar o Python 3 por meio do ADS?
Se você tentar instalar o Python 3, mas receber um erro sobre o TLS/SSL, adicione estes dois componentes opcionais:

_exemplo de erro:_
```
$: ~/0.0.1/bin/python3 -m pip install --user "jupyter>=1.0.0" --extra-index-url https://prose-python-packages.azurewebsites.net
WARNING: pip is configured with locations that require TLS/SSL, however the ssl module in Python is not available.
Looking in indexes: https://pypi.org/simple, https://prose-python-packages.azurewebsites.net
Requirement already satisfied: jupyter
```

_instale estes itens:_

- [Homebrew](https://brew.sh) (opcional). Instale o Homebrew e execute `brew update` na linha de comando.

- *OpenSSL* (opcional). Em seguida, execute `brew install openssl`.

## <a name="install-the-extension"></a>Instalar a extensão

Para instalar a extensão de Machine Learning no Azure Data Studio, siga as etapas abaixo.

1. Abra o gerenciador de extensões no Azure Data Studio. Você poderá selecionar o ícone de extensões ou selecionar Extensões no menu Exibir.

1. Selecione a extensão de **Machine Learning** e veja os detalhes.

1. Clique em **Instalar**.

1. Clique em **Recarregar** para habilitar a extensão. Isso só será necessário na primeira vez que você instalar uma extensão.

<a name="settings"></a>

## <a name="extension-settings"></a>Configurações da extensão

Para alterar as configurações da extensão de Machine Learning, siga as etapas abaixo.

1. Abra o gerenciador de extensões no Azure Data Studio. Você poderá selecionar o ícone de extensões ou selecionar Extensões no menu Exibir.

1. Localize a extensão de **Machine Learning** dentre as extensões **habilitadas**.

1. Clique no ícone **Gerenciar**.

1. Clique no ícone **Configurações da extensão**.

As configurações das extensões se parecem com esta:

:::image type="content" source="media/machine-learning-extension/ml-extension-settings.png" alt-text="Configurações da extensão de Machine Learning":::

### <a name="enable-python"></a>Habilitar Python

Para usar a extensão de Machine Learning, bem como o gerenciamento de pacotes do Python no banco de dados, siga as etapas abaixo.

> [!IMPORTANT]
> A extensão de Machine Learning requer que o Python seja habilitado e configurado para a maioria das funcionalidades funcionar, mesmo que você não queira usar o gerenciamento de pacotes do Python na funcionalidade do banco de dados.

1. Verifique se **Machine Learning: habilitar Python** está habilitada. Essa configuração é habilitada por padrão.

1. Forneça o caminho para a instalação do Python pré-existente em **Machine Learning: caminho do Python**. Esse pode ser o caminho completo para o executável do Python ou a pasta em que o executável está. Se você usou um [notebook do kernel do Python](notebooks-tutorial-python-kernel.md) no Azure Data Studio, a extensão usará o caminho do notebook por padrão.

### <a name="enable-r"></a>Habilitar R

Para usar a extensão de Machine Learning para o gerenciamento de pacotes do R no banco de dados, siga as etapas abaixo.

1. Verifique se **Machine Learning: habilitar R** está habilitada. Essa configuração é desabilitada por padrão.

1. Fornecer o caminho para a instalação do R pré-existente em **Machine Learning: caminho do R**. Deve ser o caminho completo para o executável do R. 

## <a name="use-the-machine-learning-extension"></a>Usar a extensão de Machine Learning

Para usar a extensão de Machine Learning no Azure Data Studio, siga as etapas abaixo.

1. Abra as conexões no Azure Data Studio.

1. Clique com o botão direito do mouse no servidor e selecione **Gerenciar**.

1. Clique em **Machine Learning** no menu do lado esquerdo em **Geral**.

Siga os links em **Próximas etapas** para ver como você pode usar a extensão de Machine Learning para gerenciar pacotes, fazer previsões e importar modelos no banco de dados.

## <a name="next-steps"></a>Próximas etapas

- [Gerenciar pacotes no banco de dados](machine-learning-extension-manage-packages.md)
- [Fazer previsões](machine-learning-extension-predictions.md)
- [Importar ou exibir modelos](machine-learning-extension-import-view-models.md)
- [Notebooks no Azure Data Studio](notebooks-guidance.md)
- [Documentação do machine learning do SQL](../machine-learning/index.yml)
- [Machine learning e IA com o ONNX no SQL no Edge (versão prévia)](/azure/azure-sql-edge/onnx-overview)
