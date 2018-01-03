---
title: Identificadores de ambiente | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fa388a7724fdda836a9a82b3f00476ed0a4288bf
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="environment-handles"></a>Identificadores de ambiente
Um *ambiente* é um contexto global acessar dados; associado a um ambiente é qualquer informação que é global por natureza, tais como:  
  
-   Estado do ambiente  
  
-   Diagnóstico do nível do ambiente atual  
  
-   Os identificadores de conexões atualmente alocados no ambiente  
  
-   As configurações atuais de cada atributo de ambiente  
  
 Dentro de um trecho de código que implementa ODBC (o Gerenciador de Driver ou um driver), um identificador de ambiente identifica uma estrutura para conter essas informações.  
  
 Identificadores de ambiente não são usados com frequência em aplicativos ODBC. Eles são sempre usados em chamadas para **SQLDataSources** e **SQLDrivers** e às vezes é usado em chamadas para **SQLAllocHandle**, **SQLEndTran**, **SQLFreeHandle**, **SQLGetDiagField**, e **SQLGetDiagRec**.  
  
 Cada trecho de código que implementa ODBC (o Gerenciador de Driver ou um driver) contém um ou mais identificadores de ambiente. Por exemplo, o Gerenciador de Driver mantém um identificador de ambiente separado para cada aplicativo que está conectado a ele. Identificadores de ambiente são alocados com **SQLAllocHandle** e liberadas com **SQLFreeHandle**.
