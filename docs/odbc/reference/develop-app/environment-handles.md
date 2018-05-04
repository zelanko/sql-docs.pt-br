---
title: Identificadores de ambiente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0031b874c1fa9d295002518af80b8ea39b48404b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
