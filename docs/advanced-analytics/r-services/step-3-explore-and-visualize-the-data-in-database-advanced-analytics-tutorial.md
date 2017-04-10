---
title: "Etapa 3: Explorar e visualizar os dados (Tutorial de an&#225;lise avan&#231;ada no banco de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: 7fe670f3-5e62-43ef-97eb-b9af54df9128
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Etapa 3: Explorar e visualizar os dados (Tutorial de an&#225;lise avan&#231;ada no banco de dados)
Em geral, o desenvolvimento de uma solução de ciência de dados inclui intensiva exploração e visualização de dados. Nesta etapa, você vai examinar os dados de exemplo e gerar algumas plotagens usando funções do R. Essas funções do R já estão incluídas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]; neste passo a passo, você vai treinar como chamar funções do R por meio do [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## Examinar os dados  
Primeiro, reserve um minuto para examinar os dados de exemplo se você ainda não fez isso.  
  
No conjunto de dados original, os identificadores de táxi e os registros de corrida eram fornecidos em arquivos separados. No entanto, para facilitar o uso dos dados de exemplo, os dois conjuntos de dados originais foram unidos nas colunas _medallion_, _hack_license_ e _pickup_datetime_.  Também foram obtidas amostras dos registros para que fosse obtido apenas 1% do número original de registros. O conjunto de dados resultante com redução da resolução tem 1.703.957 linhas e 23 colunas.  
  
**Identificadores de táxi**  
  
-   A coluna _medallion_ representa o número de ID exclusivo do táxi.  
  
-   A coluna _hack_license_ contém o número de licença do motorista do táxi (anônimo).  
  
**Registros de corrida e tarifa**  
  
-   Cada registro de corrida inclui os locais de embarque e desembarque de passageiros, a hora e a distância da corrida.  
  
-   Cada registro de tarifa inclui informações de pagamento, como a forma de pagamento, o valor total do pagamento e o valor da gorjeta.  
  
-   As três últimas colunas podem ser usadas para várias tarefas de aprendizado de máquina.  A coluna _tip_amount_ contém valores numéricos contínuos e pode ser usada como a coluna **label** para a análise de regressão. A coluna _tipped_ tem apenas valores sim/não e é usada para classificação binária. A coluna _tip_class_ tem vários **rótulos de classe** e, portanto, pode ser usada como o rótulo para tarefas de classificação de várias classes.  
  
    Este passo a passo demonstra apenas a tarefa de classificação binária; sinta-se à vontade para tentar criar modelos para as outras duas tarefas de aprendizado de máquina, regressão e classificação de várias classes.  
  
-   Os valores usados para as colunas de rótulo se baseiam na coluna _tip_amount_, usando estas regras de negócio:  
  
    |Nome de coluna derivada|Regra|  
    |-|-|  
     |tipped|Se tip_amount > 0, tipped = 1; caso contrário, tipped = 0|  
    |tip_class|Classe 0: tip_amount = $0<br /><br />Classe 1: tip_amount > US$ 0 e tip_amount <= US$ 5<br /><br />Classe 2: tip_amount > US$ 5 e tip_amount <= US$ 10<br /><br />Classe 3: tip_amount > US$ 10 e tip_amount <= US$ 20<br /><br />Classe 4: tip_amount > $20|  
  
## Criar plotagens usando o R no T-SQL  
Como a visualização é uma ferramenta avançada para entender a distribuição dos dados e das exceções, o R fornece diversos pacotes para a visualização de dados. A distribuição de software livre padrão do R também inclui várias funções para a criação de histogramas, dispersões, gráficos de caixa e outros gráficos de exploração de dados.  
  
Normalmente, o R cria imagens usando um dispositivo do R para a saída gráfica. Você pode capturar a saída desse dispositivo e armazenar a imagem em um tipo de dados **varbinary** para renderização no aplicativo ou salvar as imagens em um dos formatos de arquivo com suporte (.JPG, .PDF, etc.).  
  
Nesta seção, você aprenderá a trabalhar com cada tipo de saída usando procedimentos armazenados.  
  
-   Armazenando plotagens como o tipo de dados varbinary  
  
-   Salvando plotagens em arquivos (.JPG, .PDF) no servidor  
  
### Armazenando plotagens como o tipo de dados varbinary  
Você usará `rxHistogram`, uma das funções avançadas do R fornecidas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para plotar um histograma com base em dados de uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para facilitar a chamada à função do R, você a encapsulará em um procedimento armazenado, _PlotHistogram_.  
  
O procedimento armazenado retorna a imagem como um fluxo de dados varbinary, que obviamente não pode ser exibido de forma direta. No entanto, você pode usar o utilitário **bcp** para obter os dados varbinary e salvá-los como um arquivo de imagem em um computador cliente.  
  
##### Para criar o procedimento armazenado PlotHistogram  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra uma nova janela de consulta.  
  
2.  Selecione o banco de dados para o passo a passo e crie o procedimento usando essa instrução.  
  
    ```  
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
  
    -   O objeto gráfico do R é serializado para um data.frame do R para saída. Essa é uma solução alternativa temporária para o CTP3.  
  
##### Para gerar dados varbinary em um arquivo gráfico visível  
  
1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], execute a seguinte instrução:  
  
    ```  
    EXEC [dbo].[PlotHistogram]  
    ```  
  
**Resultados**  
  
*plot*  
*0xFFD8FFE000104A4649...*  
  
2.  Abra um prompt de comando do PowerShell e execute o seguinte comando, fornecendo o nome da instância apropriada, o nome do banco de dados, o nome de usuário e as credenciais como argumentos:  
  
    ```  
    bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  <database name>  -U <user name> -P <password>  
  
    ```  
  
    > [!NOTE]  
    > As opções de comando do **bcp** diferenciam maiúsculas de minúsculas.  
  
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
  
*Iniciando cópia...*  
*1 linhas copiadas.*  
*Tamanho do pacote de rede (bytes): 4096*  
*Tempo de relógio (ms.) Total     : 3922   Média : (0.25 linhas/s)*  
   
> [!TIP]  
 > Se você salvar as informações de formato em um arquivo (bcp.fmt), o utilitário **bcp** vai gerar uma definição de formato que pode ser aplicada a comandos semelhantes no futuro, sem a solicitação de escolher opções de formato de arquivo gráfico. Para usar o arquivo de formato, adicione `-f bcp.fmt` ao final da linha de comando, após o argumento de senha.  
  
4.  O arquivo de saída será criado no mesmo diretório em que você executou o comando do PowerShell. Para exibir a plotagem, basta abrir o arquivo plot.jpg.  
  
    ![taxi trips with and without tips](../../advanced-analytics/r-services/media/rsql-devtut-tippedornot.jpg "taxi trips with and without tips")  
  
### Salvando plotagens em arquivos (jpg, pdf) no servidor  
A geração de uma plotagem do R em um tipo de dados binário pode ser conveniente para consumo dos aplicativos, mas não é muito útil para um cientista de dados que precisa da plotagem renderizada durante o estágio de exploração de dados. Normalmente, o cientista de dados vai gerar várias visualizações de dados, para obter informações sobre os dados de diferentes perspectivas.  
  
Para gerar gráficos que podem ser exibidos com mais facilidade, você pode usar um procedimento armazenado que cria a saída do R em formatos populares, como .JPG, .PDF e .PNG. Depois que o procedimento armazenado criar o gráfico, basta abrir o arquivo para visualizar a plotagem.  
  
Nesta etapa, você criará um novo procedimento armazenado, _PlotInOutputFiles_, que demonstra como usar as funções de plotagem do R para criar histogramas, dispersões e muito mais nos formatos .JPG e .PDF. Os arquivos gráficos são salvos em arquivos locais; ou seja, em uma pasta na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##### Para criar o procedimento armazenado PlotInOutputFiles  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra uma nova janela de consulta e cole na instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir.  
  
    ```  
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
  
    -   Todos os arquivos são salvos na pasta local _C:\temp\Plots\\_.  
  
        A pasta de destino é definida pelos argumentos fornecidos ao script do R como parte do procedimento armazenado.  Você pode alterar a pasta de destino alterando o valor da variável `mainDir`.  
  
2.  Execute a instrução para criar o procedimento armazenado.  
  
  
##### Para gerar os arquivos gráficos  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], execute a seguinte consulta SQL:  
  
    ```  
    EXEC PlotInOutputFiles  
  
    ```  
  
**Resultados**  
  
*Mensagem(ns) STDOUT do script externo:*  
*[1] Creating output plot files:[1]* *C:\\\temp\\\plots\\\rHistogram_Tipped_18887f6265d4.jpg[1]* *C:\\\temp\\\plots\\\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]* *C:\\\temp\\\plots\\\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf*  
  
