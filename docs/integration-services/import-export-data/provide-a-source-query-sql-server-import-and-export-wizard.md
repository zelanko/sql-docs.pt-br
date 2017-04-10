---
title: "Fornecer uma consulta de origem (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.providesourcequery.f1"
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
caps.latest.revision: 61
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 57
---
# Fornecer uma consulta de origem (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server)
Se você tiver especificado que deseja fornecer uma consulta para selecionar os dados a serem copiados, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará **Fornecer uma consulta de fonte**. Nessa página, você grava e testa a consulta SQL que seleciona os dados a serem copiados da fonte de dados para o destino. Você também pode colar o texto de uma consulta salva ou carregá-lo de um arquivo.

## <a name="screen-shot-of-the-source-query-page"></a>Captura de tela da página Consulta de Origem  
A captura de tela a seguir mostra a página **Fornecer uma Consulta de Tabela** do Assistente.
 
Neste exemplo simples, o usuário deseja copiar todas as linhas e todas as colunas da tabela **Sales.Customer**.
  
 ![Source query page of the Import and Export Wizard](../../integration-services/import-export-data/media/source-query.png "Source query page of the Import and Export Wizard")  

## <a name="provide-the-query-and-check-its-syntax"></a>Fornecer a consulta e verificar a sintaxe
**Instrução SQL**  
 Digite uma consulta SELECT para recuperar linhas específicas de dados do banco de dados de origem. Você também pode colar o texto de uma consulta salva ou carregá-lo de um arquivo clicando em **Carregar**. 
  
 Por exemplo, a seguinte instrução de consulta recupera **SalesPersonID**, **SalesQuota** e **SalesYTD** do banco de dados da AdventureWorks para vendedores cujo percentual de comissão for superior a 1,5 por cento.  
  
```  
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  

Se a sua fonte de dados for Excel, consulte [Fornecer uma consulta de origem para o Excel](Provide%20a%20Source%20Query%20%28SQL%20Server%20Import%20and%20Export%20Wizard%29.md\#excelQueries) mais adiante neste tópico para saber como especificar planilhas e intervalos do Excel em uma consulta.

 Para obter mais exemplos de consultas SELECT, veja [Exemplos SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md) ou pesquise online.  
  
 **Analisar**  
 Verifique a sintaxe da instrução SQL que você inseriu na caixa de texto **Instrução SQL**.  
  
> [!NOTE] Se o tempo necessário para verificar a sintaxe da instrução ultrapassar o valor de tempo limite, que é de 30 segundos, a análise será interrompida e será gerado um erro. Você não conseguirá ir além dessa página do assistente quando a análise for bem-sucedida. Uma solução possível para evitar exceder o tempo limite é criar uma exibição de banco de dados com base na consulta e consultar a exibição usando o assistente em vez de inserir o texto da consulta diretamente.  
  
 **Procurar**  
 Selecione um arquivo salvo que contém o texto de uma instrução SQL usando a caixa de diálogo **Abrir**. Selecionar um arquivo copia o texto do arquivo na caixa de texto **Instrução de SQL**.  
 
## <a name="a-nameexcelqueriesa-provide-a-source-query-for-excel"></a><a name="excelQueries"></a> Fornecer uma consulta de origem para o Excel
Há três tipos de objetos do Excel que você pode consultar.
-   **Planilha.** Para consultar uma planilha, acrescente o caractere $ ao final do nome da planilha e adicione delimitadores no começo e no final da cadeia de caracteres, por exemplo, **[Sheet1$]**.

    ```
    SELECT * FROM [Sheet1$]
    ```

-   **Intervalo nomeado.** Para consultar um intervalo nomeado, basta usar o nome do intervalo, por exemplo, **MyDataRange**.
    
    ```
    SELECT * FROM MyDataRange
    ```

-   **Intervalo sem nome.** Para especificar um intervalo de células ainda não nomeado, acrescente o caractere $ ao final do nome da planilha, adicione a especificação do intervalo e adicione delimitadores no começo e no final da cadeia de caracteres, por exemplo, **[Sheet1$A1:B4]**.

    ```
    SELECT * FROM [Sheet1$A1:B4]
    ```

Independentemente de você especificar uma planilha ou um intervalo como a tabela de origem, o driver lerá o bloco *contíguo* de células começando pela primeira célula não vazia no canto superior esquerdo da planilha ou do intervalo. Como isso, você não pode ter linhas vazias nos dados de origem. Por exemplo, você não pode ter uma linha vazia entre os cabeçalhos de coluna e as linhas de dados. Se você tiver um título seguido por linhas vazias na parte superior da planilha acima dos seus dados, não será possível consultar a planilha. No Excel, você deve atribuir um nome ao intervalo de dados e consultar o intervalo nomeado em vez da planilha.

## <a name="whats-next"></a>O que vem a seguir?  
 Depois de escrever e testar a consulta SQL que seleciona os dados a serem copiados, a próxima página depende do destino dos dados.  
  
-   Para a maioria dos destinos, a próxima página é **Selecionar Tabelas e Exibições de Origem**. Nessa página, examine a consulta que você forneceu e, opcionalmente, selecione colunas para copiar e visualizar os dados de exemplo. Para obter mais informações, consulte [Selecionar Tabelas e Exibições de Origem](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).  
  
-   Se o destino for um arquivo simples, a próxima página será **Configurar destino de arquivo simples**. Nessa página, especifique opções de formatação para o arquivo simples de destino. (Depois de configurar o arquivo simples, a página seguinte é **Selecionar Tabelas e Exibições de Origem**.) Para obter mais informações, consulte [Configurar destino arquivo simples](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
