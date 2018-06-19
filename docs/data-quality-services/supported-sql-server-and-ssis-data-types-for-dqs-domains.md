---
title: Tipos de dados do SQL Server e do SSIS com suporte em domínios do DQS | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4931143a-b84d-478b-9b45-174128d36ed3
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e7e297690f6b2a6c14d4b280905a0fa888d0b4ed
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35311115"
---
# <a name="supported-sql-server-and-ssis-data-types-for-dqs-domains"></a>O SQL Server com suporte e tipos de dados do SSIS para domínios do DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

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
  
 O restante dos tipos de dados do SQL Server não tem suporte no DQS. Para obter informações sobre todos os tipos de dados do SQL Server, consulte [Tipos de dados &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md).  
  
##  <a name="SSIS"></a> Tipos de dados do SSIS com suporte  
 A tabela a seguir fornece informações sobre os tipos de dados do SSIS com suporte para cada tipo de dados de domínio do DQS:  
  
|Tipo de dados de domínio DQS|Tipo de dados do SSIS com suporte|  
|--------------------------|------------------------------|  
|data|DT_DATE|  
|Decimal|DT_DECIMAL<br /><br /> DT_NUMERIC<br /><br /> DT_R4<br /><br /> DT_R8|  
|Integer|DT_I1<br /><br /> DT_I2<br /><br /> DT_I4<br /><br /> DT_I8<br /><br /> DT_U1<br /><br /> DT_U2<br /><br /> DT_U4<br /><br /> DT_U8|  
|Cadeia de caracteres|DT_STR<br /><br /> DT_WSTR|  
  
 O restante dos tipos de dados do SSIS não tem suporte no DQS. Para obter informações sobre todos os tipos de dados do SSIS, consulte [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar um domínio](../data-quality-services/managing-a-domain.md)  
  
  
