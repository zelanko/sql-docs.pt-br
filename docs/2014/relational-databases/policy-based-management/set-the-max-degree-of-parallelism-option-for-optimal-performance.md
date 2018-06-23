---
title: Definir o grau máximo da opção de paralelismo para obter o desempenho ideal | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3fc4f4c3da6505d3c9464144a37eb98682969d9d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116366"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>Definir o grau máximo da opção de paralelismo para obtenção do desempenho ideal
  Esta regra determina se a opção grau máximo de paralelismo (MAXDOP) pode obter um valor maior que 8. A configuração desta opção com um valor maior frequentemente causa o consumo indesejável de recursos e a degradação do desempenho.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Defina a opção grau máximo de paralelismo como 8 ou menos usando sp_configure.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Artigo 329204 da Base de Dados de Conhecimento Microsoft](http://go.microsoft.com/fwlink/?linkid=117786)  
  
 [Configurar a opção de configuração de servidor max degree of parallelism](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
