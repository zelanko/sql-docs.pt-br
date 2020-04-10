---
title: MARS (Vários Conjuntos de Resultados Ativos)
description: Descreve como ter mais de um SqlDataReader aberto em uma conexão quando cada instância de SqlDataReader é iniciada a partir de um comando separado.
ms.date: 08/15/2019
ms.assetid: c90ef863-bac7-44cf-adc1-f05c36fcf57d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: e93493a28adfecd7dd39c79a86170b06ed18b992
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924286"
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
