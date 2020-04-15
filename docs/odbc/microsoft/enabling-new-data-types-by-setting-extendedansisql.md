---
title: Habilitando novos tipos de dados definindo ExtendedAnsiSQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b703c5c14c4743e13feee139d16e5dfeb3c24c63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303407"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>Habilitar novos tipos de dados configurar ExtendedAnsiSQL
Dois novos tipos de dados estão disponíveis nas bases de dados do Jet 4.0 quando a bandeira ExtendedAnsiSQL é ligada: SQL_DECIMAL e SQL_NUMERIC. A precisão e a escala padrão são 18 e 0, respectivamente. Os dados acessados via ODBC que são digitados como SQL_DECIMAL ou SQL_NUMERIC serão mapeados para o Microsoft Jet Decimal em vez de Moeda.  
  
 Quando o sinalizador ExtendedAnsiSQL é desligado, você não pode criar tabelas com tipos decimais ou numéricos, e esses tipos não aparecerão no SQLGetTypeInfo(). No entanto, se a tabela contiver os novos tipos de dados, eles podem ser usados com os tipos de dados corretos.
