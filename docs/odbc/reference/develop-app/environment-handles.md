---
title: Identificadores de ambiente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 409b2c14282238766457d349287f65d90fe463b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114318"
---
# <a name="environment-handles"></a>Identificadores de ambiente
Uma *ambiente* é um contexto global no qual acessar dados; associado a um ambiente é qualquer informação que é global por natureza, tais como:  
  
-   Estado do ambiente  
  
-   O diagnóstico de nível do ambiente atual  
  
-   Os identificadores de conexões atualmente alocados no ambiente  
  
-   As configurações atuais de cada atributo de ambiente  
  
 Dentro de um trecho de código que implementa o ODBC (o Gerenciador de Driver ou um driver), um identificador de ambiente identifica uma estrutura para conter essas informações.  
  
 Identificadores de ambiente não são frequentemente usadas em aplicativos ODBC. Eles são sempre usados em chamadas para **SQLDataSources** e **SQLDrivers** e, às vezes, é usado em chamadas para **SQLAllocHandle**, **SQLEndTran**, **SQLFreeHandle**, **SQLGetDiagField**, e **SQLGetDiagRec**.  
  
 Cada parte do código que implementa o ODBC (o Gerenciador de Driver ou um driver) contém um ou mais identificadores de ambiente. Por exemplo, o Gerenciador de Driver mantém um identificador de ambiente separado para cada aplicativo que está conectado a ele. Identificadores de ambiente são alocados com **SQLAllocHandle** e liberadas com **SQLFreeHandle**.
