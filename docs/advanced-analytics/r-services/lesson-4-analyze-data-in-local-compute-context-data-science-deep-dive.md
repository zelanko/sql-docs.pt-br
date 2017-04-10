---
title: "Li&#231;&#227;o 4: Analisar dados no contexto de computa&#231;&#227;o local (Aprofundamento da ci&#234;ncia de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "10/03/2016"
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
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Li&#231;&#227;o 4: Analisar dados no contexto de computa&#231;&#227;o local (Aprofundamento da ci&#234;ncia de dados)
Embora geralmente seja muito mais rápido executar código R complexo usando o contexto do servidor, às vezes, é mais conveniente extrair seus dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e analisá-los em sua estação de trabalho particular.  
  
Nesta seção, você aprenderá a voltar para um contexto de computação local e mover dados entre contextos para otimizar o desempenho.  
  
## Criar um resumo local  
  
1.  Altere o contexto de computação para fazer todo o seu trabalho localmente.  
  
    ```R  
    rxSetComputeContext ("local")    
    ```  
  
2.  Ao extrair dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], muitas vezes, é possível obter um desempenho melhor aumentando o número de linhas extraídas para cada leitura.  Para fazer isso, aumente o valor do parâmetro *rowsPerRead* na fonte de dados.  
  
    ```R  
    sqlServerDS1 <- RxSqlServerData(  
       connectionString = sqlConnString,        
       table = sqlFraudTable,   
       colInfo = ccColInfo,   
       rowsPerRead = 10000)  
    ```  
  
    Anteriormente, o valor de *rowsPerRead* estava definido como 5000.  
  
3.  Agora, chame *rxSummary* na nova fonte de dados.  
  
    ```R  
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)    
    ```  
  
    Os resultados reais devem ser iguais a quando você executa *rxSummary* no contexto do computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  No entanto, a operação pode ser mais rápida ou mais lenta. Depende muito da conexão com seu banco de dados, pois os dados estão sendo transferidos para o computador local para análise.  
  

## Próxima etapa  
[Mover dados entre o SQL Server e o arquivo XDF &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/move-data-between-sql-server-and-xdf-file-data-science-deep-dive.md)  
  
## Etapa anterior  
[Executar análise de agrupamento usando rxDataStep &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/perform-chunking-analysis-using-rxdatastep-data-science-deep-dive.md)  
  
  
  
