---
title: Gerenciar pacotes com a extensão de Machine Learning
titleSuffix: Azure Data Studio
description: Saiba como gerenciar pacotes do Python ou do R no banco de dados com a extensão de Machine Learning para Azure Data Studio.
ms.date: 05/19/2020
ms.reviewer: sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 0fdd781e26597e1c188ce08c1df9852c39aaecec
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88745476"
---
# <a name="manage-packages-in-database-with-machine-learning-extension-preview-for-azure-data-studio"></a>Gerenciar pacotes no banco de dados com a extensão de Machine Learning (versão prévia) para Azure Data Studio

Saiba como gerenciar pacotes do Python ou do R no banco de dados com a [extensão de Machine Learning para Azure Data Studio](machine-learning-extension.md).

> [!IMPORTANT]
> Gerenciar pacotes no banco de dados com a extensão de Machine Learning atualmente só é compatível com os [Serviços de Machine Learning](../machine-learning/sql-server-machine-learning-services.md) no SQL Server 2019.

## <a name="prerequisites"></a>Pré-requisitos

- Instale e configure a [extensão de Machine Learning para Azure Data Studio](machine-learning-extension.md). Você precisa especificar os [caminhos de instalação do Python ou do R nas Configurações da Extensão](machine-learning-extension.md#settings) para que o gerenciamento de pacotes funcione.

- O pacote **sqlmlutils**. Se o pacote ainda não estiver instalado, a extensão de Machine Learning solicitará que você o instale.

- A Autenticação do Windows não é compatível com o SQL Server em Linux. Portanto, você precisa usar a autenticação do SQL para se conectar ao SQL Server em Linux.

## <a name="manage-python-packages"></a>Gerenciar pacotes do Python

Você pode instalar e desinstalar pacotes do Python com a extensão de Machine Learning.

### <a name="install-new-python-package"></a>Instalar novo pacote do Python

Siga as etapas abaixo para instalar pacotes do Python no banco de dados.

1. Clique em **Gerenciar pacotes no banco de dados**.

1. Se for solicitado que você instale o **sqlmlutils**, clique em **Sim**.

1. Na guia **Instalados**, selecione **Python** no **Tipo de pacote** e selecione o banco de dados em **Localização**.

1. Clique na guia **Adicionar**.

1. Insira o pacote do Python que você deseja instalar em **Pesquisar pacotes do Python** e clique em **Pesquisar**.

1. Verifique se o pacote está listado em **Nome do pacote** e se a versão desejada está listada em **Versão do pacote**.

1. Clique em **Instalar**.

1. Clique em **Fechar** e verifique se o pacote foi instalado com sucesso em **Tarefas**.

### <a name="uninstall-a-python-package"></a>Desinstalar um pacote do Python

Siga as etapas abaixo para desinstalar pacotes do Python no banco de dados.

> [!NOTE]
> Você só poderá desinstalar pacotes que foram instalados no seu banco de dados. Não é possível desinstalar um pacote que tenha sido pré-instalado com os Serviços de Machine Learning do SQL Server.

1. Clique em **Gerenciar pacotes no banco de dados**.

1. Se for solicitado que você instale o **sqlmlutils**, clique em **Sim**.

1. Na guia **Instalados**, selecione **Python** no **Tipo de pacote** e selecione o banco de dados em **Localização**.

1. Selecione os pacotes que você deseja desinstalar.

1. Clique em **Desinstalar os pacotes selecionados**.

1. Clique em **Fechar** e verifique se o pacote foi instalado com sucesso em **Tarefas**.

## <a name="manage-r-packages"></a>Gerenciar pacotes do R

Você pode instalar e desinstalar pacotes do R com a extensão de Machine Learning.

### <a name="install-new-r-package"></a>Instalar novos pacote do R

Siga as etapas abaixo para instalar pacotes do Python no banco de dados.

1. Clique em **Gerenciar pacotes no banco de dados**.

1. Se for solicitado que você instale o **sqlmlutils**, clique em **Sim**.

1. Na guia **Instalados**, selecione **R** no **Tipo de pacote** e selecione o banco de dados em **Localização**.

1. Clique na guia **Adicionar**.

1. Insira o pacote do R que você deseja instalar em **Pesquisar pacotes do R** e clique em **Pesquisar**.

1. Verifique se o pacote está listado em **Nome do pacote** e se a versão desejada está listada em **Versão do pacote**.

1. Clique em **Instalar**.

1. Clique em **Fechar** e verifique se o pacote foi instalado com sucesso em **Tarefas**.

### <a name="uninstall-an-r-package"></a>Desinstalar um pacote do R

Siga as etapas abaixo para desinstalar pacotes do R no banco de dados.

> [!NOTE]
> Você só poderá desinstalar pacotes que foram instalados no seu banco de dados. Não é possível desinstalar um pacote que tenha sido pré-instalado com os Serviços de Machine Learning do SQL Server.

1. Clique em **Gerenciar pacotes no banco de dados**.

1. Se for solicitado que você instale o **sqlmlutils**, clique em **Sim**.

1. Na guia **Instalados**, selecione **R** no **Tipo de pacote** e selecione o banco de dados em **Localização**.

1. Selecione os pacotes que você deseja desinstalar.

1. Clique em **Desinstalar os pacotes selecionados**.

1. Clique em **Fechar** e verifique se o pacote foi instalado com sucesso em **Tarefas**.

## <a name="next-steps"></a>Próximas etapas

- [Extensão do Machine Learning no Azure Data Studio](machine-learning-extension.md)
- [Fazer previsões](machine-learning-extension-predictions.md)
- [Importar ou exibir modelos](machine-learning-extension-import-view-models.md)
- [Notebooks no Azure Data Studio](notebooks-guidance.md)
- [Documentação do machine learning do SQL](../machine-learning/index.yml)
