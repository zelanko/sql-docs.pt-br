---
title: Definindo campos de descritores | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 04f9520e2ef462df481bb104e389aeb57b5dd457
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304147"
---
# <a name="setting-descriptor-fields"></a>Configurar campos de descritor
Para modificar os campos de um descritor, um aplicativo pode chamar **SQLSetDescField**. Alguns campos são somente leitura e não podem ser definidos. (Veja a descrição da função [SQLSetDescField.)](../../../odbc/reference/syntax/sqlsetdescfield-function.md)  
  
 Os campos de registro do descritor são definidos com um número recorde *(RecNumber)* de 1 ou mais, enquanto os campos de cabeçalho do descritor são definidos com um número recorde de 0. Um número recorde de 0 também é usado para definir campos de marcação, de acordo com a convenção de que os marcadores estão contidos na coluna 0. Isso pode deixar a impressão de que os campos de marcadores estão contidos no cabeçalho do descritor, mas este não é o caso. Os campos de marcação são diferentes dos campos de cabeçalho.  
  
 Ao definir campos individualmente, o aplicativo deve seguir a seqüência definida no [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). A configuração de alguns campos faz com que o driver defina outros campos. Isso garante que o descritor esteja sempre pronto para ser usado depois que o aplicativo tiver especificado um tipo de dados. Quando o aplicativo define o campo SQL_DESC_TYPE, o driver verifica se outros campos que especificam o tipo são válidos e consistentes.  
  
 Se uma chamada de função que definirum campo descritor falhar, o conteúdo do campo descritor será indefinido após a chamada de função com falha.
