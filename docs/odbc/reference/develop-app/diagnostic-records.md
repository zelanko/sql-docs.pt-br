---
description: Registros de diagnóstico
title: Registros de diagnóstico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- handles [ODBC], diagnostic records
- header records [ODBC]
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 92c73f9b-3ed7-410d-9cec-2771004aae60
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1b407ef1f8664191a16f54942f42f4088824517c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499917"
---
# <a name="diagnostic-records"></a>Registros de diagnóstico
Associados a cada ambiente, conexão, instrução e identificador de descritor são *registros de diagnóstico*. Esses registros contêm informações de diagnóstico sobre a última função chamada que usava um identificador específico. Os registros são substituídos somente quando outra função é chamada usando esse identificador. Não há nenhum limite para o número de registros de diagnóstico que podem ser armazenados a qualquer momento.  
  
 Há dois tipos de registros de diagnóstico: um *registro de cabeçalho* e zero ou mais *registros de status*. O registro de cabeçalho é o registro 0; os registros de status são registros 1 e acima. Os registros de diagnóstico são compostos de vários campos separados, que são diferentes para o registro de cabeçalho e os registros de status. Além disso, os componentes ODBC podem definir seus próprios campos de registro de diagnóstico.  
  
 Embora os registros de diagnóstico possam ser considerados como estruturas, não há nenhum requisito para que eles realmente sejam estruturas; como um driver armazena as informações de diagnóstico são específicas do driver.  
  
 Os campos nos registros de diagnóstico são recuperados com **SQLGetDiagField**. Os campos SQLSTATE, número de erro nativo e mensagem de diagnóstico dos registros de status podem ser recuperados em uma única chamada com **SQLGetDiagRec**.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Registro de cabeçalho](../../../odbc/reference/develop-app/header-record.md)  
  
-   [Registros de status](../../../odbc/reference/develop-app/status-records.md)
