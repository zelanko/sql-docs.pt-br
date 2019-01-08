---
title: Guia de início rápido para verificar o Python existe no SQL Server
description: Guia de início rápido para verificar o Python e serviços de Machine Learning existem no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 7a2e9bf58839832ba29b103d2e862a845090a9f1
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046736"
---
# <a name="quickstart-verify-python-exists-in-sql-server"></a>Guia de início rápido: Verifique se que existe do Python no SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server inclui o suporte de linguagem do Python para análises de ciência de dados em dados do SQL Server residentes. Execução do script é por meio de procedimentos armazenados, usando qualquer uma das seguintes abordagens:

+ Interna [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) procedimento armazenado, passando o script Python no como um parâmetro de entrada.
+ Encapsular o script de Python em um [procedimento armazenado de personalizado](sqldev-in-database-r-for-sql-developers.md) criado por você.

Neste início rápido, você verificará que [serviços de aprendizado de máquina do SQL Server 2017](../what-is-sql-server-machine-learning.md) está instalado e configurado.

## <a name="prerequisites"></a>Prerequisites

Este exercício exige o acesso a uma instância do SQL Server com [serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) instalado.

Instância do SQL Server pode estar em uma máquina virtual do Azure ou no local. Apenas lembre-se de que o recurso de script externo é desabilitado por padrão, portanto, talvez você precise [habilitar scripts externos](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verifique **Launchpad do SQL Server service** está em execução antes de começar.

Você também precisa de uma ferramenta para executar consultas SQL. Você pode executar os scripts de Python usando qualquer gerenciamento de banco de dados ou consultar a ferramenta, desde que ele pode se conectar a uma instância do SQL Server e executar uma consulta T-SQL ou procedimento armazenado. Este início rápido usa [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="verify-python-exists"></a>Verifique se que existe do Python

Você pode confirmar esse serviços de Machine Learning (está habilitado para sua instância do SQL Server e qual versão do Python é instalado. Siga as etapas abaixo.

1. Abra o SQL Server Management Studio e conecte-se à instância do SQL Server.

2. Execute o código a seguir. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import sys
    print(sys.version)';
    GO
    ```

3. O Python `print` função retorna a versão para o **mensagens** janela. Na saída do exemplo abaixo, você pode ver que, nesse caso, SQL Server tem de Python versão 3.5.2 instalado.

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
    ```

Se você obtiver erros, há uma variedade de coisas que você pode fazer para garantir que a instância e o Python pode se comunicar.

Primeiro, elimine quaisquer problemas de instalação. Configuração de pós-instalação é necessária para habilitar o uso de bibliotecas de código externo. Ver [instalar serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md). Da mesma forma, certifique-se de que o serviço Launchpad está em execução.

Você também deve adicionar o grupo de usuários do Windows `SQLRUserGroup` como um logon na instância, para garantir que o Launchpad poderá fornecer comunicação entre o Python e o SQL Server. (O mesmo grupo é usado para ambos os R e execução de código do Python.) Para obter mais informações, consulte [habilitado a autenticação implícita](../security/add-sqlrusergroup-to-database.md).

Além disso, talvez você precise habilitar protocolos de rede que foram desabilitados ou abrir o firewall para que o SQL Server pode se comunicar com clientes externos. Para obter mais informações, consulte [Solucionando problemas de instalação](../common-issues-external-script-execution.md).

## <a name="call-revoscalepy-functions"></a>Chamar funções revoscalepy

Para verificar se **revoscalepy** estiver disponível, execute um script de exemplo que inclui [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) que produz um resumo estatístico de dados. O script a seguir demonstra como recuperar um arquivo de dados do exemplo. xdf de exemplos internos incluídos no revoscalepy. A função RxOptions fornece o **sampleDataDir** parâmetro que retorna o local dos arquivos de exemplo.

Como rx_summary retorna um objeto do tipo `class revoscalepy.functions.RxSummary.RxSummaryResults`, que contém vários elementos, você pode usar o pandas para extrair apenas o quadro de dados em um formato tabular.

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

## <a name="list-python-packages"></a>Listar os pacotes do Python

A Microsoft fornece um número de pacotes de Python pré-instalados com serviços de Machine Learning em sua instância do SQL Server. Para ver uma lista de quais Python pacotes são instalados, incluindo a versão, siga as etapas abaixo.

1. Execute o script abaixo em sua instância do SQL Server.

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'Python',
    @script=N'import pip
    for i in pip.get_installed_distributions():
        print(i)';
    GO
    ```

2. O resultado é de `pip.get_installed_distributions()` em Python e retornados como `STDOUT` mensagens.

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

Agora que você confirmou a que sua instância estiver pronta para trabalhar com Python, dar uma interação de Python básica examinar mais detalhadamente.

> [!div class="nextstepaction"]
> [Guia de início rápido: Script de Python de "Hello world" no SQL Server ](quickstart-python-run-using-t-sql.md)
