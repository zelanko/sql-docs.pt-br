---
title: "Forneça uma consulta de origem (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 190c39de92d8fc1b559f43c90c95e446ccc87272
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>Fornecer uma consulta de origem (Assistente de Importação e Exportação do SQL Server)
Se você tiver especificado que deseja fornecer uma consulta para selecionar os dados a serem copiados, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará **Fornecer uma consulta de fonte**. Nessa página, você grava e testa a consulta SQL que seleciona os dados a serem copiados da fonte de dados para o destino. Você também pode colar o texto de uma consulta salva, ou carregar o texto da consulta de um arquivo.

## <a name="screen-shot-of-the-source-query-page"></a>Captura de tela da página Consulta de Origem  
A captura de tela a seguir mostra a página **Fornecer uma Consulta de Tabela** do Assistente.
 
Neste exemplo simples, o usuário tiver inserido a consulta `SELECT * FROM Sales.Customer` para copiar todas as linhas e todas as colunas da **Sales. Customer** tabela no banco de dados de origem.
-   `SELECT *`significa copia todas as colunas.
-   A ausência de um `WHERE` cláusula significa copiar todas as linhas.
  
 ![Página de consulta de fonte do Assistente de importação e exportação](../../integration-services/import-export-data/media/source-query.png "página de consulta de fonte do Assistente de importação e exportação")  

## <a name="provide-the-query-and-check-its-syntax"></a>Fornecer a consulta e verificar a sintaxe
**Instrução SQL**  
 Digite uma consulta SELECT para recuperar linhas e colunas de dados do banco de dados de origem. Você também pode colar o texto de uma consulta salva ou carregar a consulta de um arquivo clicando em **procurar**. 
  
 Por exemplo, a consulta a seguir recupera o **SalesPersonID**, **SalesQuota**, e **SalesYTD** do exemplo da AdventureWorks do banco de dados para vendedores cuja Porcentagem de comissão for superior a 1,5 por cento.  
  
```sql
SELECT SalesPersonID, SalesQuota, SalesYTD  
FROM Sales.SalesPerson  
WHERE CommissionPct > 0.015  
```  

Para obter mais exemplos de consultas SELECT, veja [Exemplos SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-examples-transact-sql.md) ou pesquise online.  

Se a sua fonte de dados for Excel, consulte [Fornecer uma consulta de origem para o Excel](#excelQueries) mais adiante neste tópico para saber como especificar planilhas e intervalos do Excel em uma consulta.
  
 **Analisar**  
 Verifique a sintaxe da instrução SQL que você inseriu na caixa de texto **Instrução SQL** .  
  
> [!NOTE]
> Se o tempo necessário para verificar a sintaxe da instrução ultrapassar o valor de tempo limite, que é de 30 segundos, a análise será interrompida e será gerado um erro. Você não conseguirá ir além dessa página do assistente quando a análise for bem-sucedida. Uma solução possível para evitar exceder o tempo limite é criar uma exibição de banco de dados com base na consulta e consultar a exibição usando o assistente em vez de inserir o texto da consulta diretamente.  
  
 **Procurar**  
 Selecione um arquivo salvo que contém o texto de uma consulta SQL usando o **abrir** caixa de diálogo. Selecionar um arquivo copia o texto do arquivo na caixa de texto **Instrução de SQL** .  
 
## <a name="excelQueries"></a> Fornecer uma consulta de origem para o Excel
### <a name="specify-excel-objects-in-queries"></a>Especificar objetos do Excel em consultas
Há três tipos de objetos do Excel que você pode consultar.
-   **Planilha.** Para consultar uma planilha, acrescente o caractere $ ao final do nome da planilha e adicione delimitadores no começo e no final da cadeia de caracteres, por exemplo, **[Sheet1$]**.

    ```sql
    SELECT * FROM [Sheet1$]
    ```

-   **Intervalo nomeado.** Para consultar um intervalo nomeado, basta usar o nome do intervalo, por exemplo, **MyDataRange**.
    
    ```sql
    SELECT * FROM MyDataRange
    ```

-   **Intervalo sem nome.** Para especificar um intervalo de células ainda não nomeado, acrescente o caractere $ ao final do nome da planilha, adicione a especificação do intervalo e adicione delimitadores no começo e no final da cadeia de caracteres, por exemplo, **[Sheet1$A1:B4]**.

    ```sql
    SELECT * FROM [Sheet1$A1:B4]
    ```

### <a name="prepare-the-excel-source-data"></a>Preparar os dados de origem do Excel
Independentemente de você especificar uma planilha ou um intervalo como a tabela de origem, o driver lerá o bloco *contíguo* de células começando pela primeira célula não vazia no canto superior esquerdo da planilha ou do intervalo. Como isso, você não pode ter linhas vazias nos dados de origem. Por exemplo, você não pode ter uma linha vazia entre os cabeçalhos de coluna e as linhas de dados. Se você tiver um título seguido por linhas vazias na parte superior da planilha acima dos seus dados, não será possível consultar a planilha. No Excel, você deve atribuir um nome ao intervalo de dados e consultar o intervalo nomeado em vez da planilha.

## <a name="whats-next"></a>O que vem a seguir?  
 Depois de escrever e testar a consulta SQL que seleciona os dados a serem copiados, a próxima página depende do destino dos dados.  
  
-   Para a maioria dos destinos, a próxima página é **Selecionar Tabelas e Exibições de Origem**. Nessa página, examine a consulta que você forneceu e, opcionalmente, selecione colunas para copiar e visualizar os dados de exemplo. Para obter mais informações, consulte [Selecionar Tabelas e Exibições de Origem](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).  
  
-   Se o destino for um arquivo simples, a próxima página será **Configurar destino de arquivo simples**. Nessa página, especifique opções de formatação para o arquivo simples de destino. (Depois de configurar o arquivo simples, a página seguinte é **Selecionar Tabelas e Exibições de Origem**.) Para obter mais informações, consulte [Configurar destino arquivo simples](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  



