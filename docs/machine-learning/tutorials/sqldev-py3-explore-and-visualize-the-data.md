---
title: 'Python + T-SQL: Explorar dados'
description: Tutorial mostrando como inserir o Python em procedimentos armazenados do SQL Server e funções do T-SQL
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 05b51550880e2e2324698cdadc92ba1d7dd1cc7f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775355"
---
# <a name="explore-and-visualize-the-data"></a>Explorar e visualizar os dados
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este artigo faz parte de um tutorial, [Análise do Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md). 

Nesta etapa, você explora os dados de exemplo e gera alguns gráficos. Posteriormente, você aprende a serializar objetos gráficos no Python e desserializá-los e fazer gráficos.

## <a name="review-the-data"></a>Examinar os dados

Primeiro, reserve um minuto para procurar o esquema de dados, já que fizemos algumas alterações para facilitar o uso dos dados de Táxi de NYC

+ O conjunto de recursos original usava arquivos separados para os identificadores de táxi e os registros de viagem. Nós ingressamos os dois conjuntos de dados originais nas colunas _medallion_, _hack_license_ e _pickup_datetime_.  
+ O conjunto de dados original abrangia muitos arquivos e era muito grande. Reduzimos a amostra para obter apenas 1% do número original de registros. A tabela de dados atual tem 1.703.957 linhas e 23 colunas.

**Identificadores de táxi**

A coluna _medallion_ representa o número da ID exclusiva do táxi.

A coluna _hack_license_ contém o número de licença do motorista do táxi (anônimo).

**Registros de corrida e tarifa**

Cada registro de corrida inclui os locais de embarque e desembarque de passageiros, a hora e a distância da corrida.

Cada registro de tarifa inclui informações de pagamento, como a forma de pagamento, o valor total do pagamento e o valor da gorjeta.

As três últimas colunas podem ser usadas para várias tarefas de aprendizado de máquina.  A coluna _tip_amount_ contém valores numéricos contínuos e pode ser usada como a coluna **label** para a análise de regressão. A coluna _tipped_ tem apenas valores sim/não e é usada para classificação binária. A coluna _tip_class_ tem vários **rótulos de classe** e, portanto, pode ser usada como o rótulo para tarefas de classificação de várias classes.

Os valores usados para as colunas de rótulo se baseiam na coluna `tip_amount` usando estas regras de negócio:

+ A coluna de rótulo `tipped` tem os valores possíveis 0 e 1

    Se `tip_amount` > 0, `tipped` = 1; caso contrário, `tipped` = 0

+ A coluna de rótulo `tip_class` tem os valores de classe possíveis 0-4

    Classe 0: `tip_amount` = $0

    Classe 1: `tip_amount` > $0 e `tip_amount` <= $5
    
    Classe 2: `tip_amount` > $5 e `tip_amount` <= $10
    
    Classe 3: `tip_amount` > $10 e `tip_amount` <= $20
    
    Classe 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>Criar gráficos usando o Python no T-SQL

Em geral, o desenvolvimento de uma solução de ciência de dados inclui intensiva exploração e visualização de dados. Como a visualização é uma ferramenta avançada para entender a distribuição dos dados e das exceções, o Python fornece diversos pacotes para a visualização de dados. O módulo **matplotlib** é uma das bibliotecas mais populares para visualização e inclui muitas funções para criar histogramas, gráficos de dispersão, gráficos de caixa e outros grafos de exploração de dados.

Nesta seção, você aprenderá a trabalhar com gráficos usando procedimentos armazenados. Em vez de abrir a imagem no servidor, você armazena o objeto Python `plot` como dados **varbinary** e, em seguida, grava-os em um arquivo que pode ser compartilhado ou exibido em outro lugar.

### <a name="create-a-plot-as-varbinary-data"></a>Criar um gráfico como dados varbinary

