---
title: O que&#39;novo no CLR Integration | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 45e4f0578d06eeafc545bea2b6374a37b8ef7cbc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874062"
---
# <a name="what39s-new-in-clr-integration"></a>O que&#39;s novos na integração CLR
  Estes são os novos recursos da integração CLR no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]:  
  
-   Na versão 4 do CLR, os objetos de banco de dados CLR não capturam mais exceções de estado corrompidas. Agora, essas exceções são capturadas na camada de hospedagem da integração CLR. Essas exceções ainda podem ser capturadas pelos componentes do banco de dados CLR definindo um atributo de código ([\<legacyCorruptedStateExceptionsPolicy > elemento](https://go.microsoft.com/fwlink/?LinkId=204954)). No entanto, isso não é recomendado porque os resultados não são confiáveis quando ocorre uma exceção de estado corrompida.  
  
-   Devido aos rigorosos requisitos de segurança do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], os componentes do banco de dados CLR continuarão usando o modelo de segurança de acesso do código definido no CLR versão 2.0.  
  
-   No CLR versão 4, um erro de formato em um valor `System.TimeSpan` gerará um `System.FormatExceptions`. Antes da versão 4 do CLR, um erro de formato em um valor `System.TimeSpan` era ignorado. Aplicativos de banco de dados que se baseiam no comportamento anterior à versão 4 do CLR deverão ser executados com um nível de compatibilidade de banco de dados (`ALTER DATABASE Compatibility Level`) igual a 100 ou inferior. Para obter mais informações, consulte [< TimeSpan_LegacyFormatMode > elemento](https://go.microsoft.com/fwlink/?LinkId=205109).  
  
-   A versão 4 do CLR oferece suporte ao Unicode 5.1. As operações de classificação que envolvem acentos e símbolos serão aprimoradas. Talvez ocorram problemas de compatibilidade se o seu aplicativo se basear no comportamento de classificação herdado. Para habilitar a classificação herdada, o nível de compatibilidade de banco de dados (`ALTER DATABASE Compatibility Level`) deve ser definido como 100 ou inferior. Para oferecer suporte a essa condição, o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] instalará o arquivo sort00001000.dll no diretório do .NET Framework 4 (C:\Windows\Microsoft.NET\Framework\v4.0.30319). Para obter mais informações, consulte [ \<CompatSortNLSVersion > elemento](https://go.microsoft.com/fwlink/?LinkId=205110).  
  
-   As colunas a seguir foram adicionadas ao [DM clr_appdomains](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql): `total_processor_time_ms`, `total_allocated_memory_kb`, e `survived_memory_kb`.  
  
  
