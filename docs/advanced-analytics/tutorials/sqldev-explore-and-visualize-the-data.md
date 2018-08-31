---
title: Lição 3 explorar e visualizar dados usando R e T-SQL (aprendizado de máquina do SQL Server) | Microsoft Docs
description: Tutorial que mostra como incorporar o R no SQL Server procedimentos armazenados e funções T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6b34de3c71629a1563bf0d480306680dc6253748
ms.sourcegitcommit: 320958d0f55b6974abf46f8a04f7a020ff86a0ae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703619"
---
# <a name="lesson-3-explore-and-visualize-the-data"></a>Lição 3: Explorar e visualizar os dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte de um tutorial para desenvolvedores SQL sobre como usar o R no SQL Server.

Nesta lição, você vai examinar os dados de exemplo e, em seguida, gerar algumas plotagens usando [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) partir [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) e genérica [Hist](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist) função em r de base. Essas funções do R já estão incluídas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

Um objetivo importante é que mostra como chamar funções R do [!INCLUDE[tsql](../../includes/tsql-md.md)] em procedimentos armazenados e salvar os resultados em formatos de arquivo do aplicativo:

+ Criar um procedimento armazenado usando **RxHistogram** para gerar uma plotagem R como dados varbinary. Use **bcp** para exportar o fluxo binário para um arquivo de imagem.
+ Criar um procedimento armazenado usando **Hist** para gerar um gráfico, salvar os resultados como saída JPG e PDF.

> [!NOTE]
> Como a visualização é uma ferramenta poderosa para entender a forma de dados e distribuição, o R fornece uma variedade de funções e pacotes para a geração de histogramas, dispersões, gráficos de caixa e outros gráficos de exploração de dados. R normalmente cria imagens usando um dispositivo do R para saída gráfica, o que você pode capturar e armazenar como uma **varbinary** tipo de dados para renderização no aplicativo. Você também pode salvar as imagens em qualquer um dos formatos de arquivo de suporte (. JPG. PDF, etc.).

## <a name="review-the-data"></a>Revise os dados

Em geral, o desenvolvimento de uma solução de ciência de dados inclui intensiva exploração e visualização de dados. Portanto, primeiro, reserve um minuto para examinar os dados de exemplo, se você ainda não fez isso.

No conjunto de dados original, os identificadores de táxi e os registros de corrida eram fornecidos em arquivos separados. No entanto, para facilitar a usar os dados de exemplo, dois conjuntos de dados originais foram Unidos nas colunas _medallion_, _hack\_licença_, e _pickup\_ Data e hora_.  Também foram obtidas amostras dos registros para que fosse obtido apenas 1% do número original de registros. O conjunto de dados resultante com redução da resolução tem 1.703.957 linhas e 23 colunas.

**Identificadores de táxi**
  
-   A coluna _medallion_ representa o número de ID exclusivo do táxi.
  
-   O _hack\_licença_ coluna contém o número de licença do motorista do táxi (anônimo).
  
**Registros de corrida e tarifa**
  
-   Cada registro de corrida inclui os locais de embarque e desembarque de passageiros, a hora e a distância da corrida.
  
-   Cada registro de tarifa inclui informações de pagamento, como a forma de pagamento, o valor total do pagamento e o valor da gorjeta.
  
-   As três últimas colunas podem ser usadas para várias tarefas de aprendizado de máquina. O _dica\_quantidade_ coluna contém valores numéricos contínuos e pode ser usada como o **rótulo** coluna para análise de regressão. A coluna _tipped_ tem apenas valores sim/não e é usada para classificação binária. O _dica\_classe_ coluna tem vários **rótulos de classe** e, portanto, pode ser usado como o rótulo para tarefas de classificação multiclasse.
  
    Este passo a passo demonstra apenas a tarefa de classificação binária; sinta-se à vontade para tentar criar modelos para as outras duas tarefas de aprendizado de máquina, regressão e classificação de várias classes.
  
