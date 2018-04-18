---
title: O que&#39;novo no integração CLR | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
caps.latest.revision: 7
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2215d703e3284d0216693d7abb94a4fc11f2225f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="clr-integration---what39s-new"></a>Integração do CLR - o que&#39;novidades
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Estes são os novos recursos da integração CLR no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]:  
  
-   Na versão 4 do CLR, os objetos de banco de dados CLR não capturam mais exceções de estado corrompidas. Agora, essas exceções são capturadas na camada de hospedagem da integração CLR. Essas exceções ainda podem ser capturadas pelos componentes do banco de dados CLR definindo um atributo de código ([\<legacyCorruptedStateExceptionsPolicy > elemento](http://go.microsoft.com/fwlink/?LinkId=204954)). No entanto, isso não é recomendado porque os resultados não são confiáveis quando ocorre uma exceção de estado corrompida.  
  
-   Devido aos rigorosos requisitos de segurança do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], os componentes do banco de dados CLR continuarão usando o modelo de segurança de acesso do código definido no CLR versão 2.0.  
  
-   No CLR versão 4, um erro de formato em um **System. TimeSpan** valor irá gerar um **System.FormatExceptions**. Antes da versão 4 do CLR, um erro de formato em um **System. TimeSpan** valor foi ignorado. Aplicativos de banco de dados que dependem do comportamento anterior à versão 4 do CLR devem ser executado com um nível de compatibilidade do banco de dados (**nível de compatibilidade do banco de dados ALTER**) de 100 ou inferior. Para obter mais informações, consulte [< TimeSpan_LegacyFormatMode > elemento](http://go.microsoft.com/fwlink/?LinkId=205109).  
  
-   A versão 4 do CLR oferece suporte ao Unicode 5.1. As operações de classificação que envolvem acentos e símbolos serão aprimoradas. Talvez ocorram problemas de compatibilidade se o seu aplicativo se basear no comportamento de classificação herdado. Para habilitar a classificação herdada, o nível de compatibilidade do banco de dados (**nível de compatibilidade do banco de dados ALTER**) deve ser definido como 100 ou inferior. Para oferecer suporte a essa condição, o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instalará o arquivo sort00001000.dll no diretório do .NET Framework 4 (C:\Windows\Microsoft.NET\Framework\v4.0.30319). Para obter mais informações, consulte [ \<CompatSortNLSVersion > elemento](http://go.microsoft.com/fwlink/?LinkId=205110).  
  
-   As colunas a seguir foram adicionadas ao [sys.DM clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md): **total_processor_time_ms**, **total_allocated_memory_kb**, e **survived_ memory_kb**.  
  
  
