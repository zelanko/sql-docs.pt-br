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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284348"
---
# <a name="unicode-drivers"></a>Drivers Unicode
Se um motorista deve ser um driver Unicode ou um driver ANSI depende inteiramente da natureza da fonte de dados. Se a fonte de dados suportar dados Unicode, o driver deve ser um driver Unicode. Se a fonte de dados só suportar dados ANSI, o driver deve permanecer como driver ANSI.  
  
 Um driver Unicode deve exportar **SQLConnectW** para ser reconhecido como um driver Unicode pelo Driver Manager.  
  
 Um driver Unicode deve aceitar funções Unicode (com um sufixo de *W*) e armazenar dados Unicode. Ele também pode aceitar funções ANSI, mas não é necessário. (O Driver Manager não passa uma chamada de função ANSI com o sufixo *A* para o driver, mas converte-a em uma chamada de função ANSI sem o sufixo e depois passa para o driver.)  
  
 Um driver Unicode deve ser capaz de retornar conjuntos de resultados em Unicode ou ANSI, dependendo da vinculação do aplicativo. Se um aplicativo se vincular a SQL_C_CHAR, o driver Unicode deve converter dados SQL_WCHAR para SQL_CHAR. O driver manager mapeará SQL_C_WCHAR para SQL_C_CHAR para drivers ANSI, mas não faz nenhum mapeamento para drivers Unicode.  
  
> [!NOTE]  
>  Ao determinar o tipo de driver, o Driver Manager ligará para **o SQLSetConnectAttr** e definirá o atributo SQL_ATTR_ANSI_APP na hora da conexão. Se o aplicativo estiver usando APIs ANSI, SQL_ATTR_ANSI_APP será definido como SQL_AA_TRUE e, se estiver usando unicode, ele será definido como um valor de SQL_AA_FALSE. Este atributo é usado para que o motorista possa exibir diferentes comportamentos com base no tipo de aplicativo. O atributo não pode ser definido diretamente pelo aplicativo e não é suportado pelo **SQLGetConnectAttr**. Se um driver apresentar o mesmo comportamento para aplicativos ANSI e Unicode, ele deve retornar SQL_ERROR para esse atributo. Se o driver retornar SQL_SUCCESS, o Gerenciador de driver separação das conexões ANSI e Unicode quando o Pooling de Conexões for usado.
