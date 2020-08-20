---
description: Identificadores de ambiente
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1aa22a89288f4dd5a8400484078f57b60fc135fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461498"
---
# <a name="environment-handles"></a>Identificadores de ambiente
Um *ambiente* é um contexto global no qual acessar dados; associado a um ambiente, qualquer informação que seja global por natureza, como:  
  
-   O estado do ambiente  
  
-   O diagnóstico atual no nível do ambiente  
  
-   Os identificadores de conexões atualmente alocadas no ambiente  
  
-   As configurações atuais de cada atributo de ambiente  
  
 Dentro de um trecho de código que implementa o ODBC (o Gerenciador de driver ou um driver), um identificador de ambiente identifica uma estrutura para conter essas informações.  
  
 Os identificadores de ambiente não são usados com frequência em aplicativos ODBC. Eles são sempre usados em chamadas para **SQLDataSources** e **SQLDrivers** e, às vezes, usados em chamadas para **SQLAllocHandle**, **SQLEndTran**, **SQLFreeHandle**, **SQLGetDiagField**e **SQLGetDiagRec**.  
  
 Cada parte do código que implementa o ODBC (o Gerenciador de driver ou um driver) contém um ou mais identificadores de ambiente. Por exemplo, o Gerenciador de driver mantém um identificador de ambiente separado para cada aplicativo conectado a ele. Os identificadores de ambiente são alocados com **SQLAllocHandle** e liberados com **SQLFreeHandle**.
