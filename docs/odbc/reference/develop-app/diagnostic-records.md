---
title: Registros de Diagnóstico | Microsoft Docs
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
ms.openlocfilehash: b564f2837bc76e04011170e191d00c08d10c119d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305177"
---
# <a name="diagnostic-records"></a>Registros de diagnóstico
Associados a cada ambiente, conexão, declaração e alça descritor são *registros de diagnóstico*. Esses registros contêm informações de diagnóstico sobre a última função chamada que usou uma alça específica. Os registros são substituídos somente quando outra função é chamada usando essa alça. Não há limite para o número de registros diagnósticos que podem ser armazenados a qualquer momento.  
  
 Existem dois tipos de registros de diagnóstico: um *registro de cabeçalho* e zero ou mais *registros de status*. O registro de cabeçalho é o recorde 0; os registros de status são registros 1 e superior. Os registros de diagnóstico são compostos por uma série de campos separados, que são diferentes para o registro de cabeçalho e os registros de status. Além disso, os componentes ODBC podem definir seus próprios campos de registro de diagnóstico.  
  
 Embora os registros diagnósticos possam ser considerados como estruturas, não há necessidade de que sejam realmente estruturas; como um motorista armazena as informações de diagnóstico é específico do motorista.  
  
 Os campos nos registros de diagnóstico são recuperados com **o SQLGetDiagField**. O SQLSTATE, o número de erro nativo e os campos de mensagens de diagnóstico de registros de status podem ser recuperados em uma única chamada com **o SQLGetDiagRec**.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Registro de cabeçalho](../../../odbc/reference/develop-app/header-record.md)  
  
-   [Registros de status](../../../odbc/reference/develop-app/status-records.md)
