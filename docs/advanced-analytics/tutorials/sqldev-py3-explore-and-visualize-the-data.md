---
title: Lição 1 explorar e visualizar dados usando o Python e T-SQL – SQL Server Machine Learning
description: Tutorial que mostra como incorporar o Python no SQL Server procedimentos armazenados e funções T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: b9011894c4cf524b0eeaf016cd0d3de60058832e
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512413"
---
# <a name="explore-and-visualize-the-data"></a>Explorar e visualizar os dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte de um tutorial [análise de Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md). 

Nesta etapa, você pode explora os dados de exemplo e gerar algumas plotagens. Posteriormente, você aprenderá como serializar objetos gráficos em Python e, em seguida, desserializar os objetos e fazer gráficos.

## <a name="review-the-data"></a>Revise os dados

Primeiro, reserve um minuto para procurar o esquema de dados, como fizemos algumas alterações para torná-lo mais fácil de usar os dados de táxi de NYC

+ O conjunto de dados original usado arquivos separados para os identificadores de táxi e os registros de corrida. Podemos ingressou dois conjuntos de dados originais nas colunas _medallion_, _hack_license_, e _pickup_datetime_.  
+ O conjunto de dados original ocupadas muitos arquivos e era muito grande. Temos diminuída para obter apenas 1% do número original de registros. A tabela de dados atual tem 1.703.957 linhas e 23 colunas.

**Identificadores de táxi**

O _medallion_ coluna representa o número de identificação exclusivo do táxi.

O _hack_license_ coluna contém o número de licença do motorista do táxi (anônimo).

**Registros de corrida e tarifa**

Cada registro de corrida inclui os locais de embarque e desembarque de passageiros, a hora e a distância da corrida.

Cada registro de tarifa inclui informações de pagamento, como a forma de pagamento, o valor total do pagamento e o valor da gorjeta.

As três últimas colunas podem ser usadas para várias tarefas de aprendizado de máquina.  A coluna _tip_amount_ contém valores numéricos contínuos e pode ser usada como a coluna **label** para a análise de regressão. A coluna _tipped_ tem apenas valores sim/não e é usada para classificação binária. A coluna _tip_class_ tem vários **rótulos de classe** e, portanto, pode ser usada como o rótulo para tarefas de classificação de várias classes.

Os valores usados para as colunas de rótulo se baseiam no `tip_amount` coluna, usando essas regras de negócio:

+ Coluna de rótulo `tipped` tem os valores possíveis 0 e 1

    Se `tip_amount` > 0, `tipped` = 1; caso contrário `tipped` = 0

+ Coluna de rótulo `tip_class` tem valores de classe possíveis de 0 a 4

    Classe 0: `tip_amount` = US $0

    Classe 1: `tip_amount` > US $0 e `tip_amount` < = US $5
    
    Classe 2: `tip_amount` > US $5 e `tip_amount` < = US $10
    
    Classe 3: `tip_amount` > US $10 e `tip_amount` < = US $20
    
    Classe 4: `tip_amount` > US $20.

## <a name="create-plots-using-python-in-t-sql"></a>Criar plotagens usando o Python no T-SQL

Em geral, o desenvolvimento de uma solução de ciência de dados inclui intensiva exploração e visualização de dados. Como a visualização é uma ferramenta poderosa para entender a distribuição dos dados e exceções, o Python fornece muitos pacotes para visualização de dados. O **matplotlib** módulo é uma das bibliotecas mais populares para visualização e inclui muitas funções para a criação de histogramas, dispersões, gráficos de caixa e outros gráficos de exploração de dados.

Nesta seção, você aprenderá como trabalhar com gráficos usando procedimentos armazenados. Em vez de abrir a imagem no servidor, armazene o objeto de Python `plot` como **varbinary** dados e, em seguida, gravar do que em um arquivo que pode ser compartilhado ou exibidos em outro lugar.

### <a name="create-a-plot-as-varbinary-data"></a>Criar um gráfico como dados varbinary

O procedimento armazenado retorna um Python serializado `figure` objeto como um fluxo de **varbinary** dados. Você não pode exibir os dados binários diretamente, mas você pode usar o código Python para desserializar e exibir os números no cliente e, em seguida, salve o arquivo de imagem em um computador cliente.

1. Criar o procedimento armazenado **PyPlotMatplotlib**, se o script do PowerShell ainda não fez isso.

    - A variável `@query` define o texto da consulta `SELECT tipped FROM nyctaxi_sample`, que é passado para o bloco de código do Python como o argumento para a variável de entrada de script `@input_data_1`.
    - O script Python é bastante simple: **matplotlib** `figure` objetos são usados para fazer o gráfico de dispersão e de histograma, e esses objetos são serializados usando a `pickle` biblioteca.
    - O objeto de gráfico do Python é serializado para um **pandas** DataFrame de saída.
  
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

2. Agora execute o procedimento armazenado sem argumentos para gerar um gráfico de dados embutidos como consulta de entrada.

    ```sql
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. Os resultados devem ser algo parecido com isto:
  
    ```sql
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. De um [cliente Python](../python/setup-python-client-tools-sql.md), agora você pode se conectar à instância do SQL Server que gerou os objetos de plotagem binário e exibir os gráficos. 

    Para fazer isso, execute o seguinte código do Python, substituindo o nome do servidor, nome do banco de dados e as credenciais conforme apropriado. Verifique se que a versão do Python é o mesmo no cliente e o servidor. Também Certifique-se de que as bibliotecas Python no seu cliente (como matplotlib) são a versão igual ou superior em relação as bibliotecas instaladas no servidor.
  
    **Usando a autenticação do SQL Server:**
    
    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
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
    cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=True;')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5.  Se a conexão for bem-sucedida, você verá uma mensagem semelhante ao seguinte:
  
    *Os gráficos são salvos no diretório: xxxx*
  
6.  O arquivo de saída é criado no diretório de trabalho do Python. Para exibir a plotagem, localize o diretório de trabalho do Python e abra o arquivo. A imagem a seguir mostra um gráfico salvo no computador cliente.
  
    ![Valor de tarifa vs quantidade de gorjeta](media/sqldev-python-sample-plot.png "gorjeta quantidade vs tarifa") 

## <a name="next-step"></a>Próxima etapa

[Criar recursos de dados usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Etapa anterior

[Baixar o conjunto de dados de táxi de NYC](demo-data-nyctaxi-in-sql.md)

