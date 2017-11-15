---
title: "Tipos de dados do SQL Server e do SSIS com suporte em domínios do DQS | Microsoft Docs"
ms.custom: 
ms.date: 11/08/2011
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4931143a-b84d-478b-9b45-174128d36ed3
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 74842335306dd35539a3ff0193f6daba3aadef49
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="supported-sql-server-and-ssis-data-types-for-dqs-domains"></a>O SQL Server com suporte e tipos de dados do SSIS para domínios do DQS
  Há muitos tipos de dados no SQL Server e no SSIS (SQL Server Integration Services), mas somente quatro tipos de dados para domínios do DQS: Data, Decimal, Inteiro e Cadeia de Caracteres. Nem todos os SQL Server e tipos de dados do SSIS têm suporte no DQS. Você poderá mapear sua fonte de dados para um domínio DQS para realizar atividades de qualidade de dados somente se o tipo de dados de origem tiver suporte no DQS e corresponder ao tipo de dados de domínio do DQS. Este tópico fornece informações sobre os tipos de dados do SQL Server e do SSIS que têm suporte e estão disponíveis para mapear para cada um dos quatro tipos de dados de domínio no DQS.  
  
> [!NOTE]  
>  Nos arquivos .xlsx e .xls, o tipo de dados da coluna de origem é determinado pelo tipo de dados mais frequente nas oito primeiras linhas. Se uma célula para não estiver em conformidade com esse tipo de dados, ela receberá um valor nulo. De modo semelhante, em arquivos .csv, o tipo de dados da coluna de origem é determinado pelo tipo de dados mais frequente nas oito primeiras linhas.  
  
##  <a name="SQLServer"></a> Tipos de dados do SQL Server com suporte  
 A tabela a seguir fornece informações sobre os tipos de dados de SQL Server com suporte para cada tipo de dados de domínio do DQS:  
  
|Tipo de dados de domínio DQS|Tipo de dados do SQL Server com suporte|  
|--------------------------|------------------------------------|  
|Data|Data|  
|Decimal|Decimal<br /><br /> float<br /><br /> money<br /><br /> numeric<br /><br /> real<br /><br /> smallmoney|  
|Integer|bigint<br /><br /> int<br /><br /> smallint<br /><br /> tinyint|  
|Cadeia de caracteres|char<br /><br /> nchar<br /><br /> nvarchar<br /><br /> varchar|  
  
 O restante dos tipos de dados do SQL Server não tem suporte no DQS. Para obter informações sobre todos os tipos de dados do SQL Server, consulte [Tipos de dados &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md).  
  
##  <a name="SSIS"></a> Tipos de dados do SSIS com suporte  
 A tabela a seguir fornece informações sobre os tipos de dados do SSIS com suporte para cada tipo de dados de domínio do DQS:  
  
|Tipo de dados de domínio DQS|Tipo de dados do SSIS com suporte|  
|--------------------------|------------------------------|  
|Data|DT_DATE|  
|Decimal|DT_DECIMAL<br /><br /> DT_NUMERIC<br /><br /> DT_R4<br /><br /> DT_R8|  
|Integer|DT_I1<br /><br /> DT_I2<br /><br /> DT_I4<br /><br /> DT_I8<br /><br /> DT_U1<br /><br /> DT_U2<br /><br /> DT_U4<br /><br /> DT_U8|  
|Cadeia de caracteres|DT_STR<br /><br /> DT_WSTR|  
  
 O restante dos tipos de dados do SSIS não tem suporte no DQS. Para obter informações sobre todos os tipos de dados do SSIS, consulte [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar um domínio](../data-quality-services/managing-a-domain.md)  
  
  