-   Os valores usados para as colunas de rótulo se baseiam na _dica\_quantidade_ coluna, usando essas regras de negócio:
  
    |Nome de coluna derivada|Regra|
    |-|-|
     |tipped|Se tip_amount > 0, tipped = 1; caso contrário, tipped = 0|
    |tip_class|Classe 0: tip_amount = $0<br /><br />Classe 1: tip_amount > US$ 0 e tip_amount <= US$ 5<br /><br />Classe 2: tip_amount > US$ 5 e tip_amount <= US$ 10<br /><br />Classe 3: tip_amount > US$ 10 e tip_amount <= US$ 20<br /><br />Classe 4: tip_amount > $20|

## <a name="create-a-stored-procedure-using-rxhistogram-to-plot-the-data"></a>Criar um procedimento armazenado usando rxHistogram para plotar os dados

Para criar o gráfico, use [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram), uma das funções avançadas do R fornecidas no [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). Esta etapa plota um histograma com base em dados de um [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. Você pode encapsular essa função em um procedimento armazenado, **PlotHistogram**.

1. Na [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Pesquisador de objetos, clique com botão direito a **NYCTaxi_Sample** banco de dados, expanda **programabilidade**e, em seguida, expanda **Stored Procedures** para exibir o procedimentos criados na lição 2.

2. Clique com botão direito **PlotHistogram** e selecione **modificar** para exibir o código-fonte. Você pode executar este procedimento para chamar **rxHistogram** nos dados contidos na coluna da tabela nyctaxi_sample oblíquo.

3. Opcionalmente, como um exercício de aprendizado, crie sua própria cópia desse procedimento armazenado usando o exemplo a seguir. Abra uma nova janela de consulta e cole o script a seguir para criar um procedimento armazenado que plota o histograma. Este exemplo é denominada **PlotHistogram2** para evitar conflitos de nome com o procedimento já existente.

    ```SQL
    CREATE PROCEDURE [dbo].[PlotHistogram2]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =  
      N'SELECT tipped FROM nyctaxi_sample'  
      EXECUTE sp_execute_external_script @language = N'R',  
                                         @script = N'  
       image_file = tempfile();  
       jpeg(filename = image_file);  
       #Plot histogram  
       rxHistogram(~tipped, data=InputDataSet, col=''lightgreen'',   
       title = ''Tip Histogram'', xlab =''Tipped or not'', ylab =''Counts'');  
       dev.off();  
       OutputDataSet <- data.frame(data=readBin(file(image_file, "rb"), what=raw(), n=1e6));  
       ',  
       @input_data_1 = @query  
       WITH RESULT SETS ((plot varbinary(max)));  
    END
    GO
    ```

O procedimento armazenado **PlotHistogram2** é idêntico a um procedimento armazenado pré-existente **PlotHistogram** criado pelo `RunSQL_SQL_Walkthrough.ps1` script. 
  
+ A variável `@query` define o texto da consulta (`'SELECT tipped FROM nyctaxi_sample'`), que é passado para o script do R como o argumento da variável de entrada de script, `@input_data_1`.
  
+ O script R é bem simple: uma variável do R (`image_file`) é definido para armazenar a imagem e, em seguida, o **rxHistogram** função é chamada para gerar a plotagem.
  
+ O dispositivo do R é definido como **desativar** porque você está executando este comando como um script externo no SQL Server. Normalmente em R, quando você emitir um comando de plotagem de alto nível, R é aberta uma janela de gráficos, chamada de um *dispositivo*. Você poderá alterar o tamanho e as cores e outros aspectos da janela ou desativar o dispositivo se estiver gravando em um arquivo ou tratando a saída de alguma outra forma.
  
+ O objeto gráfico do R é serializado para um data.frame do R para saída.

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>Execute o procedimento armazenado e usar o bcp para exportar os dados binários para um arquivo de imagem

O procedimento armazenado retorna a imagem como um fluxo de dados varbinary, que obviamente não pode ser exibido de forma direta. No entanto, você pode usar o utilitário **bcp** para obter os dados varbinary e salvá-los como um arquivo de imagem em um computador cliente.
  
1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], execute a seguinte instrução:
  
    ```SQL
    EXEC [dbo].[PlotHistogram]
    ```
  
    **Resultados**
    
    *plot*
    *0xFFD8FFE000104A4649...*
  
2.  Abra um prompt de comando do PowerShell e execute o seguinte comando, fornecendo o nome da instância apropriada, o nome de banco de dados, nome de usuário e as credenciais como argumentos. Para aqueles que usam identidades do Windows, você pode substituir **- U** e **-P** com **-T**.
  
     ```text
     bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  TaxiNYC_Sample  -U <user name> -P <password>
     ```

    > [!NOTE]
    > Opções de comando para bcp diferenciam maiusculas de minúsculas.
  
3.  Se a conexão for bem-sucedida, será solicitado que você insira mais informações sobre o formato de arquivo gráfico. 

   Pressione ENTER em cada prompt para aceitar os padrões, exceto para essas alterações:
    
    -   Em **comprimento do prefixo de plotagem do campo**, digite 0
  
    -   Digite **Y** se você desejar salvar os parâmetros de saída para reutilização posterior.
  
    ```
    Enter the file storage type of field plot [varbinary(max)]: 
    Enter prefix-length of field plot [8]: 0
    Enter length of field plot [0]:
    Enter field terminator [none]:
  
    Do you want to save this format information in a file? [Y/n]
    Host filename [bcp.fmt]:
    ```
  
    **Resultados**
    
    ```
    Starting copy...
    1 rows copied.
    Network packet size (bytes): 4096
    Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
    ```

    > [!TIP]
    > Se você salvar as informações de formato em um arquivo (bcp.fmt), o utilitário **bcp** vai gerar uma definição de formato que pode ser aplicada a comandos semelhantes no futuro, sem a solicitação de escolher opções de formato de arquivo gráfico. Para usar o arquivo de formato, adicione `-f bcp.fmt` ao final da linha de comando, após o argumento de senha.
  
4.  O arquivo de saída será criado no mesmo diretório em que você executou o comando do PowerShell. Para exibir a plotagem, basta abrir o arquivo plot.jpg.
  
    ![viagens de táxi com e sem gorjetas](media/rsql-devtut-tippedornot.jpg "viagens de táxi com e sem gorjetas")  
  
## <a name="create-a-stored-procedure-using-hist-and-multiple-output-formats"></a>Criar um procedimento armazenado usando Hist e vários formatos de saída

Normalmente, os cientistas de dados geram várias visualizações de dados para obter informações sobre os dados de diferentes perspectivas. Neste exemplo, o procedimento armazenado usa a função Hist para criar o histograma, exportando os dados binários para formatos populares, como. JPG. PDF, e. PNG. 

1. Use o procedimento armazenado existente **PlotInOutputFiles**, escrever histogramas, dispersões e outros gráficos de R para. JPG e. Formato PDF. O `RunSQL_SQL_Walkthrough.ps1` cria **PlotInOutputFiles** e adiciona-o banco de dados. Use o botão direito do mouse **modificar** para exibir o código-fonte.

2. Opcionalmente, como um exercício de aprendizado, crie sua própria cópia do procedimento como **PlotInOutputFiles2**, com um nome exclusivo para evitar um conflito de nomenclatura.

    Na [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra uma nova **consulta** janela e cole o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução.
  
    ```SQL
    CREATE PROCEDURE [dbo].[PlotInOutputFiles2]  
    AS  
    BEGIN  
      SET NOCOUNT ON;  
      DECLARE @query nvarchar(max) =  
      N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'  
      EXECUTE sp_execute_external_script @language = N'R',  
      @script = N'  
       # Set output directory for files and check for existing files with same names   
        mainDir <- ''C:\\temp\\plots''  
        dir.create(mainDir, recursive = TRUE, showWarnings = FALSE)  
        setwd(mainDir);  
        print("Creating output plot files:", quote=FALSE)
        
        # Open a jpeg file and output histogram of tipped variable in that file.  
        dest_filename = tempfile(pattern = ''rHistogram_Tipped_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.jpg'',sep="")  
        print(dest_filename, quote=FALSE);  
        jpeg(filename=dest_filename);  
        hist(InputDataSet$tipped, col = ''lightgreen'', xlab=''Tipped'',   
            ylab = ''Counts'', main = ''Histogram, Tipped'');  
         dev.off();  

        # Open a pdf file and output histograms of tip amount and fare amount.   
        # Outputs two plots in one row  
        dest_filename = tempfile(pattern = ''rHistograms_Tip_and_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=7);  
        par(mfrow=c(1,2));  
        hist(InputDataSet$tip_amount, col = ''lightgreen'',   
            xlab=''Tip amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram, Tip amount'', xlim = c(0,40), 100);  
        hist(InputDataSet$fare_amount, col = ''lightgreen'',   
            xlab=''Fare amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram,   
            Fare amount'',   
            xlim = c(0,100), 100);  
       dev.off();  
  
        # Open a pdf file and output an xyplot of tip amount vs. fare amount using lattice;  
        # Only 10,000 sampled observations are plotted here, otherwise file is large.  
        dest_filename = tempfile(pattern = ''rXYPlots_Tip_vs_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=4);  
        plot(tip_amount ~ fare_amount,   
            data = InputDataSet[sample(nrow(InputDataSet), 10000), ],   
            ylim = c(0,50),   
            xlim = c(0,150),   
            cex=.5,   
            pch=19,   
            col=''darkgreen'',    
            main = ''Tip amount by Fare amount'',   
            xlab=''Fare Amount ($)'',   
            ylab = ''Tip Amount ($)'');   
        dev.off();',  
     @input_data_1 = @query  
     END
    ```
  
+ A saída da consulta SELECT no procedimento armazenado é armazenada no quadro de dados padrão do R, `InputDataSet`. Várias funções de plotagem do R podem ser chamadas para gerar os arquivos gráficos reais. A maior parte do script do R inserido representa opções para essas funções gráficas, como `plot` ou `hist`.
  
+ Todos os arquivos são salvos na pasta local _C:\temp\Plots\\_. A pasta de destino é definida pelos argumentos fornecidos ao script do R como parte do procedimento armazenado.  Você pode alterar a pasta de destino alterando o valor da variável `mainDir`.

+ Para gerar os arquivos em uma pasta diferente, altere o valor da variável `mainDir` no script do R inserido no procedimento armazenado. Você também pode modificar o script para gerar formatos diferentes, mais arquivos e assim por diante.

### <a name="execute-the-stored-procedure"></a>Executar o procedimento armazenado

Execute a instrução a seguir para exportar dados de plotagem binário para formatos de arquivo JPEG e PDF.

```SQL
EXEC PlotInOutputFiles
```

**Resultados**
    
```
STDOUT message(s) from external script:
[1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 

C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]

C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
```

Os números nos nomes de arquivo são gerados aleatoriamente para garantir que você não receberá um erro ao tentar gravar em um arquivo existente.

### <a name="view-output"></a>Exibir saída 

Para exibir o gráfico, abra a pasta de destino e examine os arquivos que foram criados pelo código R no procedimento armazenado.

1. Acesse a pasta indicada na mensagem de STDOUT (no exemplo, isso é C:\temp\plots\)

2. Abra `rHistogram_Tipped.jpg` para mostrar o número de corridas que receberam uma gorjeta versus as corridas que receberam nenhuma gorjeta. (Esse histograma é parecido com o gerado na etapa anterior).

3. Abra `rHistograms_Tip_and_Fare_Amount.pdf` para exibir a distribuição de valores de gorjetas, plotado com base nos valores de tarifa.
    
  ![histograma mostrando tip_amount e fare_amount](media/rsql-devtut-tipamtfareamt.PNG "histograma mostrando tip_amount e fare_amount")

4. Abra `rXYPlots_Tip_vs_Fare_Amount.pdf` para ver uma dispersão com o valor da tarifa no eixo x e o valor da gorjeta no eixo y.

   ![valor da gorjeta plotado durante o valor da tarifa](media/rsql-devtut-tipamtbyfareamt.PNG "gorjeta plotado durante o valor da tarifa")

## <a name="next-lesson"></a>Próxima lição

[Lição 3: Criar recursos de dados usando o T-SQL](sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>Lição anterior

[Lição 1: Configurar os dados de demonstração de táxi de NYC](sqldev-download-the-sample-data.md)
