---
title: Tipos de dados do SQL Server e do SSIS com suporte em domínios do DQS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
ms.assetid: 4931143a-b84d-478b-9b45-174128d36ed3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a3fb96c10c017a1505f0a6e0036de346040cfec0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48195756"
---
# <a name="supported-sql-server-and-ssis-data-types-for-dqs-domains"></a>O SQL Server com suporte e tipos de dados do SSIS para domínios do DQS
  Há muitos tipos de dados no SQL Server e no SSIS (SQL Server Integration Services), mas somente quatro tipos de dados para domínios do DQS: Data, Decimal, Inteiro e Cadeia de Caracteres. Nem todos os SQL Server e tipos de dados do SSIS têm suporte no DQS. Você poderá mapear sua fonte de dados para um domínio DQS para realizar atividades de qualidade de dados somente se o tipo de dados de origem tiver suporte no DQS e corresponder ao tipo de dados de domínio do DQS. Este tópico fornece informações sobre os tipos de dados do SQL Server e do SSIS que têm suporte e estão disponíveis para mapear para cada um dos quatro tipos de dados de domínio no DQS.  
  
> [!NOTE]  
>  Nos arquivos .xlsx e .xls, o tipo de dados da coluna de origem é determinado pelo tipo de dados mais frequente nas oito primeiras linhas. Se uma célula para não estiver em conformidade com esse tipo de dados, ela receberá um valor nulo. De modo semelhante, em arquivos .csv, o tipo de dados da coluna de origem é determinado pelo tipo de dados mais frequente nas oito primeiras linhas.  
  
##  <a name="SQLServer"></a> Tipos de dados do SQL Server com suporte  
 A tabela a seguir fornece informações sobre os tipos de dados de SQL Server com suporte para cada tipo de dados de domínio do DQS:  
  
|Tipo de dados de domínio DQS|Tipo de dados do SQL Server com suporte|  
|--------------------------|------------------------------------|  
|data|Data|  
|Decimal|Decimal<br /><br /> FLOAT<br /><br /> money<br /><br /> NUMERIC<br /><br /> REAL<br /><br /> SMALLMONEY|  
|Integer|BIGINT<br /><br /> INT<br /><br /> smallint<br /><br /> TINYINT|  
|Cadeia de caracteres|char<br /><br /> NCHAR<br /><br /> NVARCHAR<br /><br /> varchar|  
  
 O restante dos tipos de dados do SQL Server não tem suporte no DQS. Para obter informações sobre todos os tipos de dados do SQL Server, consulte [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).  
  
##  <a name="SSIS"></a> Tipos de dados do SSIS com suporte  
 A tabela a seguir fornece informações sobre os tipos de dados do SSIS com suporte para cada tipo de dados de domínio do DQS:  
  
|Tipo de dados de domínio DQS|Tipo de dados do SSIS com suporte|  
|--------------------------|------------------------------|  
|data|DT_DATE|  
|Decimal|DT_DECIMAL<br /><br /> DT_NUMERIC<br /><br /> DT_R4<br /><br /> DT_R8|  
|Integer|DT_I1<br /><br /> DT_I2<br /><br /> DT_I4<br /><br /> DT_I8<br /><br /> DT_U1<br /><br /> DT_U2<br /><br /> DT_U4<br /><br /> DT_U8|  
|Cadeia de caracteres|DT_STR<br /><br /> DT_WSTR|  
  
 O restante dos tipos de dados do SSIS não tem suporte no DQS. Para obter informações sobre todos os tipos de dados do SSIS, consulte [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar um domínio](../../2014/data-quality-services/managing-a-domain.md)  
  
  
