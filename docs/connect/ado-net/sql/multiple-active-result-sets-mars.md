---
title: MARS (Vários Conjuntos de Resultados Ativos)
description: Descreve como ter mais de um SqlDataReader aberto em uma conexão quando cada instância de SqlDataReader é iniciada a partir de um comando separado.
ms.date: 08/15/2019
ms.assetid: c90ef863-bac7-44cf-adc1-f05c36fcf57d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 4475e4b8a71b4abcf4e1c2324a49e03a8bb64fbb
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896678"
---
# <a name="multiple-active-result-sets-mars"></a>MARS (Vários Conjuntos de Resultados Ativos)

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

MARS (Conjuntos de resultados ativos múltiplos) é um recurso que permite a execução de vários lotes em uma única conexão. Em versões anteriores, só era possível executar um lote por vez em uma única conexão. Executar vários lotes com o MARS não implica na execução simultânea de operações.  
  
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
