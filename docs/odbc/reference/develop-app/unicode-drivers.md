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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e555ff4a3b33c4c827371dc1ad63546736d7189
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63473035"
---
# <a name="unicode-drivers"></a>Drivers Unicode
Se um driver deve ser um driver de Unicode ou um driver de ANSI depende totalmente da natureza da fonte de dados. Se a fonte de dados oferece suporte a dados Unicode, o driver deve ser um driver de Unicode. Se a fonte de dados só dá suporte a dados ANSI, o driver deve permanecer um driver de ANSI.  
  
 Um driver de Unicode deve exportar **SQLConnectW** é reconhecido como um driver de Unicode pelo Gerenciador de Driver.  
  
 Um driver de Unicode deve aceitar funções Unicode (com um sufixo *W*) e armazenar dados Unicode. Ele também pode aceitar funções ANSI, mas não é necessário. (O Gerenciador de Driver não passar uma chamada de função ANSI com o *um* sufixo para o driver, mas converte-o para um ANSI de função chamada sem o sufixo e, em seguida, passa-lo para o driver.)  
  
 Um driver de Unicode deve ser capaz de retornar conjuntos de resultados em Unicode ou ANSI, dependendo da associação do aplicativo. Se um aplicativo se associar ao SQL_C_CHAR, o driver de Unicode deve converter os dados SQL_WCHAR em SQL_CHAR. O Gerenciador de driver mapeará SQL_C_WCHAR para SQL_C_CHAR para drivers de ANSI, mas não nenhum mapeamento para drivers de Unicode.  
  
> [!NOTE]  
>  Ao determinar o tipo de driver, o Gerenciador de Driver chamará **SQLSetConnectAttr** e defina o atributo SQL_ATTR_ANSI_APP em tempo de conexão. Se o aplicativo está usando APIs ANSI, SQL_ATTR_ANSI_APP será definido como SQL_AA_TRUE e se ele estiver usando o Unicode, ele será definido como um valor de SQL_AA_FALSE. Esse atributo é usado para que o driver pode apresentar um comportamento diferente com base no tipo de aplicativo. O atributo não pode ser definido diretamente pelo aplicativo, e não é suportado pelo **SQLGetConnectAttr**. Se um driver de apresentar o mesmo comportamento para aplicativos ANSI e Unicode, ele deverá retornar SQL_ERROR para este atributo. Se o driver retornará SQL_SUCCESS, o Gerenciador de Driver vai separar as conexões de ANSI e Unicode quando o pool de Conexão é usado.
