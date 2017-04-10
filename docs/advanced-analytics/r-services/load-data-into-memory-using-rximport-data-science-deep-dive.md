---
title: "Carregar dados na mem&#243;ria usando rxImport (Aprofundamento da ci&#234;ncia de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
ms.assetid: 47a42e9a-05a0-4a50-871d-de73253cf070
caps.latest.revision: 14
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Carregar dados na mem&#243;ria usando rxImport (Aprofundamento da ci&#234;ncia de dados)
A função *rxImport* pode ser usada para mover dados de uma fonte de dados para um quadro de dados na memória da sessão em R ou para um arquivo XDF em disco. Se você não especificar um arquivo como destino, os dados serão colocados na memória como um quadro de dados.  
  
Nesta etapa, você aprenderá a obter dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usar a função *rxImport* para colocar os dados de seu interesse em um arquivo local. Dessa forma, você pode analisá-los no contexto de computação local repetidamente, sem precisar consultar o banco de dados novamente.  
  
## Extrair um subconjunto de dados do SQL Server para a memória local  
Você decidiu que deseja examinar somente os indivíduos de alto risco mais detalhadamente. A tabela de origem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é grande e, portanto, você obterá as informações apenas sobre os clientes alto risco e os carregará em um quadro de dados na memória da estação de trabalho local.  
  
1.  Redefina o contexto de computação como a estação de trabalho local.  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
2.  Crie um novo objeto de fonte de dados do SQL Server, fornecendo uma instrução SQL válida no parâmetro *sqlQuery*. Este exemplo obtém um subconjunto das observações com as classificações de risco mais altas. Dessa forma, somente os dados que você realmente precisa são colocados na memória local.  
  
    ```R    
    sqlServerProbDS <- RxSqlServerData(       
        sqlQuery = paste("SELECT * FROM ccScoreOutput2",  
        "WHERE (ccFraudProb > .99)"),
        connectionString = sqlConnString)   
    ```  
  
3.  Use a função *rxImport* para de fato carregar os dados em um quadro de dados na sessão em R local.  
  
    ```R  
    highRisk <- rxImport(sqlServerProbDS)   
    ```  
     Se a operação for bem-sucedida, você verá uma mensagem de status: Linhas Lidas: 35, Total de Linhas Processadas: 35, Tempo Total para a Parte: 0,036 segundos 
   
4.  Agora que tem as observações de alto risco em um quadro de dados na memória, você pode usar várias funções de R para manipular o quadro de dados. Por exemplo, você pode ordenar os clientes pela pontuação de risco e imprimir os clientes que apresentam o maior risco.  
  
    ```R  
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]   
    row.names(orderedHighRisk) <- NULL    
    head(orderedHighRisk)  
  
    ```  
  
 **Resultados**  
  
 *ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1*  
*9.786345    SD   Male  Principal   23456       25            5 75   0.99994382*  
*9.433040    FL Female  Principal   20629       24           28 75   0.99992003*  
*8.556785    NY Female  Principal   19064       82           53 43   0.99980784*  
*8.188668    AZ Female  Principal   19948       29            0 75   0.99972235*  
*7.551699    NY Female  Principal   11051       95            0 75   0.99947516*  
*7.335080    NV   Male  Principal   21566        4            6  75   0.9993482*  
  
## Mais sobre rxImport  
Você pode usar *rxImport* não apenas para mover os dados, mas para transformar os dados no processo de leitura. Por exemplo, é possível especificar o número de caracteres para colunas de largura fixa, fornecer uma descrição das variáveis, definir níveis de colunas de fator e, até mesmo, criar novos níveis a serem usados após a importação.  
  
A função *rxImport* atribui nomes de variáveis às colunas durante o processo de importação, mas você pode indicar novos nomes de variáveis usando o parâmetro *colInfo* ou alterar os tipos de dados usando o parâmetro *colClasses*.  
  
Ao especificar outras operações no parâmetro *transforms*, você pode fazer o processamento básico em cada parte dos dados que é lida.  
  
## Próxima etapa  
[Criar nova tabela do SQL Server usando rxDataStep &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/create-new-sql-server-table-using-rxdatastep-data-science-deep-dive.md)  
  
## Etapa anterior  
[Lição 3: Transformar dados usando o R &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
## Consulte também  
[Tutoriais do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
