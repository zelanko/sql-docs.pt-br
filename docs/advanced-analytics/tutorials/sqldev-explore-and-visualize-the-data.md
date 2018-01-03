---
title: "Lição 3: Explorar e visualizar os dados | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 7fe670f3-5e62-43ef-97eb-b9af54df9128
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9a47e9d2b2bec007af27b8e8ce26d6a6c6f67c3f
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="lesson-3-explore-and-visualize-the-data"></a>Lição 3: Explorar e visualizar os dados

Este artigo faz parte de um tutorial para desenvolvedores em SQL sobre como usar o R no SQL Server.

Nesta lição, você vai examinar os dados de exemplo e, em seguida, gerar alguns gráficos usando funções de R. Essas funções de R já estão incluídas na [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Você pode chamar as funções R [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="review-the-data"></a>Revise os dados

Em geral, o desenvolvimento de uma solução de ciência de dados inclui intensiva exploração e visualização de dados. Primeiro, reserve um minuto para examinar os dados de exemplo, se ainda não o fez.

No conjunto de dados original, os identificadores de táxi e os registros de corrida eram fornecidos em arquivos separados. No entanto, para facilitar a usar os dados de exemplo, dois conjuntos de dados originais tiveram ingressados nas colunas _medallion_, _hack\_licença_, e _retirada\_ DateTime_.  Também foram obtidas amostras dos registros para que fosse obtido apenas 1% do número original de registros. O conjunto de dados resultante com redução da resolução tem 1.703.957 linhas e 23 colunas.

**Identificadores de táxi**
  
-   A coluna _medallion_ representa o número de ID exclusivo do táxi.
  
-   O _hack\_licença_ coluna contém o número de licença do driver táxi (anônimos).
  
**Registros de corrida e tarifa**
  
-   Cada registro de corrida inclui os locais de embarque e desembarque de passageiros, a hora e a distância da corrida.
  
-   Cada registro de tarifa inclui informações de pagamento, como a forma de pagamento, o valor total do pagamento e o valor da gorjeta.
  
-   As três últimas colunas podem ser usadas para várias tarefas de aprendizado de máquina.  O _dica\_quantidade_ coluna contém valores numéricos contínuos e pode ser usada como o **rótulo** coluna para análise de regressão. A coluna _tipped_ tem apenas valores sim/não e é usada para classificação binária. O _dica\_classe_ coluna tem vários **rótulos de classe** e, portanto, pode ser usado como o rótulo para tarefas de classificação multiclasse.
  
    Este passo a passo demonstra apenas a tarefa de classificação binária; sinta-se à vontade para tentar criar modelos para as outras duas tarefas de aprendizado de máquina, regressão e classificação de várias classes.
  
-   Os valores usados para as colunas de rótulo se baseiam no _dica\_quantidade_ coluna, usando essas regras de negócio:
  
    |Nome de coluna derivada|Regra|
    |-|-|
     |tipped|Se tip_amount > 0, tipped = 1; caso contrário, tipped = 0|
    |tip_class|Classe 0: tip_amount = $0<br /><br />Classe 1: tip_amount > US$ 0 e tip_amount <= US$ 5<br /><br />Classe 2: tip_amount > US$ 5 e tip_amount <= US$ 10<br /><br />Classe 3: tip_amount > US$ 10 e tip_amount <= US$ 20<br /><br />Classe 4: tip_amount > $20|

## <a name="create-plots-using-r-in-t-sql"></a>Criar gráficos usando o R em T-SQL

Como a visualização é uma ferramenta avançada para entender a distribuição dos dados e das exceções, o R fornece diversos pacotes para a visualização de dados. A distribuição de software livre padrão do R também inclui várias funções para a criação de histogramas, dispersões, gráficos de caixa e outros gráficos de exploração de dados.

Normalmente, o R cria imagens usando um dispositivo do R para a saída gráfica. Você pode capturar a saída desse dispositivo e armazenar a imagem em um tipo de dados **varbinary** para renderização no aplicativo ou salvar as imagens em um dos formatos de arquivo com suporte (.JPG, .PDF, etc.).

Nesta seção, você aprenderá a trabalhar com cada tipo de saída usando procedimentos armazenados. O processo geral é o seguinte:

- Criar um procedimento armazenado para gerar um gráfico de R como dados varbinary

- Gerar a plotagem e salvá-lo em um arquivo de imagem

- Use um procedimento armazenado para converter os binário plotar dados em um arquivo JPG ou PDF

### <a name="create-the-stored-procedure-plothistogram"></a>Criar o procedimento armazenado PlotHistogram

1. Para criar o gráfico, use `rxHistogram`, uma das funções de R aprimoradas fornecidas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]para plotar um histograma com base em dados de um [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. Para facilitar a chamada à função do R, você a encapsulará em um procedimento armazenado, _PlotHistogram_.

    Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra uma nova **consulta** janela.

2. No banco de dados que contém os dados do tutorial, crie o procedimento usando esta instrução:

    ```SQL
    CREATE PROCEDURE [dbo].[PlotHistogram]
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

    Lembre-se de modificar o código para usar o nome de tabela correto, se necessário.
  
    -   A variável `@query` define o texto da consulta (`'SELECT tipped FROM nyctaxi_sample'`), que é passado para o script do R como o argumento da variável de entrada de script, `@input_data_1`.
  
    -   O script do R é bem simples: uma variável do R (`image_file`) é definido para armazenar a imagem e a função do `rxHistogram` é chamada para gerar a plotagem.
  
    -   O dispositivo do R é definido como **desativado**.
  
        No R, quando você emite um comando de plotagem de alto nível, o R abrirá uma janela de gráficos, chamada um *dispositivo*. Você poderá alterar o tamanho e as cores e outros aspectos da janela ou desativar o dispositivo se estiver gravando em um arquivo ou tratando a saída de alguma outra forma.
  
    -   O objeto gráfico do R é serializado para um data.frame do R para saída.

### <a name="generate-the-graphics-data-and-save-to-file"></a>Gerar os dados de gráficos e salvar arquivo

O procedimento armazenado retorna a imagem como um fluxo de dados varbinary, que obviamente não pode ser exibido de forma direta. No entanto, você pode usar o utilitário **bcp** para obter os dados varbinary e salvá-los como um arquivo de imagem em um computador cliente.
  
1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], execute a seguinte instrução:
  
    ```SQL
    EXEC [dbo].[PlotHistogram]
    ```
  
    **Resultados**
    
    *plotagem*
    *0xFFD8FFE000104A4649...*
  
2.  Abra um prompt de comando do PowerShell e execute o seguinte comando, fornecendo o nome da instância apropriada, o nome do banco de dados, o nome de usuário e as credenciais como argumentos:
  
     ```
     bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  <database name>  -U <user name> -P <password>
     ```

    > [!NOTE]
    > Opções de comando para bcp diferenciam maiusculas de minúsculas.
  
3.  Se a conexão for bem-sucedida, será solicitado que você insira mais informações sobre o formato de arquivo gráfico. Pressione ENTER em cada prompt para aceitar os padrões, exceto para essas alterações:
  
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
  
### <a name="export-the-plot-data-to-a-viewable-file"></a>Exportar os dados de plotagem para um arquivo visível

Gerando um gráfico de R em um binário de dados tipo pode ser conveniente para consumo por aplicativos, mas não é muito útil para um cientista de dados que precisa de plotagem renderizada durante a fase de exploração de dados. Normalmente, o cientista de dados vai gerar várias visualizações de dados, para obter informações sobre os dados de diferentes perspectivas.

Para gerar gráficos para os usuários, você pode usar um procedimento armazenado que cria a saída de R em formatos populares, como. JPG. PDF, e. PNG. Depois que o procedimento armazenado criar o gráfico, basta abrir o arquivo para visualizar a plotagem.

1. Criar um novo procedimento armazenado, _PlotInOutputFiles_, que demonstra como gravar histogramas, scatterplots e outros gráficos de R para. JPG e. Formato PDF.

    Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra uma nova **consulta** janela e cole o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução.
  
    ```SQL
    CREATE PROCEDURE [dbo].[PlotInOutputFiles]  
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
  
    -   A saída da consulta SELECT no procedimento armazenado é armazenada no quadro de dados padrão do R, `InputDataSet`. Várias funções de plotagem do R podem ser chamadas para gerar os arquivos gráficos reais.
  
        A maior parte do script do R inserido representa opções para essas funções gráficas, como `plot` ou `hist`.
  
    -   Todos os arquivos são salvos na pasta local _C:\temp\Plots\\_. A pasta de destino é definida pelos argumentos fornecidos ao script do R como parte do procedimento armazenado.  Você pode alterar a pasta de destino alterando o valor da variável `mainDir`.
  
2.  Execute a instrução para criar o procedimento armazenado.

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

    Os números nos nomes de arquivo são gerados aleatoriamente para garantir que você não receber um erro ao tentar gravar em um arquivo existente.

3. Para exibir o gráfico, abra a pasta de destino e revise os arquivos que foram criados pelo código R no procedimento armazenado.

    + O arquivo `rHistogram_Tipped.jpg` mostra o número de viagens que tem uma dica versus as viagens que não obteve nenhuma dica. (Esse histograma é parecido com o gerado na etapa anterior.)

    + O arquivo `rHistograms_Tip_and_Fare_Amount.pdf` mostra a distribuição de valores de ponta, plotada em relação à quantidade de passagens.
    
    ![histograma mostrando tip_amount e fare_amount](media/rsql-devtut-tipamtfareamt.PNG "histograma mostrando tip_amount e fare_amount")

    + O arquivo `rXYPlots_Tip_vs_Fare_Amount.pdf` contém um scatterplot com a quantidade de passagens no eixo x e o valor de dica no eixo y.

    ![quantidade de dica plotado durante o período de tarifa](media/rsql-devtut-tipamtbyfareamt.PNG "quantidade dica plotados pela quantidade de passagens")

2.  Para gerar os arquivos em uma pasta diferente, altere o valor da variável `mainDir` no script do R inserido no procedimento armazenado. Você também pode modificar o script para gerar formatos diferentes, mais arquivos e assim por diante.

## <a name="next-lesson"></a>Próxima lição

[Lição 4: Criar recursos de dados usando o T-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>Lição anterior

[Lição 2: Importar dados para o SQL Server usando o PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)
