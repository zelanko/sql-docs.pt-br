---
title: Configurando campos de descritor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 34c4a6e3d98b6711c77fb50d7156207de148881a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094250"
---
# <a name="setting-descriptor-fields"></a>Configurar campos de descritor
Para modificar os campos de um descritor de, um aplicativo pode chamar **SQLSetDescField**. Alguns campos são somente leitura e não podem ser definidos. (Consulte a [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) descrição da função.)  
  
 Campos de registro do descritor são definidos com um número de registro (*RecNumber*) de tempo de 1 ou posterior, os campos de cabeçalho do descritor são definidos com um número de registro de 0. Um número de registro de 0 também é usado para definir campos de indicador, acordo com a convenção de que os indicadores estão contidos na coluna 0. Isso pode deixar a impressão de que os campos de indicador estão contidos dentro do cabeçalho do descritor, mas isso não for o caso. Campos de marcador são diferentes de campos de cabeçalho.  
  
 Ao definir os campos individualmente, o aplicativo deve seguir a sequência definida em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Definir alguns campos faz com que o driver definir outros campos. Isso garante que o descritor sempre está pronto para ser usado depois que o aplicativo tiver especificado um tipo de dados. Quando o aplicativo define o campo SQL_DESC_TYPE, o driver verifica que os outros campos que especificam o tipo são válidos e consistentes.  
  
 Se uma chamada de função que seria definir um campo de descritor falhar, o conteúdo do campo de descritor é indefinido após a chamada de função com falha.
