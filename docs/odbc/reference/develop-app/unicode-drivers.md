---
title: Drivers de Unicode | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e73a559545a870d83e3d8e2e94dd20f6731f72eb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="unicode-drivers"></a>Drivers de Unicode
Se um driver deve ser um driver de Unicode ou um driver de ANSI depende completamente a natureza da fonte de dados. Se a fonte de dados oferece suporte a dados Unicode, o driver deve ser um driver de Unicode. Se a fonte de dados suporta apenas dados ANSI, o driver deve permanecer um driver de ANSI.  
  
 Um driver de Unicode deve exportar **SQLConnectW** seja reconhecido como um driver de Unicode pelo Gerenciador de Driver.  
  
 Um driver de Unicode deve aceitar funções Unicode (com um sufixo de *W*) e armazenar dados Unicode. Ele também pode aceitar funções ANSI, mas não é necessário. (O Gerenciador de Driver não passa uma chamada de função ANSI a *um* sufixo para o driver, mas converte-o para ANSI função chamada sem o sufixo e, em seguida, passa-lo para o driver.)  
  
 Um driver de Unicode deve ser capaz de retornar conjuntos de resultados em Unicode ou ANSI, dependendo da associação do aplicativo. Se um aplicativo associa a SQL_C_CHAR, o driver de Unicode deve converter dados SQL_WCHAR em SQL_CHAR. O Gerenciador de driver será mapeada SQL_C_WCHAR SQL_C_CHAR para drivers de ANSI, mas não nenhum mapeamento para drivers de Unicode.  
  
> [!NOTE]  
>  Ao determinar o tipo de driver, o Gerenciador de Driver chamará **SQLSetConnectAttr** e definir o atributo SQL_ATTR_ANSI_APP em tempo de conexão. Se o aplicativo está usando APIs ANSI, SQL_ATTR_ANSI_APP será definido como SQL_AA_TRUE e se ele estiver usando o Unicode, ele será definido como um valor de SQL_AA_FALSE. Este atributo é usado para que o driver pode apresentar um comportamento diferente com base no tipo de aplicativo. O atributo não pode ser definido diretamente pelo aplicativo e não é suportado por **SQLGetConnectAttr**. Se um driver apresentar o mesmo comportamento para aplicativos ANSI e Unicode, ele deverá retornar SQL_ERROR para este atributo. Se o driver retornará SQL_SUCCESS, o Gerenciador de Driver separará ANSI e Unicode conexões quando o Pooling de Conexão é usado.