2.  Abra a pasta de destino e examine os arquivos que foram criados pelo código do R no procedimento armazenado. (Os números nos nomes de arquivo são gerados aleatoriamente.)  
  
*  rHistogram_Tipped_*nnnn*.jpg: mostra o número de corridas que receberam uma gorjeta (1) versus as corridas que não receberam nenhuma gorjeta (0). Esse histograma é parecido com o gerado na etapa anterior.  
  
*  rHistograms_Tip_and_Fare_Amount_*nnnn*.pdf: mostra a distribuição dos valores nas colunas tip_amount e fare_amount.  
  
        ![histogram showing tip_amount and fare_amount](../../advanced-analytics/r-services/media/rsql-devtut-tipamtfareamt.PNG "histogram showing tip_amount and fare_amount")  
  
*  rXYPlots_Tip_vs_Fare_Amount_*nnnn*.pdf: uma dispersão com o valor da tarifa no eixo x e o valor da gorjeta no eixo y.  
  
        ![tip amount plotted over fare amount](../../advanced-analytics/r-services/media/rsql-devtut-tipamtbyfareamt.PNG "tip amount plotted over fare amount")  
  
3.  Para gerar os arquivos em uma pasta diferente, altere o valor da variável `mainDir` no script do R inserido no procedimento armazenado.  
  
    Você também pode modificar o script para gerar formatos diferentes, mais arquivos e assim por diante.  
  
## Próxima etapa  
[Etapa 4: Criar recursos de dados usando o T-SQL](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## Etapa anterior  
[Etapa 2: Importar dados para o SQL Server usando o PowerShell](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md)  
  
## Consulte também  
[Análise avançada no banco de dados para desenvolvedores do SQL &#40;Tutorial&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[Tutoriais do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
