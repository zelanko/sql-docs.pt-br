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
ms.openlocfilehash: 6aada496465c642570f9b60a0b1659bbe9ee3db6
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890896"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>Definir o grau máximo da opção de paralelismo para obtenção do desempenho ideal
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regra determina se a opção grau máximo de paralelismo (MAXDOP) pode obter um valor maior que 8. A configuração desta opção com um valor maior frequentemente causa o consumo indesejável de recursos e a degradação do desempenho.  
  
## <a name="best-practice-recommendations"></a>Recomendações de melhores práticas  
 A opção de configuração de MAXDOP (grau máximo de paralelismo) controla o número de processadores usados para a execução de uma consulta em um plano paralelo. Essa opção determina o número de threads usados para os operadores do plano de consulta que realizam o trabalho em paralelo. Dependendo se o SQL Server foi configurado em um computador SMP (multiprocessamento simétrico), um computador NUMA (acesso de memória não uniforme) ou em processadores habilitados para hyperthreading, você precisará configurar a opção de grau máximo de paralelismo adequadamente. 
 
 As recomendações para configurar o MAXDOP dependem da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo usada. Para obter diretrizes específicas da versão, confira [Configurar a Opção de Configuração do Servidor de grau máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines) e configure a política para verificar o valor do grau máximo de paralelismo devidamente.     
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Recomendações e diretrizes da opção de configuração do grau máximo de paralelismo no SQL Server](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)    
 [Configurar a Opção de Configuração do Servidor de grau máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)     
