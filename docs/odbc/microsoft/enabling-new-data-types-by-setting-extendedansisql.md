---
title: Habilitar novos tipos de dados, definindo ExtendedAnsiSQL | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9eeff1a55315b30ab0d2cafa92f0aa4a511f9ab9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>Habilitar novos tipos de dados, definindo ExtendedAnsiSQL
Dois novos tipos de dados estão disponíveis em bancos de dados Jet 4.0 quando o sinalizador ExtendedAnsiSQL está ativado: SQL_DECIMAL e SQL_NUMERIC. A precisão e escala padrão são 18 e 0, respectivamente. Dados acessados por meio de ODBC que é digitado como SQL_DECIMAL ou SQL_NUMERIC serão mapeados para o Microsoft Jet Decimal em vez de moeda.  
  
 Quando o sinalizador ExtendedAnsiSQL estiver desativado, você não pode criar tabelas com tipos decimais ou numéricos e esses tipos não aparecerão no SQLGetTypeInfo(). No entanto, se a tabela contém os novos tipos de dados, eles podem ser usados com os tipos de dados correto.
