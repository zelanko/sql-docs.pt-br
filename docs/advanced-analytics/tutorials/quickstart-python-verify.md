---
title: O início rápido para verificar se o Python existe no SQL Server
description: Início rápido para verificar se o Python e o Serviços de Machine Learning existem no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0dd5714f47c90c0091daacbd792b80c05ec68675
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469694"
---
# <a name="quickstart-verify-python-exists-in-sql-server"></a>Início Rápido: Verificar se o Python existe no SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O SQL Server inclui suporte a idiomas Python para análise de ciência de dados em dados SQL Server residentes. A execução do script é por meio de procedimentos armazenados, usando uma das seguintes abordagens:

+ Procedimento armazenado [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) interno, passando o script Python no como um parâmetro de entrada.
+ Encapsular script Python em um [procedimento armazenado personalizado](sqldev-in-database-r-for-sql-developers.md) que você criar.

Neste guia de início rápido, você verificará se [SQL Server Serviços de Machine Learning 2017](../what-is-sql-server-machine-learning.md) está instalado e configurado.

## <a name="prerequisites"></a>Pré-requisitos

Este exercício requer acesso a uma instância do SQL Server com [SQL Server 2017 serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) instalado.

Sua instância de SQL Server pode estar em uma máquina virtual do Azure ou no local. Apenas esteja ciente de que o recurso de script externo está desabilitado por padrão, portanto, talvez seja necessário [habilitar o script externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificar se **SQL Server Launchpad serviço** está em execução antes de iniciar.

Você também precisa de uma ferramenta para executar consultas SQL. Você pode executar os scripts do Python usando qualquer ferramenta de consulta ou gerenciamento de banco de dados, desde que ele possa se conectar a uma instância de SQL Server e executar uma consulta T-SQL ou um procedimento armazenado. Este início rápido usa o [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="verify-python-exists"></a>Verificar se o Python existe

Você pode confirmar se o Serviços de Machine Learning (está habilitado para sua instância do SQL Server e qual versão do Python está instalada. Siga as etapas abaixo.

1. Abra SQL Server Management Studio e conecte-se à sua instância do SQL Server.

2. Execute o código a seguir. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import sys
    print(sys.version)';
    GO
    ```

3. A função `print` Python retorna a versão para a janela **mensagens** . Na saída de exemplo abaixo, você pode ver que SQL Server nesse caso têm o Python versão 3.5.2 instalado.

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
    ```

Se você receber erros, há uma variedade de coisas que você pode fazer para garantir que a instância e o Python possam se comunicar.

Primeiro, descartar quaisquer problemas de instalação. A configuração pós-instalação é necessária para habilitar o uso de bibliotecas de código externo. Consulte [instalar SQL Server 2017 serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md). Da mesma forma, verifique se o serviço Launchpad está em execução.

Você também deve adicionar o grupo `SQLRUserGroup` de usuários do Windows como um logon na instância do, para garantir que o Launchpad possa fornecer comunicação entre o Python e o SQL Server. (O mesmo grupo é usado para a execução de código em R e Python.) Para obter mais informações, consulte [criar um logon para SQLRUserGroup](../security/create-a-login-for-sqlrusergroup.md).

Além disso, talvez seja necessário habilitar os protocolos de rede que foram desabilitados ou abrir o firewall para que SQL Server possam se comunicar com clientes externos. Para obter mais informações, consulte [solução de problemas de instalação](../common-issues-external-script-execution.md).

## <a name="call-revoscalepy-functions"></a>Chamar funções revoscalepy

Para verificar se o **revoscalepy** está disponível, execute um script de exemplo que inclua [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) que produza dados de resumo estatísticos. O script a seguir demonstra como recuperar um arquivo de dados Sample. Xdf de exemplos internos incluídos no revoscalepy. A função RxOptions fornece o parâmetro **sampleDataDir** que retorna o local dos arquivos de exemplo.

Como rx_summary retorna um objeto do tipo `class revoscalepy.functions.RxSummary.RxSummaryResults`, que contém vários elementos, você pode usar pandas para extrair apenas o quadro de dados em um formato tabular.

```sql
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

## <a name="list-python-packages"></a>Listar pacotes python

A Microsoft fornece vários pacotes do Python pré-instalados com o Serviços de Machine Learning em sua instância do SQL Server. Para ver uma lista dos pacotes do Python instalados, incluindo a versão, siga as etapas abaixo.

1. Execute o script abaixo em sua instância de SQL Server.

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import pip
    for i in pip.get_installed_distributions():
        print(i)';
    GO
    ```

2. A saída é de `pip.get_installed_distributions()` no Python e retornada como `STDOUT` mensagens.

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    xlwt 1.2.0
    XlsxWriter 0.9.6
    xlrd 1.0.0
    win-unicode-console 0.5
    widgetsnbextension 2.0.0
    wheel 0.29.0
    Werkzeug 0.12.1
    wcwidth 0.1.7
    unicodecsv 0.14.1
    traitlets 4.3.2
    tornado 4.4.2
    toolz 0.8.2
    testpath 0.3
    tables 3.2.2
    sympy 1.0
    statsmodels 0.8.0
    sqlparse 0.1.19
    SQLAlchemy 1.1.9
    snowballstemmer 1.2.1
    six 1.10.0
    simplegeneric 0.8.1
    seaborn 0.7.1
    scipy 0.19.0
    scikit-learn 0.18.1
    ...
    ```

## <a name="next-steps"></a>Próximas etapas

Agora que você confirmou que sua instância está pronta para funcionar com o Python, dê uma olhada em mais detalhes em uma interação básica do Python.

> [!div class="nextstepaction"]
> [Início Rápido: Script do Python "Olá, mundo" no SQL Server](quickstart-python-run-using-t-sql.md)
