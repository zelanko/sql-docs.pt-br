---
title: Exemplos de expressões avançadas do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- functions [Integration Services]
- operators [Integration Services]
- expressions [Integration Services], examples
- examples [Integration Services]
ms.assetid: c7794ba3-0de5-466b-ae8a-9ddd27360049
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9272a6c11ce226f385c0b1f79f965a2a0f55835e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62901117"
---
# <a name="examples-of-advanced-integration-services-expressions"></a>Exemplos de expressões avançadas do Integration Services
  Esta seção fornece exemplos de expressões avançadas que combinam múltiplos operadores e funções. Se uma expressão for usada em uma restrição precedente ou na transformação Divisão Condicional, ela deve ser avaliada como uma expressão Booleana. No entanto, essa restrição não se aplica a expressões usadas em expressões de propriedades, variáveis, na transformação Coluna Derivada ou no contêiner Loop For.  
  
 Os exemplos a seguir usam os bancos de dados **AdventureWorks** e bancos de dados [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada exemplo identifica as tabelas que usa.  
  
## <a name="boolean-expressions"></a>Expressões boolianas  
  
-   Este exemplo usa a tabela **Product** . A expressão avaliará a entrada do mês na coluna **SellStartDate** e retornará TRUE se o mês for junho ou posterior.  
  
    ```  
    DATEPART("mm",SellStartDate) > 6  
    ```  
  
-   Este exemplo usa a tabela **Product** . A expressão avaliará o resultado arredondado da divisão da coluna **ListPrice** pela coluna **StandardCost** e retornará TRUE se o resultado for maior que 1,5.  
  
    ```  
    ROUND(ListPrice / StandardCost,2) > 1.50  
    ```  
  
-   Este exemplo usa a tabela **Product** . A expressão retornará TRUE se todas as três operações forem avaliadas como TRUE. Se a coluna **Size** e a variável **BikeSize** tiverem tipos de dados incompatíveis, a expressão exigirá uma conversão explícita conforme demonstra o segundo exemplo. A conversão para DT_WSTR inclui o comprimento da cadeia de caracteres.  
  
    ```  
    MakeFlag ==  TRUE && FinishedGoodsFlag == TRUE && Size != @BikeSize  
    MakeFlag ==  TRUE && FinishedGoodsFlag == TRUE  && Size != (DT_WSTR,10)@BikeSize  
    ```  
  
-   Este exemplo usa a tabela **CurrencyRate** . A expressão compara valores em tabelas e variáveis. Ela retornará TRUE se as entradas nas colunas **FromCurrencyCode** ou **ToCurrencyCode** forem iguais a valores variáveis e se o valor em **AverageRate** for maior do que o valor em **EndOfDayRate**.  
  
    ```  
    (FromCurrencyCode == @FromCur || ToCurrencyCode == @ToCur) && AverageRate > EndOfDayRate  
    ```  
  
-   Este exemplo usa a tabela **Currency** . A expressão retornará TRUE se o primeiro caractere na coluna **Name** não for a ou A.  
  
    ```  
    SUBSTRING(UPPER(Name),1,1) != "A"  
    ```  
  
     A expressão a seguir fornece os mesmos resultados, mas é mais eficiente porque somente um caractere é convertido em maiúsculas.  
  
    ```  
    UPPER(SUBSTRING(Name,1,1)) != "A"  
    ```  
  
## <a name="non-boolean-expressions"></a>Expressões não Booleanas  
 Expressões não Booleanas são usadas na transformação Coluna Derivada, expressões de propriedade e no contêiner Loop For.  
  
-   Este exemplo usa a tabela **Contato** . A expressão remove os espaços à esquerda e à direita das colunas **FirstName**, **MiddleName**e **LastName** . Ela extrairá a primeira letra da coluna **MiddleName** se não for nula, concatenará a inicial do segundo nome e os valores em **FirstName** e **LastName**e inserirá os espaços apropriados entre os valores.  
  
    ```  
    TRIM(FirstName) + " " + (!ISNULL(MiddleName) ? SUBSTRING(MiddleName,1,1) + " " : "") + TRIM(LastName)  
    ```  
  
-   Este exemplo usa a tabela **Contato** . A expressão valida entradas na coluna **Salutation** . Retorna uma entrada **Salutation** ou uma cadeia de caracteres vazia.  
  
    ```  
    (Salutation == "Sr." || Salutation == "Ms." || Salutation == "Sra." || Salutation == "Mr.") ? Salutation : ""  
    ```  
  
-   Este exemplo usa a tabela **Product** . A expressão converte o primeiro caractere na coluna **Color** em maiúscula e converte os caracteres restantes em minúsculas.  
  
    ```  
    UPPER(SUBSTRING(Color,1,1)) + LOWER(SUBSTRING(Color,2,15))  
    ```  
  
-   Este exemplo usa a tabela **Product** . A expressão calculará o número de meses em que um produto foi vendido e retornará a cadeia de caracteres “Desconhecido” se a coluna **SellStartDate** ou a coluna **SellEndDate** contiver NULL.  
  
    ```  
    !(ISNULL(SellStartDate)) && !(ISNULL(SellEndDate)) ? (DT_WSTR,2)DATEDIFF("mm",SellStartDate,SellEndDate) : "Unknown"  
    ```  
  
-   Este exemplo usa a tabela **Product** . A expressão calcula a marcação na coluna **StandardCost** e arredonda o resultado a uma precisão de dois. O resultado é apresentado como uma porcentagem.  
  
    ```  
    ROUND(ListPrice / StandardCost,2) * 100  
    ```  
  
## <a name="related-tasks"></a>Related Tasks  
 [Usar uma expressão em um componente de fluxo de dados](../use-an-expression-in-a-data-flow-component.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Artigo técnico, [SSIS Expression Cheat Sheet](https://pragmaticworks.com/Resources/Cheat-Sheets/SSIS-Expression-Cheat-Sheet), em pragmaticworks.com  
  
  
