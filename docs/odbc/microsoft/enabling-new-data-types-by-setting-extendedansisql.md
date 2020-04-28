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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303407"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>Habilitar novos tipos de dados configurar ExtendedAnsiSQL
Dois novos tipos de dados estão disponíveis em bancos de dado Jet 4,0 quando o sinalizador ExtendedAnsiSQL está ativado: SQL_DECIMAL e SQL_NUMERIC. A precisão e a escala padrão são 18 e 0, respectivamente. Os dados acessados via ODBC que são digitados como SQL_DECIMAL ou SQL_NUMERIC serão mapeados para o Microsoft Jet decimal em vez de moeda.  
  
 Quando o sinalizador ExtendedAnsiSQL está desativado, não é possível criar tabelas com tipos decimais ou numéricos, e esses tipos não aparecerão em SQLGetTypeInfo (). No entanto, se a tabela contiver os novos tipos de dados, eles poderão ser usados com os tipos de dados corretos.
