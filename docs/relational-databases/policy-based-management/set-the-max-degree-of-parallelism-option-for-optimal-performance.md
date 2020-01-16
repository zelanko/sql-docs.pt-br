---
title: Grau máximo de paralelismo e gerenciamento baseado em políticas
description: Descreve como configurar uma política para verificar o valor do grau máximo de paralelismo para o gerenciamento baseado em políticas do SQL Server.
ms.custom: seo-lt-2019
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c5f261998588fa15074a25c606a0aa50f742f04a
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557815"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>Definir o grau máximo da opção de paralelismo para obtenção do desempenho ideal
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regra determina se a opção grau máximo de paralelismo (MAXDOP) pode obter um valor maior que 8. A configuração desta opção com um valor maior frequentemente causa o consumo indesejável de recursos e a degradação do desempenho.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Defina a opção grau máximo de paralelismo como 8 ou menos usando sp_configure.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Recomendações e diretrizes para a opção de configuração max degree of parallelism do SQL Server](https://go.microsoft.com/fwlink/?linkid=117786)  
  
 [Configurar a opção de configuração de servidor max degree of parallelism](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
