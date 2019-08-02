---
title: O início rápido para verificar se o R existe no SQL Server
description: Início rápido para verificar se o R e o Serviços de Machine Learning existem no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 072a6f34a7cb91505d77356d6ec3835915c310d0
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715407"
---
# <a name="quickstart-verify-r-exists-in-sql-server"></a>Início Rápido: Verificar se o R existe no SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O SQL Server inclui suporte à linguagem R para análise de ciência de dados em dados SQL Server residentes. Seu script R pode consistir em funções de R de software livre, bibliotecas de R de terceiros ou bibliotecas do Microsoft R internas, como [RevoScaleR](../r/revoscaler-overview.md) para análise preditiva em escala.

A execução do script é por meio de procedimentos armazenados, usando uma das seguintes abordagens:

+ Procedimento armazenado [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) interno, passando o script R no como um parâmetro de entrada.
+ Encapsular script R em um [procedimento armazenado personalizado](sqldev-in-database-r-for-sql-developers.md) que você criar.

Neste guia de início rápido, você verificará se [SQL Server serviços de Machine Learning](../what-is-sql-server-machine-learning.md) ou [SQL Server 2016 R Services](../r/sql-server-r-services.md) estão instalados e configurados.

## <a name="prerequisites"></a>Pré-requisitos

Este exercício requer acesso a uma instância do SQL Server com uma das seguintes opções já instaladas:

+ [SQL Server serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md), com a linguagem R instalada
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

Sua instância de SQL Server pode estar em uma máquina virtual do Azure ou no local. Apenas esteja ciente de que o recurso de script externo está desabilitado por padrão, portanto, talvez seja necessário [habilitar o script externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificar se **SQL Server Launchpad serviço** está em execução antes de iniciar.

Você também precisa de uma ferramenta para executar consultas SQL. Você pode executar os scripts do R usando qualquer ferramenta de consulta ou gerenciamento de banco de dados, desde que ele possa se conectar a uma instância de SQL Server e executar uma consulta T-SQL ou um procedimento armazenado. Este início rápido usa o [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="verify-r-exists"></a>Verificar se o R existe

Você pode confirmar se o Serviços de Machine Learning (com R) está habilitado para sua instância do SQL Server e qual versão do R está instalada. Siga as etapas abaixo.

1. Abra SQL Server Management Studio e conecte-se à sua instância do SQL Server.

2. Execute o código a seguir. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'R',
    @script=N'print(version)';
    GO
    ```

3. A função `print` R retorna a versão para a janela **mensagens** . Na saída de exemplo abaixo, você pode ver que SQL Server nesse caso têm R versão 3.3.3 instalada.

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

Se você receber erros dessa consulta, descartar quaisquer problemas de instalação. A configuração pós-instalação é necessária para habilitar o uso de bibliotecas de código externo. Consulte [instalar SQL Server serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) ou [instalar o SQL Server R Services 2016](../install/sql-r-services-windows-install.md). Da mesma forma, verifique se o serviço Launchpad está em execução.

Dependendo do seu ambiente, você pode precisar habilitar as contas de trabalho R para se conectar ao SQL Server, instalar bibliotecas de rede adicional, habilitar a execução remota de código ou reiniciar a instância depois que tudo estiver configurado. Para obter mais informações, consulte [perguntas frequentes sobre instalação e atualização do R Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

## <a name="list-r-packages"></a>Listar pacotes de R

A Microsoft fornece vários pacotes de R pré-instalados com Serviços de Machine Learning em sua instância de SQL Server. Para ver uma lista de quais pacotes do R estão instalados, incluindo informações de versão, dependências, licença e caminho de biblioteca, siga as etapas abaixo.

1. Execute o script abaixo em sua instância de SQL Server.

    ```SQL
    EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
    OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
    WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
        , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
    ```

2. A saída é de `installed.packages()` em R e retornada como um conjunto de resultados.

    **Resultados**

    ![Pacotes instalados em R](./media/rsql-installed-packages.png)

## <a name="next-steps"></a>Próximas etapas

Agora que você confirmou que sua instância está pronta para trabalhar com o R, dê uma olhada em mais detalhes em uma interação básica de R.

> [!div class="nextstepaction"]
> [Início Rápido: Script R "Olá mundo" no SQL Server](quickstart-r-run-using-tsql.md)
