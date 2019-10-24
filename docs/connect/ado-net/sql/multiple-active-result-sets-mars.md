---
title: MARS (Vários Conjuntos de Resultados Ativos)
description: Descreve como ter mais de um SqlDataReader aberto em uma conexão quando cada instância do SqlDataReader é iniciada a partir de um comando separado.
ms.date: 08/15/2019
ms.assetid: c90ef863-bac7-44cf-adc1-f05c36fcf57d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 7097dc3717966d441cd669ddccd189c2510211aa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452139"
---
# <a name="multiple-active-result-sets-mars"></a>MARS (Vários Conjuntos de Resultados Ativos)

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

MARS (vários conjuntos de resultados ativos) é um recurso que permite a execução de vários lotes em uma única conexão. Em versões anteriores, apenas um lote poderia ser executado por vez em uma única conexão. A execução de vários lotes com MARS não implica a execução simultânea de operações.  
  
## <a name="in-this-section"></a>Nesta seção  
[Habilitando conjuntos de resultados ativos múltiplos](enable-multiple-active-result-sets.md)  
Discute como usar o MARS com o SQL Server.  
  
[Manipulando dados](manipulate-data.md)  
Fornece exemplos de aplicativos de codificação MARS.  
  
## <a name="related-sections"></a>Seções relacionadas  
[Operações assíncronas](asynchronous-operations.md)  
Fornece detalhes sobre como usar os novos recursos assíncronos no .NET.  
  
## <a name="next-steps"></a>Próximas etapas
- [SQL Server e ADO.NET](index.md)
