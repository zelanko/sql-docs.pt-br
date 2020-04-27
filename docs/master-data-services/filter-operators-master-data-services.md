---
title: Operadores de filtro
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 27914c8b-8951-4b7d-914d-1cbf528dd248
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 2127678ec9e6afbb17944ec80308e2e5e4bb440f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73729196"
---
# <a name="filter-operators-master-data-services"></a>Operadores de filtro (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Ao filtrar uma lista de membros, os seguintes operadores estão disponíveis.  
  
> [!NOTE]  
>  Quando você filtrar por vários critérios, todos os critérios devem ser verdadeiros para retornar resultados. Por exemplo, SquareFeet = 2000 **AND** Division <> 123.  
  
## <a name="filter-operators"></a>Operadores de filtro  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**É igual a**|Retorna valores de atributo que são exatamente iguais aos critérios especificados. Por exemplo, para filtrar por **Mountain-100**, você deve digitar **Mountain-100**.|  
|**Não é igual a**|Retorna valores de atributo que não são exatamente iguais aos critérios especificados. Os critérios de filtragem devem ser exatamente iguais ao valor do atributo que você deseja omitir dos resultados. Por exemplo, para omitir resultados que correspondam a **Mountain-100**, você deve digitar **Mountain-100**.<br /><br /> <br /><br /> Observação: quando você aplica uma condição de filtro com uma cláusula "Não é igual a" em um atributo, um membro para o qual o atributo é NULL transmitirá a condição de filtro e será retornado se SET ANSI_NULLS estiver definido como ON em suas configurações de banco de dados. Para interromper esse comportamento, defina SET ANSI_NULLS como OFF em suas configurações de banco de dados. Quando SET ANSI_NULLS é definido como OFF, as comparações de todos os dados com um valor nulo serão avaliadas como TRUE se o valor dos dados for NULL, com o resultado de que o membro não transmite a cláusula "Não é igual a". Para obter mais informações, consulte [SET ANSI_NULLS &#40;Transact-SQL&#41;](../t-sql/statements/set-ansi-nulls-transact-sql.md).|  
|**É como**|Usa o operador LIKE do Transact-SQL para filtrar resultados. Para obter mais informações, consulte [LIKE &#40;Transact-SQL&#41;](../t-sql/language-elements/like-transact-sql.md) nos Manuais Online do SQL Server.|  
|**Não é como**|Usa o operador NOT do Transact-SQL para filtrar resultados. Para obter mais informações, consulte [NOT &#40;Transact-SQL&#41;](../t-sql/language-elements/not-transact-sql.md) nos Manuais Online do SQL Server.|  
|**É maior que**|Retorna valores de atributo que são maiores que os critérios especificados. Por exemplo, para retornar valores de atributo que começam com uma letra maior que **F**, digite **F**.|  
|**É menor que**|Retorna valores de atributo que são menores que os critérios especificados. Por exemplo, para retornar valores de atributo que começam com uma letra menor que **F**, digite **F**.|  
|**É maior ou igual a**|Retorna valores de atributo que são maiores ou iguais aos critérios especificados. Por exemplo, para retornar valores de atributo que começam com o número **3** ou maior, digite **3**.|  
|**É menor ou igual a**|Retorna valores de atributo que são menores ou iguais aos critérios especificados. Por exemplo, para retornar valores de atributo que começam com o número **3** ou menor, digite **3**.|  
|**Acordo**|Usa um índice de pesquisa difuso para filtrar resultados.<br /><br /> Use o campo **Nível de Similaridade** para especificar a exatidão com a qual os valores de atributo devem corresponder aos critérios de filtragem especificados (com padrão de 30%).<br /><br /> Selecione uma das opções na caixa de listagem **Algoritmo** :<br /><br /> **Levenshtein**: uma distância baseada no número de edições (por exemplo, adições ou exclusões) necessárias para uma cadeia de caracteres corresponder a outra. Esse é o padrão. Não requer parâmetros adicionais.<br /><br /> **Jaccard**: um índice que funciona melhor ao tentar corresponder várias cadeias de caracteres. Essa pesquisa oferece suporte a um parâmetro adicional de tendência de retenção (veja abaixo).<br /><br /> **Jaro-Winkler**: uma distância que é mais bem usada para localizar nomes de pessoas duplicados. Esse método retorna mais resultados que qualquer outro método. Não oferece suporte para tendência de contenção.<br /><br /> **Subsequência comum mais longa**: funciona com base em uma subsequência na qual as letras em um padrão aparecem em ordem, embora possam ser separadas (por exemplo, "MSR" é uma subsequência de "MaSteR"). Essa pesquisa oferece suporte a um parâmetro adicional de tendência de retenção (veja abaixo).<br /><br /> <br /><br /> Observações: para o algoritmo **Jaccard** ou **Subsequência Comum Mais longa** adicionar um **Tendência de Contenção**. Esse é um limite de comprimento fornecido em uma porcentagem decimal entre 0 e 1, com um padrão de 0,62. Um limite inferior aumentará o número de possíveis correspondências retornadas.|  
|**Não corresponde**|Usa um índice de pesquisa difuso para filtrar resultados. Use o campo **Nível de Similaridade** para especificar a exatidão com a qual os valores de atributo não devem corresponder aos critérios de filtragem especificados.|  
|**Contém o padrão**|Usa expressões regulares do .NET Framework para filtrar resultados em um padrão especificado. Para obter mais informações sobre expressões regulares, consulte [Elementos de linguagem das expressões regulares](https://go.microsoft.com/fwlink/?LinkId=164401) na Biblioteca MSDN.|  
|**Não contém o padrão**|Usa expressões regulares do .NET Framework para filtrar resultados que não correspondam a um padrão especificado. Para obter mais informações sobre expressões regulares, consulte [Elementos de linguagem das expressões regulares](https://go.microsoft.com/fwlink/?LinkId=164401) na Biblioteca MSDN.|  
|**É nulo**|Retorna valores de atributo que são nulos. O campo **Critérios** é desabilitado quando você seleciona o operador **É NULO** .|  
|**Não é nulo**|Retorna valores de atributo que não são nulos. O campo **Critérios** é desabilitado quando você seleciona o operador **Não é NULO** .|  
  
  
