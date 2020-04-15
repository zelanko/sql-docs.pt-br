---
title: Tipos de Mudanças | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f44adb59aa9b0f25475a76a97fe3670de0228c08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301601"
---
# <a name="types-of-changes"></a>Tipos de alterações
Três tipos de alterações são feitas no ODBC *3.x* (e em qualquer versão do ODBC). Cada um deles afeta a compatibilidade retrógrada de forma diferente e é tratado de uma maneira diferente. Essas alterações estão descritas na tabela a seguir.  
  
|Tipo de mudança|Descrição|  
|--------------------|-----------------|  
|Novos recursos|Estes são recursos que são novos para o ODBC *3.x,* como vinculação ou descritores fora de linha. Estes são implementados somente quando o aplicativo e o driver, bem como o Driver Manager, são da versão *3.x,* portanto não há nenhuma tentativa de torná-los compatíveis com o retrocesso.|  
|Recursos duplicados|Estes são recursos que existem no ODBC *2.x* e ODBC *3.x,* mas são implementados de maneiras diferentes em cada um. As funções **SQLAllocHandle** e **SQLAllocStmt** são um exemplo. Problemas de compatibilidade retrógrada para esses e outros recursos duplicados são manipulados principalmente por mapeamentos no Driver Manager.|  
|Alterações de comportamento|Estes são recursos que são tratados de forma diferente em ODBC *2.x* e ODBC *3.x*. Um **#define** datado é um exemplo. Esses recursos são manipulados pelo driver ODBC *3.x* com base na configuração de atributos do ambiente. (Consulte [Mudanças comportamentais](../../../odbc/reference/develop-app/behavioral-changes.md) para obter mais informações.)|
