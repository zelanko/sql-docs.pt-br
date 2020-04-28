---
title: Drivers Unicode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aabdd899d78c1141716725d57e343dc002dc96ad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284348"
---
# <a name="unicode-drivers"></a>Drivers Unicode
Se um driver deve ser um driver Unicode ou um driver ANSI depende totalmente da natureza da fonte de dados. Se a fonte de dados der suporte a dados Unicode, o driver deverá ser um driver Unicode. Se a fonte de dados der suporte apenas a dados ANSI, o driver deverá permanecer como um driver ANSI.  
  
 Um driver Unicode deve exportar **SQLConnectW** para ser reconhecido como um driver Unicode pelo Gerenciador de driver.  
  
 Um driver Unicode deve aceitar funções Unicode (com um sufixo de *W*) e armazenar dados Unicode. Ele também pode aceitar funções ANSI, mas não é necessário para. (O Gerenciador de driver não passa uma chamada de função ANSI com *o sufixo* a para o driver, mas converte-o em uma chamada de função ANSI sem o sufixo e, em seguida, passa-o para o driver.)  
  
 Um driver Unicode deve ser capaz de retornar conjuntos de resultados em Unicode ou ANSI, dependendo da associação do aplicativo. Se um aplicativo for associado a SQL_C_CHAR, o driver Unicode deverá converter SQL_WCHAR dados em SQL_CHAR. O Gerenciador de driver irá mapear SQL_C_WCHAR para SQL_C_CHAR para drivers ANSI, mas não faz mapeamento para drivers Unicode.  
  
> [!NOTE]  
>  Ao determinar o tipo de driver, o Gerenciador de driver chamará **SQLSetConnectAttr** e definirá o atributo SQL_ATTR_ANSI_APP no momento da conexão. Se o aplicativo estiver usando APIs ANSI, SQL_ATTR_ANSI_APP será definido como SQL_AA_TRUE e, se estiver usando Unicode, ele será definido como um valor de SQL_AA_FALSE. Esse atributo é usado para que o driver possa exibir um comportamento diferente com base no tipo de aplicativo. O atributo não pode ser definido pelo aplicativo diretamente e não tem suporte do **SQLGetConnectAttr**. Se um driver exibir o mesmo comportamento para os aplicativos ANSI e Unicode, ele deverá retornar SQL_ERROR para esse atributo. Se o driver retornar SQL_SUCCESS, o Gerenciador de driver irá separar as conexões ANSI e Unicode quando o pool de conexões for usado.
