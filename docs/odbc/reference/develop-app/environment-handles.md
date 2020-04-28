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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b504995e99dfad032598485e370b4d5a6681ae81
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300436"
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
