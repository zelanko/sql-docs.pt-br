---
title: Caixa de diálogo Propriedades do conjunto de, opções | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10130"
- sql12.rtp.rptdesigner.datasetproperties.options.f1
ms.assetid: 95299049-71ba-427f-b723-775cb696243f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 778365e8fc7f40700b0f8c1683260f15c860a32a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109407"
---
# <a name="dataset-properties-dialog-box-options"></a>Caixa de diálogo Propriedades do Conjunto de Dados, Opções
  Selecione **Opções** na caixa de diálogo **datasetproperties** para alterar as opções de dados, como opções de agrupamento e subtotais, para a consulta. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="options"></a>Opções  
 **Ordenação**  
 Selecione uma localidade que determina a sequência de ordenação a ser usada para classificar os dados. **Padrão** indica que o servidor de relatórios deve tentar derivar o valor a partir do provedor de dados quando o relatório é executado. Se o valor não puder ser derivado, o valor padrão será derivado da configuração de localidade do computador.  
  
 **Diferencia maiúsculas de minúsculas**  
 Selecione um valor que determina a diferenciação de maiúsculas e minúsculas. Esta opção indica se os dados são maiúsculas e minúsculas. Você pode definir a **diferenciação de maiúsculas e minúsculas** como **true**, **false**ou **auto**. O valor padrão, **auto**, indica que o servidor de relatório deve tentar derivar o valor do provedor de dados quando o relatório é executado. Se o provedor de dados não der suporte ao tipo de diferenciação de maiúsculas e minúsculas, o relatório será executado como se o valor fosse **False**. Se souber o valor e souber que ele tem suporte, escolha **Verdadeiro**.  
  
 **Distinção de acentos**  
 Selecione um valor que determina a sensibilidade de acentuação. A **sensibilidade de acentos** indica se os dados diferenciam acentos e podem ser definidos como **true**, **false**ou **auto**. O valor padrão, **auto**, indica que o servidor de relatório deve tentar derivar o valor do provedor de dados quando o relatório é executado. Se o provedor de dados não der suporte o tipo de sensibilidade de acentuação, o relatório executará como se o valor fosse **Falso**. Se souber o valor e souber que ele tem suporte, escolha **Verdadeiro**.  
  
 **Sensibilidade de Kanatype**  
 Selecione um valor que determina sensibilidade de kanatype. Esta opção indica se os dados diferenciam caracteres kana; Ele pode ser definido como **true**, **false**ou **auto**. O valor padrão, **auto**, indica que o servidor de relatório deve tentar derivar o valor do provedor de dados quando o relatório é executado. Se o provedor de dados não der suporte ao tipo de sensibilidade de kanatype, o relatório executará como se o valor fosse **Falso**. Se souber o valor e souber que ele tem suporte, escolha **Verdadeiro**.  
  
 **Distinção de largura**  
 Selecione um valor que determina distinção de largura. Essa opção indica se os dados têm distinção de largura e podem ser definidos como **true**, **false**ou **auto**. O valor padrão, **auto**, indica que o servidor de relatório deve tentar derivar o valor do provedor de dados quando o relatório é executado. Se o provedor de dados não der suporte ao tipo de distinção de largura, o relatório executará como se o valor fosse **Falso**. Se souber o valor e souber que ele tem suporte, escolha **Verdadeiro**.  
  
 **Interprete subtotais como linhas de detalhe**  
 Selecione um valor que indica se deseja que linhas de subtotais sejam interpretadas como linhas de detalhes ao invés de linhas de agregação. O valor padrão, **auto**, indica que as linhas de subtotal devem ser tratadas como linhas de detalhes se o relatório `Aggregate`não usar a função () para acessar os campos no conjunto de dados. Se quiser que as linhas de subtotais sejam interpretadas como linhas de agregação, selecione **Falso**. Se você quiser que as linhas de subtotal sejam interpretadas como linhas de detalhes e souber que elas `Aggregate`não usam a função (), escolha **true**.  
  
## <a name="see-also"></a>Consulte Também  
 [Definir a localidade de um relatório ou caixa de texto &#40;Reporting Services&#41;](report-design/set-the-locale-for-a-report-or-text-box-reporting-services.md)   
 [Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Nome de ordenação do Windows &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql)   
 [Nome de ordenação do SQL Server &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)   
 [Função de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-design/report-builder-functions-aggregate-function.md)  
  
  
