---
title: Alças do Meio Ambiente | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300436"
---
# <a name="environment-handles"></a>Identificadores de ambiente
Um *ambiente* é um contexto global no qual acessar dados; associado a um ambiente é qualquer informação de natureza global, tais como:  
  
-   Estado do meio ambiente  
  
-   Os diagnósticos atuais em nível de ambiente  
  
-   As alças das conexões atualmente alocadas no meio ambiente  
  
-   As configurações atuais de cada atributo ambiente  
  
 Dentro de um código que implementa o ODBC (o Driver Manager ou um driver), uma alça de ambiente identifica uma estrutura para conter essas informações.  
  
 As alças de ambiente não são usadas com freqüência em aplicações ODBC. Eles são sempre usados em chamadas para **SQLDataSources** e **SQLDrivers** e às vezes são usados em chamadas para **SQLAllocHandle,** **SQLEndTran,** **SQLFreeHandle,** **SQLGetDiagField**e **SQLGetDiagRec**.  
  
 Cada pedaço de código que implementa o ODBC (o Driver Manager ou um driver) contém uma ou mais alças de ambiente. Por exemplo, o Driver Manager mantém uma alça de ambiente separada para cada aplicativo conectado a ele. As alças do ambiente são alocadas com **SQLAllocHandle** e liberadas com **SQLFreeHandle**.
