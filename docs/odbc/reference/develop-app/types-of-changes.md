---
title: Tipos de alterações | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac92c6d40ea9ead6b8875e3338bb740b4bdf8523
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63473178"
---
# <a name="types-of-changes"></a>Tipos de alterações
Três tipos de alterações são feitos em ODBC 3. *x* (e qualquer versão do ODBC). Cada uma dessas afeta a compatibilidade com versões anteriores de maneira diferente e é tratada de maneira diferente. Essas alterações são descritas na tabela a seguir.  
  
|Tipo de alteração|Descrição|  
|--------------------|-----------------|  
|Novos recursos|Esses são recursos que são novos no ODBC 3. *x*, como associação fora de linha ou descritores. Eles são implementados somente quando o aplicativo e driver, bem como o Gerenciador de Driver são da versão 3 *. x*, portanto, não há nenhuma tentativa de fazer essas compatível com versões anteriores.|  
|Recursos duplicados|Esses são recursos que existem no ODBC 2 *. x* e o ODBC 3. *x* , mas são implementados de maneiras diferentes em cada um. As funções **SQLAllocHandle** e **SQLAllocStmt** são um exemplo. Problemas de compatibilidade com versões anteriores para esses e outros recursos duplicados principalmente são manipulados pelos mapeamentos no Gerenciador de Driver.|  
|Alterações de comportamento|Esses são recursos que são manipulados de forma diferente de ODBC 2 *. x* e o ODBC 3. *x*. Uma data e hora **#define** é um exemplo. Esses recursos são manipulados pelo ODBC 3. *x* driver com base em uma configuração de atributo do ambiente. (Consulte [alterações de comportamento](../../../odbc/reference/develop-app/behavioral-changes.md) para obter mais informações.)|
