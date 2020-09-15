---
title: Notebooks do Azure Data Studio (Python, R)
description: Saiba como executar scripts de Python e R em um notebook no Azure Data Studio com os Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/09/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b7f711ae8b90762003f903b7fd4a59771c5d3f53
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178681"
---
# <a name="run-python-and-r-scripts-in-azure-data-studio-notebooks-with-sql-server-machine-learning-services"></a>Execute scripts de Python e R em notebooks no Azure Data Studio com os Serviços de Machine Learning do SQL Server
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

Saiba como executar scripts Python e R em notebooks do [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) com os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md). O Azure Data Studio é uma ferramenta de banco de dados multiplataforma.

## <a name="prerequisites"></a>Pré-requisitos

- [Baixe e instale o Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio) no computador da estação de trabalho. O Azure Data Studio é multiplataforma. Pode ser executado no Windows, no macOS e no Linux.

- Um servidor com Serviços de Machine Learning do SQL Server instalado e habilitado. Você pode usar os Serviços de Machine Learning em Clusters de Big Data, no Windows ou no Linux:

  - [Instalar Serviços de Machine Learning do SQL Server no Windows](sql-machine-learning-services-windows-install.md).
  - [Instalar Serviços de Machine Learning do SQL Server no Linux](../../linux/sql-server-linux-setup-machine-learning.md).
  - [Executar scripts de Python e de R com Serviços de Machine Learning em Clusters de Big Data do SQL Server](../../big-data-cluster/machine-learning-services.md).

## <a name="create-a-sql-notebook"></a>Criar um notebook SQL

> [!IMPORTANT]
> Os Serviços de Machine Learning são executados como parte do SQL Server. Portanto, você precisa usar um kernel de SQL e não um kernel de Python.

Você pode usar os Serviços de Machine Learning no Azure Data Studio com um notebook SQL. Para criar um notebook, siga estas etapas:

1. Clique em **Arquivo** e **Novo notebook** para criar um Notebook. Por padrão, o Notebook usará o **kernel SQL**.

1. Clique em **Anexar a** e **Alterar conexão**. 

    > [!div class="mx-imgBorder"]
    > ![Alterar conexão do Notebook SQL no Azure Data Studio](media/ads-attach-to-connection.png)
    
1. Conecte-se a um SQL Server novo ou existente. Você pode:

    1. Escolher uma conexão existente em **Conexões Recentes** ou **Conexões Salvas**.

    1. Criar uma conexão em **Detalhes da Conexão**. Preencha os detalhes da conexão com o SQL Server e o banco de dados.

    > [!div class="mx-imgBorder"]
    > ![Detalhes da conexão do Notebook SQL no Azure Data Studio](media/ads-connection-details.png)  

## <a name="run-python-or-r-scripts"></a>Executar scripts de Python ou R

Os notebooks SQL consistem em células de código e texto. As células de código são usadas para executar scripts de Python ou R por meio do procedimento armazenado [sp_execute_external_scripts](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). As células de texto podem ser usadas para documentar seu código no notebook.

### <a name="run-a-python-script"></a>Executar um script do Python

Siga estas etapas para executar um script de Python:

1. Clique em **+ Código** para adicionar uma célula de código.

    > [!div class="mx-imgBorder"]
    > ![Adicionar bloco de código de notebooks SQL do Azure Data Studio](media/ads-add-code.png)  

1. Insira o script a seguir na célula de código:

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

1. Clique em **Executar célula** (a seta preta redonda) ou pressione **F5** para executar a única célula.

    > [!div class="mx-imgBorder"]
    > ![Executar código de Python em notebooks SQL do Azure Data Studio](media/ads-run-python.png)  

1. O resultado será mostrado sob a célula de código.

    > [!div class="mx-imgBorder"]
    > ![Saída código de Python em Notebook SQL do Azure Data Studio](media/ads-run-python-output.png)  

### <a name="run-an-r-script"></a>Executar um script de R

Siga estas etapas para executar um script de R:

1. Clique em **+ Código** para adicionar uma célula de código.

    > [!div class="mx-imgBorder"]
    > ![Adicionar bloco de código de notebooks SQL do Azure Data Studio](media/ads-add-code.png)  

1. Insira o script a seguir na célula de código:

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

1. Clique em **Executar célula** (a seta preta redonda) ou pressione **F5** para executar a única célula.

    > [!div class="mx-imgBorder"]
    > ![Executar código de R em notebooks SQL do Azure Data Studio](media/ads-run-r.png)  

1. O resultado será mostrado sob a célula de código.

    > [!div class="mx-imgBorder"]
    > ![Saída de código de R em Notebook SQL do Azure Data Studio](media/ads-run-r-output.png)  

## <a name="next-steps"></a>Próximas etapas

- [Como usar notebooks no Azure Data Studio](../../azure-data-studio/notebooks-guidance.md)
- [Criar e executar um notebook do SQL Server](../../azure-data-studio/notebooks-tutorial-sql-kernel.md)
- [Início Rápido: executar scripts de Python simples com os Serviços de Machine Learning do SQL Server](../tutorials/quickstart-python-create-script.md)
- [Início Rápido: executar scripts de R simples com os Serviços de Machine Learning do SQL Server](../tutorials/quickstart-r-create-script.md)
