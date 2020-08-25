---
title: Fazer previsões com a extensão Machine Learning
titleSuffix: Azure Data Studio
description: Saiba como usar a extensão Machine Learning para Azure Data Studio a fim de fazer previsões com um modelo ONNX no banco de dados.
ms.date: 06/09/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 5472f4ff32a807b58091fd56f3382aa73ead142e
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88745486"
---
# <a name="make-predictions-with-machine-learning-extension-preview-for-azure-data-studio"></a>Faça previsões com a extensão Machine Learning (versão prévia) para Azure Data Studio

Saiba como usar a [extensão Machine Learning para Azure Data Studio](machine-learning-extension.md) a fim de fazer previsões com um modelo ONNX no banco de dados. A extensão gerará um script T-SQL usando o [PREDICT](../t-sql/queries/predict-transact-sql.md) para fazer previsões sobre o conjunto de dados armazenado na tabela com um modelo previamente importado, que reside em um arquivo local ou do Azure Machine Learning.

> [!IMPORTANT]
> As previsões com a extensão Machine Learning atualmente são compatíveis apenas com os [Serviços de Machine Learning na Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview) e o [SQL do Azure no Edge com ONNX](/azure/azure-sql-edge/onnx-overview).

## <a name="prerequisites"></a>Pré-requisitos

- Instale e configure a [extensão de Machine Learning para Azure Data Studio](machine-learning-extension.md). Você precisa especificar os [caminhos de instalação do Python nas Configurações da Extensão](machine-learning-extension.md#settings).

- Os pacotes **onnxruntime**, **mlflow** e **mlflow-dbstore** do Python. Se os pacotes ainda não estiverem instalados, a extensão de Machine Learning solicitará que você os instale.

## <a name="make-predictions-from-onnx-model"></a>Fazer previsões com base no modelo ONNX

Siga as etapas abaixo para usar um modelo ONNX para fazer previsões.

1. Clique em **Fazer previsões**.

1. Se for solicitado que você instale o **onnxruntime**, o **mlflow** e o **mlflow-dbstore**, clique em **Sim**.

1. Escolha onde seu modelo está localizado e clique em **Próximo**. Você pode usar:
    - **Modelos importados**. Escolha esta opção para usar um modelo que já está armazenado no banco de dados. Escolha o **Modelo de banco de dados** e a **Tabela modelo** em que o modelo está localizado, selecione o modelo que deseja usar e clique em **Próximo**.
    - **Upload de arquivo**. Escolha esta opção para usar um modelo de um arquivo. Selecione o arquivo de modelo em **Arquivos de origem** e clique em **Próximo**.
    - **Azure Machine Learning**. Escolha esta opção para usar um modelo do Azure Machine Learning. Primeiro, **entre no Azure**. Em seguida, selecione a **Conta do Azure**, a **Assinatura do Azure**, o **Grupo de recursos do Azure** e o **Workspace do Azure ML**. Selecione o modelo que deseja usar e clique em **Próximo**.

1. Mapeie os dados de origem para o modelo.
    - Selecione o **banco de dados de origem** e a **tabela de origem** que contêm o conjunto de dados ao qual você deseja aplicar a previsão.
    - Mapeie as colunas em **Mapeamento da entrada do modelo** e **saída do modelo**. A extensão mapeará automaticamente as colunas que tiverem o mesmo nome e tipo de dados.

1. Clique em **Prever**.

O Azure Data Studio criará uma consulta T-SQL com o [PREDICT](../t-sql/queries/predict-transact-sql.md), que você poderá usar para fazer previsões sobre os dados.

## <a name="next-steps"></a>Próximas etapas

- [Extensão do Machine Learning no Azure Data Studio](machine-learning-extension.md)
- [Gerenciar pacotes no banco de dados](machine-learning-extension-manage-packages.md)
- [Importar ou exibir modelos](machine-learning-extension-import-view-models.md)
- [Notebooks no Azure Data Studio](notebooks-guidance.md)
- [Documentação do machine learning do SQL](../machine-learning/index.yml)
- [Serviços de Machine Learning na Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview)
- [Machine learning e IA com o ONNX no SQL no Edge (versão prévia)](/azure/azure-sql-edge/onnx-overview)
