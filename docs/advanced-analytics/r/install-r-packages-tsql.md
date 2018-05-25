---
title: Use T-SQL (criar biblioteca externa) para instalar pacotes R nos serviços de aprendizado de máquina do SQL Server | Microsoft Docs
description: Adicionar novos pacotes de R para serviços do aprendizado de máquina 2017 SQL Server (no banco de dados)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/20/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bbc1adf4868cbfbd02afe5cae3a38fd6223e2d4d
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server-2017-machine-learning-services"></a>Use T-SQL (criar biblioteca externa) para instalar pacotes R nos serviços de aprendizado de máquina do SQL Server de 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como instalar novos pacotes de R em uma instância do SQL Server onde o aprendizado de máquina está habilitado. Há várias abordagens para escolher. Essa abordagem funciona melhor para os administradores de servidor que não estão familiarizados com R.

**Aplica-se a:**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

O [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrução, é possível adicionar um pacote ou conjunto de pacotes para uma instância ou um banco de dados sem executar R ou Python code diretamente. No entanto, esse método requer permissões de banco de dados adicionais e preparação de pacote.

+ Todos os pacotes devem estar disponível como um arquivo compactado local, em vez de download sob demanda da internet.

+ Todas as dependências devem ser identificadas pelo nome e a versão e incluídas no arquivo zip. A instrução falhará se pacotes requeridos não estão disponíveis, incluindo as dependências do pacote de downstream. 

+ Você deve ter as permissões necessárias no banco de dados. Para obter detalhes, consulte [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="download-packages-in-archive-format"></a>Baixe os pacotes no formato de arquivo

Se você estiver instalando um único pacote, baixe o pacote em formato compactado.

Se o pacote exige que todos os outros pacotes, você deve verificar se os pacotes necessários estão disponíveis. Você pode usar miniCRAN para analisar o pacote de destino e identificar todas as suas dependências. É recomendável usar [ **miniCRAN** ](create-a-local-package-repository-using-minicran.md) ou [ **igraph** ](http://igraph.org/r/) para análise de dependências de pacotes. Instalando a versão incorreta do pacote ou de dependência de pacote também pode causar a falha da instrução. 

## <a name="copy-the-file-to-a-local-folder"></a>Copie o arquivo para uma pasta local

Copie o arquivo compactado que contém todos os pacotes em uma pasta local no servidor. Se você não tiver acesso ao sistema de arquivos no servidor, você também pode passar um pacote completo como uma variável, usando um formato binário. Para obter mais informações, consulte [criar biblioteca externa](../../t-sql/statements/create-external-library-transact-sql.md).

## <a name="run-the-statement-to-upload-packages"></a>Execute a instrução para carregar pacotes

Abra um **consulta** janela, usando uma conta com privilégios administrativos.

Execute a instrução T-SQL `CREATE EXTERNAL LIBRARY` para carregar a coleção de pacote compactado para o banco de dados.

    For example, the following statement names as the package source a miniCRAN repository containing the **randomForest** package, together with its dependencies. 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    You cannot use an arbitrary name; the external library name must have the same name that you expect to use when loading or calling the package.

## <a name="verify-package-installation"></a>Verificar a instalação do pacote

Se a biblioteca é criada com êxito, você pode executar o pacote no SQL Server, chamando-o dentro de um procedimento armazenado.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    library(randomForest)'
    ```

