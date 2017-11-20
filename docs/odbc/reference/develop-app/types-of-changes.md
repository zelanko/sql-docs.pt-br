---
title: "Tipos de alterações | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a494595625d264159fbb39db03818d50ed97876
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="types-of-changes"></a>Tipos de alterações
Três tipos de alterações são feitos em ODBC 3. *x* (e qualquer versão do ODBC). Cada um deles afeta compatibilidade com versões anteriores de forma diferente e é tratada de maneira diferente. Essas alterações são descritas na tabela a seguir.  
  
|Tipo de alteração|Description|  
|--------------------|-----------------|  
|Novos recursos|Esses são recursos que são novos para o ODBC 3. *x*, como associação fora de linha ou de descritores. Eles são implementados somente quando o aplicativo e o driver, bem como o Gerenciador de Driver são da versão 3*. x*, portanto, não há nenhuma tentativa para fazer essas compatível com versões anteriores.|  
|Recursos duplicados|Esses são recursos que existem no ODBC 2*. x* e o ODBC 3. *x* , mas são implementadas de maneiras diferentes em cada um. As funções **SQLAllocHandle** e **SQLAllocStmt** são um exemplo. Problemas de compatibilidade com versões anteriores para esses e outros recursos duplicados geralmente são manipulados pelo mapeamentos no Gerenciador de Driver.|  
|Alterações de comportamento|Estes são os recursos que são tratados de maneira diferente no ODBC 2*. x* e o ODBC 3. *x*. Uma data e hora **#define** é um exemplo. Esses recursos são manipulados pelo ODBC 3. *x* driver com base em uma configuração de atributo do ambiente. (Consulte [alterações de comportamento](../../../odbc/reference/develop-app/behavioral-changes.md) para obter mais informações.)|

