---
title: Habilitando novos tipos de dados Configurando ExtendedAnsiSQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 88f11adcab09dbe6964bfd67a944912fc185bccb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031123"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>Habilitar novos tipos de dados configurar ExtendedAnsiSQL
Dois novos tipos de dados estão disponíveis em bancos de dados Jet 4.0 quando o sinalizador ExtendedAnsiSQL está ativado: SQL_DECIMAL e SQL_NUMERIC. A precisão e escala padrão são 18 e 0, respectivamente. Os dados acessados por meio de ODBC que é digitada como SQL_DECIMAL ou SQL_NUMERIC serão mapeados para Microsoft Jet Decimal em vez de moeda.  
  
 Quando o sinalizador ExtendedAnsiSQL for desativado, é possível criar tabelas com tipos decimais ou numéricos, e esses tipos não aparecerão no SQLGetTypeInfo(). No entanto, se a tabela contém os novos tipos de dados, eles podem ser usados com os tipos de dados correto.