O procedimento armazenado retorna um objeto `figure` do Python serializado como um fluxo de dados **varbinary**. Você não pode exibir os dados binários diretamente, mas pode usar o código Python no cliente para desserializar e exibir as figuras e, em seguida, salvar o arquivo de imagem em um computador cliente.

1. Crie o procedimento armazenado **PyPlotMatplotlib** se o script do PowerShell ainda não tiver feito isso.

    - A variável `@query` define o texto da consulta `SELECT tipped FROM nyctaxi_sample`, que é passado para o bloco de código do Python como o argumento para a variável de entrada de script, `@input_data_1`.
    - O script Python é bastante simples: os objetos **matplotlib** `figure` são usados para criar o histograma e o gráfico de dispersão e esses objetos então são serializados usando a biblioteca de `pickle`.
    - O objeto de gráfico do Python é serializado para um DataFrame **Pandas** para saída.
  
    ```sql
    DROP PROCEDURE IF EXISTS PyPlotMatplotlib;
    GO

    CREATE PROCEDURE [dbo].[PyPlotMatplotlib]
    AS
    BEGIN
        SET NOCOUNT ON;
        DECLARE @query nvarchar(max) =
        N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'
        EXECUTE sp_execute_external_script
        @language = N'Python',
        @script = N'
    import matplotlib
    matplotlib.use("Agg")
    import matplotlib.pyplot as plt
    import pandas as pd
    import pickle

    fig_handle = plt.figure()
    plt.hist(InputDataSet.tipped)
    plt.xlabel("Tipped")
    plt.ylabel("Counts")
    plt.title("Histogram, Tipped")
    plot0 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.tip_amount)
    plt.xlabel("Tip amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Tip amount")
    plot1 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.fare_amount)
    plt.xlabel("Fare amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Fare amount")
    plot2 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.scatter( InputDataSet.fare_amount, InputDataSet.tip_amount)
    plt.xlabel("Fare Amount ($)")
    plt.ylabel("Tip Amount ($)")
    plt.title("Tip amount by Fare amount")
    plot3 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    OutputDataSet = plot0.append(plot1, ignore_index=True).append(plot2, ignore_index=True).append(plot3, ignore_index=True)
    ',
    @input_data_1 = @query
    WITH RESULT SETS ((plot varbinary(max)))
    END
    GO
    ```

2. Agora, execute o procedimento armazenado sem argumentos para gerar um gráfico com os dados embutidos em código como a consulta de entrada.

    ```sql
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. Os resultados devem ser semelhantes a estes:
  
    ```sql
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. Em um [cliente Python](../python/setup-python-client-tools-sql.md), agora você pode se conectar à instância do SQL Server que gerou os objetos binários do gráfico e exibir os gráficos. 

    Para fazer isso, execute o seguinte código Python substituindo o nome do servidor, o nome do banco de dados e as credenciais conforme apropriado. Verifique se a versão do Python é a mesma no cliente e no servidor. Além disso, verifique se as bibliotecas do Python em seu cliente (como matplotlib) são de uma versão igual ou superior com relação às bibliotecas instaladas no servidor.
  
    **Como usar a autenticação do SQL Server:**
    
    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

    **Usando a autenticação do Windows:**

    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=True;')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5.  se a conexão for bem-sucedida, você verá uma mensagem semelhante à seguinte:
  
    *Os gráficos são salvos no diretório: xxxx*
  
6.  O arquivo de saída é criado no diretório de trabalho do Python. Para exibir o gráfico, localize o diretório de trabalho do Python e abra o arquivo. A imagem a seguir mostra um gráfico salvo no computador cliente.
  
    ![Valor da gorjeta versus valor da tarifa](media/sqldev-python-sample-plot.png "Valor da gorjeta versus valor da tarifa") 

## <a name="next-step"></a>Próxima etapa

[Criar recursos de dados usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Etapa anterior

[Baixar o conjunto de dados Táxi de NYC](demo-data-nyctaxi-in-sql.md)

