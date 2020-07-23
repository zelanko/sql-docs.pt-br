---
title: Fornecer uma consulta de origem (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.providesourcequery.f1
ms.assetid: c8cbd07e-b9c3-422f-94b8-d6fc8cf31cf5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 267db7655133669266b9fc0c9f6b54819333a6fa
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920155"
---
# <a name="provide-a-source-query-sql-server-import-and-export-wizard"></a>Fornecer uma consulta de origem (Assistente de Importação e Exportação do SQL Server)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


Se você tiver especificado que deseja fornecer uma consulta para selecionar os dados a serem copiados, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará **Fornecer uma consulta de fonte**. Nessa página, você grava e testa a consulta SQL que seleciona os dados a serem copiados da fonte de dados para o destino. Você também pode colar o texto de uma consulta salva ou carregá-lo de um arquivo.

## <a name="screen-shot-of-the-source-query-page"></a>Captura de tela da página Consulta de Origem  
A captura de tela a seguir mostra a página **Fornecer uma Consulta de Tabela** do Assistente.
 
Neste exemplo simples, o usuário inseriu a consulta `SELECT * FROM Sales.Customer` para copiar todas as linhas e todas as colunas da tabela **Sales.Customer** no banco de dados de origem.
-   `SELECT *` significa copiar todas as colunas.
-   A ausência de uma cláusula `WHERE` significa copiar todas as linhas.
  
 ![Página Consulta de origem do Assistente de Importação e Exportação](../../integration-services/import-export-data/media/source-query.png "Página Consulta de origem do Assistente de Importação e Exportação")  

## <a name="provide-the-query-and-check-its-syntax"></a>Fornecer a consulta e verificar a sintaxe
**Instrução SQL**  
 Digite uma consulta SELECT para recuperar linhas e colunas específicas de dados do banco de dados de origem. Você também pode colar o texto de uma consulta salva ou carregar a consulta de um arquivo clicando em **Procurar**. 
  
 Por exemplo, a seguinte instrução de consulta recupera **SalesPersonID**, **SalesQuota** e **SalesYTD** do banco de dados de exemplo da AdventureWorks para vendedores cujo percentual de comissão é superior a 1,5%.  
  
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
 Selecione um arquivo salvo que contém o texto de uma consulta SQL usando a caixa de diálogo **Abrir**. Selecionar um arquivo copia o texto do arquivo na caixa de texto **Instrução de SQL** .  
 
## <a name="provide-a-source-query-for-excel"></a><a name="excelQueries"></a> Fornecer uma consulta de origem para o Excel

> [!IMPORTANT]
> Para obter informações detalhadas sobre como se conectar a arquivos do Excel, e sobre limitações e problemas conhecidos para carregar dados de ou para arquivos do Excel, consulte [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md).

Há três tipos de objetos do Excel que você pode consultar.
-   **Planilha.** Para consultar uma planilha, acrescente o caractere $ ao final do nome da planilha e adicione delimitadores no começo e no final da cadeia de caracteres, por exemplo, **[Sheet1$]** .

    ```sql
    SELECT * FROM [Sheet1$]
    ```

-   **Intervalo nomeado.** Para consultar um intervalo nomeado, basta usar o nome do intervalo, por exemplo, **MyDataRange**.
    
    ```sql
    SELECT * FROM MyDataRange
    ```

-   **Intervalo sem nome.** Para especificar um intervalo de células ainda não nomeado, acrescente o caractere $ ao final do nome da planilha, adicione a especificação do intervalo e adicione delimitadores no começo e no final da cadeia de caracteres, por exemplo, **[Sheet1$A1:B4]** .

    ```sql
    SELECT * FROM [Sheet1$A1:B4]
    ```

## <a name="whats-next"></a>O que vem a seguir?  
 Depois de escrever e testar a consulta SQL que seleciona os dados a serem copiados, a próxima página depende do destino dos dados.  
  
-   Para a maioria dos destinos, a próxima página é **Selecionar Tabelas e Exibições de Origem**. Nessa página, examine a consulta que você forneceu e, opcionalmente, selecione colunas para copiar e visualizar os dados de exemplo. Para obter mais informações, consulte [Selecionar Tabelas e Exibições de Origem](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md).  
  
-   Se o destino for um arquivo simples, a próxima página será **Configurar destino de arquivo simples**. Nessa página, especifique opções de formatação para o arquivo simples de destino. (Depois de configurar o arquivo simples, a página seguinte é **Selecionar Tabelas e Exibições de Origem**.) Para obter mais informações, consulte [Configurar destino arquivo simples](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  


