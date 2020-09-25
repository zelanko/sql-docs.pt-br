---
title: Gerenciar pacotes com a extensão de Machine Learning
description: Saiba como gerenciar pacotes do Python ou do R no banco de dados com a extensão de Machine Learning para Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.reviewer: sstein
ms.custom: ''
ms.date: 05/19/2020
ms.openlocfilehash: c965bc4bd9c6b235d192db58c82fac41f4f8b532
ms.sourcegitcommit: e3460309b301a77d0babec032f53de330da001a9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91136612"
---
# <a name="manage-packages-in-database-with-machine-learning-extension-for-azure-data-studio-preview"></a>Gerenciar pacotes no banco de dados com a extensão de Machine Learning para Azure Data Studio (versão prévia)

Saiba como gerenciar pacotes do Python ou do R no banco de dados com a [extensão de Machine Learning para Azure Data Studio](machine-learning-extension.md).

> [!IMPORTANT]
> Gerenciar pacotes no banco de dados com a extensão de Machine Learning atualmente só é compatível com os [Serviços de Machine Learning](../../machine-learning/sql-server-machine-learning-services.md) no SQL Server 2019.

## <a name="prerequisites"></a>Pré-requisitos

- Instale e configure a [extensão de Machine Learning para Azure Data Studio](machine-learning-extension.md). Você precisa especificar os [caminhos de instalação do Python ou do R nas Configurações da Extensão](machine-learning-extension.md#settings) para que o gerenciamento de pacotes funcione.

- O pacote **sqlmlutils**. Se o pacote ainda não estiver instalado, a extensão de Machine Learning solicitará que você o instale.

- A Autenticação do Windows não é compatível com o SQL Server em Linux. Portanto, você precisa usar a autenticação do SQL para se conectar ao SQL Server em Linux.

## <a name="manage-python-packages"></a>Gerenciar pacotes do Python

Você pode instalar e desinstalar pacotes do Python com a extensão de Machine Learning.

### <a name="install-new-python-package"></a>Instalar novo pacote do Python

Siga as etapas abaixo para instalar pacotes do Python no banco de dados.

1. Selecione **Gerenciar pacotes no banco de dados**.

1. Se for solicitado que você instale o **sqlmlutils**, selecione **Sim**.

1. Na guia **Instalados**, selecione **Python** no **Tipo de pacote** e selecione o banco de dados em **Localização**.

1. Selecione a guia **Adicionar**.

1. Insira o pacote do Python que você deseja instalar em **Pesquisar pacotes do Python** e selecione **Pesquisar**.

1. Verifique se o pacote está listado em **Nome do pacote** e se a versão desejada está listada em **Versão do pacote**.

1. Selecione **Instalar**.

1. Selecione **Fechar** e verifique se o pacote foi instalado com sucesso em **Tarefas**.

### <a name="uninstall-a-python-package"></a>Desinstalar um pacote do Python

Siga as etapas abaixo para desinstalar pacotes do Python no banco de dados.

> [!NOTE]
> Você só poderá desinstalar pacotes que foram instalados no seu banco de dados. Não é possível desinstalar um pacote que tenha sido pré-instalado com os Serviços de Machine Learning do SQL Server.

1. Selecione **Gerenciar pacotes no banco de dados**.

1. Se for solicitado que você instale o **sqlmlutils**, selecione **Sim**.

1. Na guia **Instalados**, selecione **Python** no **Tipo de pacote** e selecione o banco de dados em **Localização**.

1. Selecione os pacotes que você deseja desinstalar.

1. Selecione **Desinstalar pacotes selecionados**.

1. Selecione **Fechar** e verifique se o pacote foi instalado com sucesso em **Tarefas**.

## <a name="manage-r-packages"></a>Gerenciar pacotes do R

Você pode instalar e desinstalar pacotes do R com a extensão de Machine Learning.

### <a name="install-new-r-package"></a>Instalar novos pacote do R

Siga as etapas abaixo para instalar pacotes do Python no banco de dados.

1. Selecione **Gerenciar pacotes no banco de dados**.

1. Se for solicitado que você instale **sqlmlutils**, selecione **Sim**.

1. Na guia **Instalados**, selecione **R** no **Tipo de pacote** e selecione o banco de dados em **Localização**.

1. Selecione a guia **Adicionar**.

1. Insira o pacote do R que deseja instalar em **Pesquisar pacotes do R** e selecione **Pesquisar**.

1. Verifique se o pacote está listado em **Nome do pacote** e se a versão desejada está listada em **Versão do pacote**.

1. Selecione **Instalar**.

1. Selecione **Fechar** e verifique se o pacote foi instalado com sucesso em **Tarefas**.

### <a name="uninstall-an-r-package"></a>Desinstalar um pacote do R

Siga as etapas abaixo para desinstalar pacotes do R no banco de dados.

> [!NOTE]
> Você só poderá desinstalar pacotes que foram instalados no seu banco de dados. Não é possível desinstalar um pacote que tenha sido pré-instalado com os Serviços de Machine Learning do SQL Server.

1. Selecione **Gerenciar pacotes no banco de dados**.

1. Se for solicitado que você instale **sqlmlutils**, selecione **Sim**.

1. Na guia **Instalados**, selecione **R** no **Tipo de pacote** e selecione o banco de dados em **Localização**.

1. Selecione os pacotes que você deseja desinstalar.

1. Selecione **Desinstalar pacotes selecionados**.

1. Selecione **Fechar** e verifique se o pacote foi instalado com sucesso em **Tarefas**.

## <a name="next-steps"></a>Próximas etapas

- [Extensão do Machine Learning no Azure Data Studio](machine-learning-extension.md)
- [Fazer previsões](machine-learning-extension-predictions.md)
- [Importar ou exibir modelos](machine-learning-extension-import-view-models.md)
- [Notebooks no Azure Data Studio](../notebooks-guidance.md)
- [Documentação do machine learning do SQL](../../machine-learning/index.yml)
