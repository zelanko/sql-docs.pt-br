---
title: Guia de início rápido para verificar R existe no SQL Server
description: Guia de início rápido para verificar o R e Machine Learning Services existem no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2bd9e43232b77bc77611b0c4cd5285b69c9a6261
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046737"
---
# <a name="quickstart-verify-r-exists-in-sql-server"></a>Guia de início rápido: Verifique se que existe de R no SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server inclui o suporte à linguagem de R para análises de ciência de dados em dados do SQL Server residentes. Seu script R pode consistir em funções de R de código-fonte aberto, bibliotecas de R de terceiros ou bibliotecas internas do Microsoft R, como [RevoScaleR](../r/revoscaler-overview.md) para análise preditiva em grande escala.

Execução do script é por meio de procedimentos armazenados, usando qualquer uma das seguintes abordagens:

+ Interna [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) procedimento armazenado, passando o script R no como um parâmetro de entrada.
+ Encapsular o script de R em um [procedimento armazenado de personalizado](sqldev-in-database-r-for-sql-developers.md) criado por você.

Neste início rápido, você verificará que [serviços do SQL Server 2017 Machine Learning](../what-is-sql-server-machine-learning.md) ou [SQL Server 2016 R Services](../r/sql-server-r-services.md) está instalado e configurado.

## <a name="prerequisites"></a>Prerequisites

Este exercício exige o acesso a uma instância do SQL Server com um dos seguintes já instalados:

+ [Serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md), com a linguagem R instalada
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

Instância do SQL Server pode estar em uma máquina virtual do Azure ou no local. Apenas lembre-se de que o recurso de script externo é desabilitado por padrão, portanto, talvez você precise [habilitar scripts externos](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verifique **Launchpad do SQL Server service** está em execução antes de começar.

Você também precisa de uma ferramenta para executar consultas SQL. Você pode executar os scripts R usando qualquer gerenciamento de banco de dados ou consultar a ferramenta, desde que ele pode se conectar a uma instância do SQL Server e executar uma consulta T-SQL ou procedimento armazenado. Este início rápido usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="verify-r-exists"></a>Verifique se que existe R

Você pode confirmar que os serviços do Machine Learning (com R) está habilitado para sua instância do SQL Server e qual versão do R está instalado. Siga as etapas abaixo.

1. Abra o SQL Server Management Studio e conecte-se à instância do SQL Server.

2. Execute o código a seguir. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'R',
    @script=N'print(version)';
    GO
    ```

3. O R `print` função retorna a versão para o **mensagens** janela. Na saída do exemplo abaixo, você pode ver que, nesse caso, SQL Server tem de R versão 3.3.3 instalado.

    **Resultados**

    ```text
    platform       x86_64-w64-mingw32          
    arch           x86_64                      
    os             mingw32                     
    system         x86_64, mingw32             
    status                                     
    major          3                           
    minor          3.3                         
    year           2017                        
    month          03                          
    day            06                          
    svn rev        72310                       
    language       R                           
    version.string R version 3.3.3 (2017-03-06)
    nickname       Another Canoe               
    ```

Se você receber erros dessa consulta, a regra os problemas de instalação. Configuração de pós-instalação é necessária para habilitar o uso de bibliotecas de código externo. Ver [instalar serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) ou [instalar o SQL Server 2016 R Services](../install/sql-r-services-windows-install.md). Da mesma forma, certifique-se de que o serviço Launchpad está em execução.

Dependendo do seu ambiente, você pode precisar habilitar as contas de trabalho R para se conectar ao SQL Server, instalar bibliotecas de rede adicional, habilitar a execução remota de código ou reiniciar a instância depois que tudo estiver configurado. Para obter mais informações, consulte [perguntas frequentes sobre atualização e instalação de serviços de R](../r/upgrade-and-installation-faq-sql-server-r-services.md).

## <a name="list-r-packages"></a>Pacotes de R da lista

A Microsoft fornece um número de pacotes de R pré-instalados com serviços de Machine Learning em sua instância do SQL Server. Para ver uma lista de quais R pacotes são instalados, incluindo a versão, dependências, licença e informações de caminho de biblioteca, siga as etapas abaixo.

1. Execute o script abaixo em sua instância do SQL Server.

    ```SQL
    EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
    OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
    WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
        , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
    ```

2. O resultado é de `installed.packages()` em R e retornado como resultado de conjunto.

    **Resultados**

    ![Pacotes instalados em R](./media/rsql-installed-packages.png)

## <a name="next-steps"></a>Próximas etapas

Agora que você confirmou a que sua instância estiver pronta para trabalhar com R, dar uma olhada mais próxima em uma interação básica do R.

> [!div class="nextstepaction"]
> [Guia de início rápido: Script de R "Hello world" no SQL Server ](quickstart-r-run-using-tsql.md)
