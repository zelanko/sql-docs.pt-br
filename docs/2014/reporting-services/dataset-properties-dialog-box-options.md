---
title: Caixa de diálogo de propriedades do conjunto de dados, opções | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10130"
- sql12.rtp.rptdesigner.datasetproperties.options.f1
ms.assetid: 95299049-71ba-427f-b723-775cb696243f
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 81a50aa53c41ee0db4b6e9d97f2b96ca58e2649c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48228027"
---
# <a name="dataset-properties-dialog-box-options"></a>Caixa de diálogo Propriedades do Conjunto de Dados, Opções
  Selecione **opções** sobre o **DatasetProperties** caixa de diálogo para alterar as opções de dados, como as opções de agrupamento e subtotais, para a consulta. Para obter mais informações, consulte [Suporte a agrupamentos e Unicode](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="options"></a>Opções  
 **Agrupamento**  
 Selecione uma localidade que determina a sequência de agrupamento a ser usada para classificar os dados. **Padrão** indica que o servidor de relatórios deve tentar derivar o valor a partir do provedor de dados quando o relatório é executado. Se o valor não puder ser derivado, o valor padrão será derivado da configuração de localidade do computador.  
  
 **Diferenciação de maiúsculas e minúsculas**  
 Selecione um valor que determina a diferenciação de maiúsculas e minúsculas. Esta opção indica se os dados são maiúsculas e minúsculas. Você pode definir a **Distinção de maiúsculas e minúsculas** como **Verdadeiro**, **Falso**ou **Automático**. O valor padrão, **Auto**, indica que o servidor de relatório deve tentar obter o valor do provedor de dados quando o relatório é executado. Se o provedor de dados não der suporte ao tipo de diferenciação de maiúsculas e minúsculas, o relatório será executado como se o valor fosse **False**. Se souber o valor e souber que ele tem suporte, escolha **Verdadeiro**.  
  
 **Distinção de acentos**  
 Selecione um valor que determina a sensibilidade de acentuação. A**Sensibilidade de acentuação** indica se os dados são sensíveis à acentuação e podem ser definidos para **Verdadeiro**, **Falso**ou **Automático**. O valor padrão, **Auto**, indica que o servidor de relatório deve tentar obter o valor do provedor de dados quando o relatório é executado. Se o provedor de dados não der suporte o tipo de sensibilidade de acentuação, o relatório executará como se o valor fosse **Falso**. Se souber o valor e souber que ele tem suporte, escolha **Verdadeiro**.  
  
 **Sensibilidade de Kanatype**  
 Selecione um valor que determina sensibilidade de kanatype. Esta opção indica se os dados são sensíveis ao kanatype; pode ser definido como **Verdadeiro**, **Falso**ou **Automático**. O valor padrão, **Auto**, indica que o servidor de relatório deve tentar obter o valor do provedor de dados quando o relatório é executado. Se o provedor de dados não der suporte ao tipo de sensibilidade de kanatype, o relatório executará como se o valor fosse **Falso**. Se souber o valor e souber que ele tem suporte, escolha **Verdadeiro**.  
  
 **Distinção de largura**  
 Selecione um valor que determina distinção de largura. Esta opção indica se os dados são sensíveis à largura e pode ser definida como **True**, **False**ou **Auto**. O valor padrão, **Auto**, indica que o servidor de relatório deve tentar obter o valor do provedor de dados quando o relatório é executado. Se o provedor de dados não der suporte ao tipo de distinção de largura, o relatório executará como se o valor fosse **Falso**. Se souber o valor e souber que ele tem suporte, escolha **Verdadeiro**.  
  
 **Interprete subtotais como linhas de detalhe**  
 Selecione um valor que indica se deseja que linhas de subtotais sejam interpretadas como linhas de detalhes ao invés de linhas de agregação. O valor padrão, **automática**, indica que as linhas de subtotais devem ser tratadas como linhas de detalhes se o relatório não usar o `Aggregate`função () para acessar os campos no conjunto de dados. Se quiser que as linhas de subtotais sejam interpretadas como linhas de agregação, selecione **Falso**. Se você deseja que as linhas de subtotais sejam interpretadas como linhas de detalhes e você souber que elas não usam o `Aggregate`() de função, escolha **verdadeiro**.  
  
## <a name="see-also"></a>Consulte também  
 [Definir a localidade em um relatório ou caixa de texto &#40;Reporting Services&#41;](report-design/set-the-locale-for-a-report-or-text-box-reporting-services.md)   
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Nome de agrupamento do Windows &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql)   
 [Nome de agrupamento do SQL Server &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)   
 [Função de agregação &#40;relatórios e SSRS&#41;](report-design/report-builder-functions-aggregate-function.md)  
  
  
