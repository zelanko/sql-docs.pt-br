---
title: Passar um parâmetro de relatório em uma URL | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], passing parameters
- passing parameters [Reporting Services]
ms.assetid: f93a94cc-27b5-435a-aa85-69e6ec6459ad
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 551fc19b3d39ef6cf12c5fdd4e77196b0abbb9fe
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65580834"
---
# <a name="pass-a-report-parameter-within-a-url"></a>Pass a Report Parameter Within a URL
  Você pode transmitir parâmetros de relatório a um relatório incluindo-os em uma URL de relatório. Esses parâmetros de URL não são prefixados, pois eles são transmitidos diretamente para o mecanismo de processamento de relatório.  

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.
  
> [!IMPORTANT]  
>  É importante que a URL inclua a sintaxe do proxy `_vti_bin` para rotear a solicitação através do SharePoint e do proxy HTTP [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . O proxy adiciona qualquer contexto à solicitação HTTP, o contexto necessário para garantir a execução adequada do relatório para servidores de relatório no modo do SharePoint.  
>   
>  Se você não incluir a sintaxe do proxy, precisará prefixar o parâmetro com *rp:* .  
  
 Todos os parâmetros de consulta podem ter parâmetros de relatório correspondentes. Você passa um parâmetro de consulta para um relatório, transmitindo o parâmetro de relatório correspondente. Para obter mais informações, consulte [Criar uma consulta no Designer de Consultas Relacionais &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md).  
  
> [!IMPORTANT]
>  Os parâmetros de relatório diferenciam maiúsculas de minúsculas.  
> 
> [!NOTE]
>  Os parâmetros de relatório diferenciam maiúsculas de minúsculas e utilizam os seguintes caracteres especiais:  
> 
>  -   Qualquer caractere de espaço na cadeia de caracteres da URL será substituído pelos caracteres "% 20", de acordo com os padrões de codificação de URL.  
> -   Um caractere de espaço na parte do parâmetro da URL será substituído por um sinal de adição (+).  
> -   Um ponto-e-vírgula em qualquer parte da cadeia de caracteres será substituído pelos caracteres "%3A."  
> -   Os navegadores devem executar a codificação de URL apropriada automaticamente. Não é preciso codificar os caracteres manualmente.  
  
 Para definir um parâmetro de relatório em uma URL, use a sintaxe a seguir:  
  
```  
  
parameter=value  
```  
  
 Por exemplo, para especificar dois parâmetros, "ReportMonth" e "ReportYear", definidos em um relatório, use a URL a seguir para um servidor de relatório de modo nativo:  
  
```  
https://myrshost/ReportServer?/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2&ReportMonth=3&ReportYear=2008  
```  
  
 Por exemplo, para especificar os mesmos dois parâmetros definidos em um relatório, use a URL de um servidor de relatório no modo integrado do SharePoint. Observe o `/_vti_bin`:  
  
```  
https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2.rdl&ReportMonth=3&ReportYear=2008  
```  
  
 Para transmitir um valor nulo para um parâmetro, use a sintaxe a seguir:  
  
```  
  
parameter  
:isnull=true  
  
```  
  
 Por exemplo,  
  
```  
SalesOrderNumber:isnull=true  
```  
  
 Para passar um valor **booliano** , use 0 para false ou 1 para true. Para passar um valor **flutuante** , inclua o separador decimal da localidade do servidor  
  
> [!NOTE]  
>  Se o seu relatório contiver um parâmetro que tenha um valor padrão e o valor da propriedade **Prompt** for **false** (isto é, a propriedade Avisar Usuário não for selecionada no Gerenciador de Relatórios), você não poderá transmitir um valor para esse parâmetro em uma URL. Isso fornece aos administradores a opção de impedir que usuários finais adicionem ou modifiquem os valores de determinados parâmetros de relatório.  
  
##  <a name="additional-examples"></a><a name="bkmk_examples"></a> Exemplos adicionais  
 O exemplo de URL a seguir inclui espaços e vários parâmetros  
  
-   O nome de pasta "Equipe de Instrução do Usuário do SQL Server" inclui espaços e, portanto, o sinal "+" substitui cada espaço.  
  
-   O nome de relatório "relatório do projeto de equipe" inclui espaços e, portanto, o sinal "+" substitui cada espaço.  
  
-   Passa dois parâmetros "teamgrouping2" com um valor "xgroup" e "teamgrouping1" com um valor "ygroup".  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup  
```  
  
 O exemplo de URL a seguir inclui um parâmetros com vários valores, "OrderID. O formato de um parâmetro com vários valores é repetir o nome do parâmetro para cada valor.  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup&OrderID=747&OrderID=787&OrderID=12  
```  
  
 O exemplo de URL a seguir passa um único parâmetro de *SellStartDate* com um valor "7/1/2005", para um servidor de relatório de modo nativo.  
  
```  
https://myserver/ReportServer/Pages/ReportViewer.aspx?%2fProduct_and_Sales_Report_AdventureWorks&SellStartDate=7/1/2005  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Acesso à URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referência de parâmetro de acesso de URL](../reporting-services/url-access-parameter-reference.md)  
  
  
