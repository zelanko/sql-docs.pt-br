---
title: 'Etapa 3: Explorar e visualizar os dados | Microsoft Docs'
ms.custom: 
ms.date: 10/17/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: ecf1953fd7b4d77e38973a929a23318b77910e91
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="step-3-explore-and-visualize-the-data"></a>Etapa 3: Explorar e visualizar os dados

Este artigo faz parte de um tutorial, [análise Python no banco de dados para desenvolvedores em SQL](sqldev-in-database-python-for-sql-developers.md). 

Nesta etapa, você pode explora os dados de exemplo e gerar alguns gráficos. Posteriormente, você aprenderá a serializar objetos gráficos em Python, desserializar os objetos e fazer gráficos.

## <a name="review-the-data"></a>Revise os dados

Primeiro, reserve um minuto para procurar o esquema de dados, como fizemos algumas alterações para tornar mais fácil de usar os dados NYC táxi

+ O conjunto de dados original usado arquivos separados para os identificadores de táxi e registros de viagem. Podemos ingressou dois conjuntos de dados originais nas colunas _medallion_, _hack_license_, e _pickup_datetime_.  
+ O conjunto de dados original estendidos muitos arquivos e era muito grande. Fornecemos reduzida para obter apenas 1% do número original de registros. A tabela de dados atual tem 1,703,957 linhas e colunas de 23.

**Identificadores de táxi**

O _medallion_ coluna representa o número de identificação exclusivo do táxi.

O _hack_license_ coluna contém o número de licença do driver táxi (anônimos).

**Registros de corrida e tarifa**

Cada registro de corrida inclui os locais de embarque e desembarque de passageiros, a hora e a distância da corrida.

Cada registro de tarifa inclui informações de pagamento, como a forma de pagamento, o valor total do pagamento e o valor da gorjeta.

As três últimas colunas podem ser usadas para várias tarefas de aprendizado de máquina.  A coluna _tip_amount_ contém valores numéricos contínuos e pode ser usada como a coluna **label** para a análise de regressão. A coluna _tipped_ tem apenas valores sim/não e é usada para classificação binária. A coluna _tip_class_ tem vários **rótulos de classe** e, portanto, pode ser usada como o rótulo para tarefas de classificação de várias classes.

Os valores usados para as colunas de rótulo se baseiam no `tip_amount` coluna, usando essas regras de negócio:

+ Coluna de rótulo `tipped` tem valores possíveis 0 e 1

    Se `tip_amount` > 0, `tipped` = 1; caso contrário, `tipped` = 0

+ Coluna de rótulo `tip_class` tem classe possíveis valores 0-4

    Classe 0: `tip_amount` = $0

    Classe 1: `tip_amount` > $0 e `tip_amount` < = US $5
    
    Classe 2: `tip_amount` > US $5 e `tip_amount` < = US $10
    
    Classe 3: `tip_amount` > $10 e `tip_amount` < = US $20
    
    Classe 4: `tip_amount` > US $20

## <a name="create-plots-using-python-in-t-sql"></a>Criar gráficos usando Python no T-SQL

Em geral, o desenvolvimento de uma solução de ciência de dados inclui intensiva exploração e visualização de dados. Como visualização é uma ferramenta poderosa para entender a distribuição dos dados e exceções, o Python fornece muitos pacotes para visualização de dados. O **matplotlib** módulo é uma das bibliotecas mais populares para visualização e inclui muitas funções para a criação de histogramas, gráficos de dispersão, gráficos de caixa e outros gráficos de exploração de dados.

Nesta seção, você aprenderá como trabalhar com gráficos usando procedimentos armazenados. Em vez de abrir a imagem no servidor, você armazena o objeto de Python `plot` como **varbinary** dados e, em seguida, gravar que para um arquivo que pode ser compartilhado ou exibidos em outro lugar.

### <a name="create-a-plot-as-varbinary-data"></a>Criar um gráfico como dados varbinary

O **revoscalepy** módulo incluído com os serviços de aprendizado de máquina do SQL Server 2017 oferece suporte a recursos semelhantes do **RevoScaleR** pacote r.  Este exemplo usa o equivalente a Python `rxHistogram` para plotar um histograma com base em dados de um [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. 

O procedimento armazenado retorna um Python serializado `figure` objeto como um fluxo de **varbinary** dados. Não é possível exibir os dados binários diretamente, mas você pode usar o código Python no cliente para desserializar e exibir os dados e, em seguida, salve o arquivo de imagem em um computador cliente.

1. Criar o procedimento armazenado _SerializePlots_, se o script do PowerShell já não fez isso.

    - A variável `@query` define o texto da consulta `SELECT tipped FROM nyctaxi_sample`, que é passado para o bloco de código Python como o argumento para a variável de entrada de script, `@input_data_1`.
    - O script de Python é bastante simple: **matplotlib** `figure` objetos são usados para fazer o gráfico de histograma e dispersão, e esses objetos, em seguida, são serializados usando o `pickle` biblioteca.
    - O objeto de gráfico do Python é serializado como um **pandas** DataFrame de saída.
  
    ```SQL
    CREATE PROCEDURE [dbo].[SerializePlots]
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

2. Agora execute o procedimento armazenado sem argumentos para gerar um gráfico de dados codificado como a consulta de entrada.

    ```
    EXEC [dbo].[SerializePlots]
    ```

3. Os resultados devem ser algo assim:
  
    ```
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. Em um cliente do Python, agora você pode se conectar à instância do SQL Server que gerou os objetos de plotagem binário e exibir os gráficos. 

    Para fazer isso, execute o código Python a seguir, substituindo o nome do servidor, nome do banco de dados e as credenciais conforme apropriado. Verifique se que a versão do Python é o mesmo no cliente e o servidor. Também, certifique-se de que as bibliotecas de Python no cliente (como matplotlib) são da versão igual ou superior em relação as bibliotecas instaladas no servidor.
  
    **Usando a autenticação do SQL Server:**
    
    ```python
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[SerializePlots]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

    **Usando a autenticação do Windows:**

    ```python
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=yes;')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[SerializePlots]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5.  Se a conexão for bem-sucedida, você verá uma mensagem semelhante ao seguinte:
  
    *Os gráficos são salvos no diretório: xxxx*
  
6.  O arquivo de saída é criado no diretório de trabalho de Python. Para exibir o gráfico, localize a pasta de trabalho do Python e abra o arquivo. A imagem a seguir mostra um gráfico salvo no computador cliente.
  
    ![Dica de quantidade de passagens vs quantidade](media/sqldev-python-sample-plot.png "quantidade de passagens dica quantidade vs") 

## <a name="next-step"></a>Próxima etapa

[Etapa 4: Criar recursos de dados usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Etapa anterior

[Etapa 2: Importar dados para o SQL Server usando o PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

