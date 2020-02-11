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
ms.openlocfilehash: 5f43dbf75754a16b3163bbb8e268400f34d372b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087815"
---
# <a name="types-of-changes"></a>Tipos de alterações
Três tipos de alterações são feitas no ODBC *3. x* (e em qualquer versão do ODBC). Cada um deles afeta a compatibilidade com versões anteriores e é manipulado de forma diferente. Essas alterações são descritas na tabela a seguir.  
  
|Tipo de alteração|DESCRIÇÃO|  
|--------------------|-----------------|  
|Novos recursos|Esses são os recursos que são novos no ODBC *3. x*, como descritores ou associações fora de linha. Eles são implementados somente quando o aplicativo e o driver, bem como o Gerenciador de driver, são da versão *3. x*, portanto, não há nenhuma tentativa de torná-los compatíveis com versões anteriores.|  
|Recursos duplicados|Esses são os recursos que existem no ODBC *2. x* e no ODBC *3. x* , mas são implementados de maneiras diferentes em cada um. As funções **SQLAllocHandle** e **SQLAllocStmt** são um exemplo. Os problemas de compatibilidade com versões anteriores para esses e outros recursos duplicados são tratados principalmente por mapeamentos no Gerenciador de driver.|  
|Alterações de comportamento|Esses são recursos que são tratados de forma diferente no ODBC *2. x* e no ODBC *3. x*. Um **#define** DateTime é um exemplo. Esses recursos são tratados pelo driver ODBC *3. x* com base em uma configuração de atributo de ambiente. (Consulte [alterações comportamentais](../../../odbc/reference/develop-app/behavioral-changes.md) para obter mais informações.)|
