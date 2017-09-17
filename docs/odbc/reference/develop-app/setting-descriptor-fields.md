---
title: Definindo campos de descritor | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f4e63f722842846815fd96bed7293388c4f86c75
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setting-descriptor-fields"></a>Campos de descritor de configuração
Para modificar os campos de um descritor de, um aplicativo pode chamar **SQLSetDescField**. Alguns campos são somente leitura e não podem ser definidos. (Consulte o [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) descrição da função.)  
  
 Campos de registro do descritor são definidos com um número de registro (*RecNumber*) de tempo de 1 ou superior, os campos de cabeçalho do descritor são definidos com um número de registro de 0. Um número de registro de 0 também é usado para definir campos de indicador, de acordo com a convenção de que os indicadores estão contidos na coluna 0. Isso pode deixar a impressão de que os campos bookmark estão contidos dentro do cabeçalho do descritor, mas isso não for o caso. Campos de indicadores são diferentes de campos de cabeçalho.  
  
 Ao definir campos individualmente, o aplicativo deve seguir a sequência definida no [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Definir alguns campos faz com que o driver definir outros campos. Isso garante que o descritor sempre está pronto para ser usado quando o aplicativo especificou um tipo de dados. Quando o aplicativo define o campo SQL_DESC_TYPE, o driver verifica que outros campos que especificam o tipo são válidos e consistentes.  
  
 Se uma chamada de função que seria definir um campo de descritor falhar, o conteúdo do campo de descritor é indefinido após a chamada de função com falha.
