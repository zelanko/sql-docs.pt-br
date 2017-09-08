---
title: 'Etapa 3: Explorar e visualizar os dados | Microsoft Docs'
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-python
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dfb80fcd3241b22f0ac72c2cf4cd8a18d1add857
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="step-3-explore-and-visualize-the-data"></a>Etapa 3: Explorar e visualizar os dados

Em geral, o desenvolvimento de uma solução de ciência de dados inclui intensiva exploração e visualização de dados. Nesta etapa, você irá explorar os dados de exemplo e gerar alguns gráficos. Posteriormente, você aprenderá como serializar objetos gráficos em Python e, em seguida, desserializar esses objetos e fazer gráficos.

> [!NOTE]
> Este passo a passo demonstra apenas a tarefa de classificação binária; Você está bem-vindo ao tentar criar modelos separados para outras tarefas de aprendizado de máquina dois, regressão e classificação multiclasse.

## <a name="review-the-data"></a>Examinar os dados

No conjunto de dados original, os identificadores de táxi e os registros de corrida eram fornecidos em arquivos separados. No entanto, para facilitar o uso dos dados de exemplo, os dois conjuntos de dados originais foram unidos nas colunas _medallion_, _hack_license_e _pickup_datetime_.  Também foram obtidas amostras dos registros para que fosse obtido apenas 1% do número original de registros. O conjunto de dados resultante com redução da resolução tem 1.703.957 linhas e 23 colunas.

**Identificadores de táxi**

- A coluna _medallion_ representa o número de ID exclusivo do táxi.
- A coluna _hack_license_ contém o número de licença do motorista do táxi (anônimo).

**Registros de corrida e tarifa**

- Cada registro de corrida inclui os locais de embarque e desembarque de passageiros, a hora e a distância da corrida.
- Cada registro de tarifa inclui informações de pagamento, como a forma de pagamento, o valor total do pagamento e o valor da gorjeta.
- As três últimas colunas podem ser usadas para várias tarefas de aprendizado de máquina.  A coluna _tip_amount_ contém valores numéricos contínuos e pode ser usada como a coluna **label** para a análise de regressão. A coluna _tipped_ tem apenas valores sim/não e é usada para classificação binária. A coluna _tip_class_ tem vários **rótulos de classe** e, portanto, pode ser usada como o rótulo para tarefas de classificação de várias classes.
- Os valores usados para as colunas de rótulo se baseiam na coluna _tip_amount_ , usando estas regras de negócio:
  
    |Nome de coluna derivada|Regra|
    |-|-|
     |tipped|Se tip_amount > 0, tipped = 1; caso contrário, tipped = 0|
    |tip_class|Classe 0: tip_amount = $0<br /><br />Classe 1: tip_amount > US$ 0 e tip_amount <= US$ 5<br /><br />Classe 2: tip_amount > US$ 5 e tip_amount <= US$ 10<br /><br />Classe 3: tip_amount > US$ 10 e tip_amount <= US$ 20<br /><br />Classe 4: tip_amount > $20|

## <a name="create-plots-using-python-in-t-sql"></a>Criar gráficos usando Python no T-SQL

Como visualização é uma ferramenta poderosa para entender a distribuição dos dados e exceções, o Python fornece muitos pacotes para visualização de dados. O **matplotlib** módulo é uma biblioteca popular que inclui muitas funções para a criação de histogramas, gráficos de dispersão, gráficos de caixa e outros gráficos de exploração de dados.

Nesta seção, você aprenderá como trabalhar com gráficos usando procedimentos armazenados. Armazenar o `plot` Python de objeto como um **varbinary** dados de tipo e salvar os gráficos gerados no servidor.

### <a name="storing-plots-as-varbinary-data-type"></a>Armazenando plotagens como o tipo de dados varbinary

O **revoscalepy** módulo incluído com os serviços de aprendizado de máquina do SQL Server 2017 contém bibliotecas análogas a bibliotecas de R no pacote RevoScaleR. Neste exemplo, você usará o equivalente a Python `rxHistogram` para plotar um histograma com base em dados de um [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. Para facilitar, você irá colocá-los em um procedimento armazenado, _PlotHistogram_.

O procedimento armazenado retorna um Python serializado `figure` objeto como um fluxo de **varbinary** dados. Não é possível exibir os dados binários diretamente, mas você pode usar o código Python no cliente para desserializar e exibir os dados e, em seguida, salve o arquivo de imagem em um computador cliente.

### <a name="create-the-stored-procedure-plotspython"></a>Criar o procedimento armazenado Plots_Python

1.  Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra uma nova **consulta** janela.

2.  Selecione o banco de dados para o passo a passo e crie o procedimento usando essa instrução. Lembre-se de modificar o código para usar o nome de tabela correto, se necessário.
  
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
**Observações:**

- A variável `@query` define o texto da consulta (`'SELECT tipped FROM nyctaxi_sample'`), que é passado para o bloco de código Python como o argumento para a variável de entrada de script, `@input_data_1`.
- O script de Python é bastante simple: **matplotlib** `figure` objetos são usados para fazer o gráfico de histograma e dispersão, e esses objetos, em seguida, são serializados usando o `pickle` biblioteca.
- O objeto de gráfico do Python é serializado como um Python **pandas** DataFrame de saída.

### <a name="output-varbinary-data-to-viewable-graphics-file"></a>Dados varbinary de saída para arquivo gráfico visível

1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], execute a seguinte instrução:
  
    ```
    EXEC [dbo].[SerializePlots]
    ```
  
    **Resultados**
  
    *plotagem*
    *0xFFD8FFE000104A4649... * 
     *0xFFD8FFE000104A4649... * 
     *0xFFD8FFE000104A4649... * 
     *0xFFD8FFE000104A4649...*

  
2.  No computador cliente, execute o código Python a seguir, substituindo o nome do servidor, nome do banco de dados e as credenciais conforme apropriado.
  
    **Para autenticação do SQL server:**
    
        ```python
        import pyodbc
        import pickle
        import os
        cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSOWRD}')
        cursor = cnxn.cursor()
        cursor.execute("EXECUTE [dbo].[SerializePlots]")
        tables = cursor.fetchall()
        for i in range(0, len(tables)):
            fig = pickle.loads(tables[i][0])
            fig.savefig(str(i)+'.png')
        print("The plots are saved in directory: ",os.getcwd())
        ```  
    **Para autenticação do Windows:**

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

    > [!NOTE]
    > Verifique se que a versão do Python é o mesmo no cliente e o servidor. Além disso, certifique-se de que as bibliotecas do Python que você está usando no seu cliente (como matplotlib) são da versão igual ou superior em relação as bibliotecas instaladas no servidor.


3.  Se a conexão for bem-sucedida, você verá os resultados abaixo
  
    *Os gráficos são salvos no diretório: xxxx*
  
4.  O arquivo de saída será criado no diretório de trabalho de Python. Para exibir o gráfico, basta abra o diretório de trabalho do Python. A imagem a seguir mostra uma plotagem de exemplo salva no computador cliente.
  
    ![Dica de quantidade de passagens vs quantidade](media/sqldev-python-sample-plot.png "quantidade de passagens dica quantidade vs") 

## <a name="next-step"></a>Próxima etapa

[Etapa 4: Criar recursos de dados usando o T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Etapa anterior

[Etapa 2: Importar dados para o SQL Server usando o PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="see-also"></a>Consulte também

[Serviços de aprendizado de máquina com Python](../python/sql-server-python-services.md)

