---
title: Importar ou exibir modelos com a extensão de Machine Learning
titleSuffix: Azure Data Studio
description: Saiba como usar a extensão de Machine Learning para Azure Data Studio a fim de importar um modelo ONNX ou exibir modelos já importados no banco de dados.
ms.date: 06/09/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 3c5faa821ecd9adcfcea426f88a388a6f7d10f27
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901048"
---
# <a name="import-or-view-models-with-machine-learning-extension-preview-for-azure-data-studio"></a>Importar ou exibir modelos com a extensão de Machine Learning (versão prévia) para Azure Data Studio

Saiba como usar a [extensão de Machine Learning para Azure Data Studio](machine-learning-extension.md) a fim de importar um modelo ONNX ou exibir modelos já importados no banco de dados.

> [!IMPORTANT]
> Importar e exibir em um banco de dados com a extensão de Machine Learning atualmente é compatível apenas com os [Serviços de Machine Learning na Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview) e o [SQL do Azure no Edge com ONNX](/azure/azure-sql-edge/onnx-overview).

## <a name="prerequisites"></a>Pré-requisitos

- Instale e configure a [extensão de Machine Learning para Azure Data Studio](machine-learning-extension.md). Você precisa especificar os [caminhos de instalação do Python nas Configurações da Extensão](machine-learning-extension.md#settings).

- Os pacotes **onnxruntime**, **mlflow** e **mlflow-dbstore** do Python. Se os pacotes ainda não estiverem instalados, a extensão de Machine Learning solicitará que você os instale.

## <a name="view-models"></a>Exibir modelos

Siga as etapas abaixo para ver os modelos de ONNX que estão armazenados no banco de dados.

1. Clique em **Importar ou exibir modelos**.

1. Se for solicitado que você instale o **onnxruntime**, o **mlflow** e o **mlflow-dbstore**, clique em **Sim**.

1. Selecione o **Banco de dados de modelos** e a **Tabela de modelos** em que os modelos estão armazenados.

Isso mostrará uma lista de modelos. Você pode editar o nome e a descrição do modelo ou excluir um modelo da lista.

## <a name="import-a-new-model"></a>Importar um novo modelo

Siga as etapas abaixo para importar um modelo ONNX no banco de dados.

1. Clique em **Importar ou exibir modelos**.

1. Se for solicitado que você instale o **onnxruntime**, o **mlflow** e o **mlflow-dbstore**, clique em **Sim**.

1. Clique em **Importar modelos**.

1. Selecione o **Banco de dados de modelos** em que deseja armazenar o modelo importado.

1. Selecione a **Tabela de modelos** em que deseja armazenar o modelo importado. Você pode escolher uma **Tabela existente** ou **Criar uma tabela**. Clique em **Próximo**.

1. Selecione onde seu modelo está localizado e clique em **Próximo**. Você pode usar:
    - **Upload de arquivo**. Escolha esta opção para usar um modelo de um arquivo. Selecione o arquivo de modelo em **Arquivos de origem** e clique em **Próximo**.
    - **Azure Machine Learning**. Escolha esta opção para usar um modelo do Azure Machine Learning. Primeiro, **entre no Azure**. Em seguida, selecione a **Conta do Azure**, a **Assinatura do Azure**, o **Grupo de recursos do Azure** e o **Workspace do Azure ML**. Selecione o modelo que deseja usar e clique em **Próximo**.

1. Insira o **Nome** e a **Descrição** do modelo e clique em **Implantar** para armazenar o modelo no banco de dados.

> [!NOTE]
> Atualmente, a extensão de Machine Learning está em versão prévia. Portanto, o esquema de tabela em que os modelos estão armazenados pode ser alterado no futuro.

## <a name="next-steps"></a>Próximas etapas

- [Extensão do Machine Learning no Azure Data Studio](machine-learning-extension.md)
- [Gerenciar pacotes no banco de dados](machine-learning-extension-manage-packages.md)
- [Fazer previsões](machine-learning-extension-predictions.md)
- [Documentação do machine learning do SQL](../machine-learning/index.yml)
- [Serviços de Machine Learning na Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview)
- [Machine learning e IA com o ONNX no SQL no Edge (versão prévia)](/azure/azure-sql-edge/onnx-overview)
