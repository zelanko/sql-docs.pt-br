---
title: O que há de novo na Integração CLR | Microsoft Docs
description: O Microsoft SQL Server que hospeda clr é chamado de integração CLR. Este artigo descreve novos recursos na integração CLR no SQL Server 2012.
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: clr
ms.topic: conceptual
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
ms.openlocfilehash: d27bf0d925d3a98dda488fb85aff7446434cc8ad
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488083"
---
# <a name="clr-integration---what39s-new"></a>Integração CLR - O que&#39;é novidade
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Estes são os novos recursos da integração CLR no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]:  
  
-   Na versão 4 do CLR, os objetos de banco de dados CLR não capturam mais exceções de estado corrompidas. Agora, essas exceções são capturadas na camada de hospedagem da integração CLR. Essas exceções ainda podem ser capturadas pelos componentes do banco de dados CLR definindo um atributo de código[\<(legacyCorruptedStateExceptionsPolicy> Element](https://go.microsoft.com/fwlink/?LinkId=204954)). No entanto, isso não é recomendado porque os resultados não são confiáveis quando ocorre uma exceção de estado corrompida.  
  
-   Devido aos rigorosos requisitos de segurança do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], os componentes do banco de dados CLR continuarão usando o modelo de segurança de acesso do código definido no CLR versão 2.0.  
  
-   Na versão 4 do CLR, um erro de formato em um valor **System.TimeSpan** gerará um **System.FormatExceptions**. Antes da versão 4 do CLR, um erro de formato em um valor **do System.TimeSpan** foi ignorado. Os aplicativos de banco de dados que dependem do comportamento antes da versão 4 do CLR devem ser executados com um nível de compatibilidade de banco de dados **(ALTER DATABASE Compatibility Level)** de 100 ou mais. Para obter mais informações, consulte [<TimeSpan_LegacyFormatMode> Element](https://go.microsoft.com/fwlink/?LinkId=205109).  
  
-   A versão 4 do CLR oferece suporte ao Unicode 5.1. As operações de classificação que envolvem acentos e símbolos serão aprimoradas. Talvez ocorram problemas de compatibilidade se o seu aplicativo se basear no comportamento de classificação herdado. Para habilitar a classificação legado, o nível de compatibilidade do banco de dados **(ALTER DATABASE Compatibility Level)** deve ser definido como 100 ou menos. Para oferecer suporte a essa condição, o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instalará o arquivo sort00001000.dll no diretório do .NET Framework 4 (C:\Windows\Microsoft.NET\Framework\v4.0.30319). Para obter mais informações, consulte [ \<CompatSortNLSVersion> Element](https://go.microsoft.com/fwlink/?LinkId=205110).  
  
-   As seguintes colunas foram adicionadas ao [sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md): **total_processor_time_ms**, **total_allocated_memory_kb**e **survived_memory_kb**.  
  
  
