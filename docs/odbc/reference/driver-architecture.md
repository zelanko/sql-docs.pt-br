---
title: Arquitetura de driver | Microsoft Docs
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
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a74f6e1b212f570ba9aa47a09310b63b13ee0e42
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="driver-architecture"></a>Arquitetura do driver
Arquitetura do driver se encaixa em duas categorias, dependendo de quais instruções SQL de processos de software:  
  
-   **Drivers baseados em arquivo** o driver acessa os dados físicos diretamente. Nesse caso, o driver atua como o driver e a fonte de dados; ou seja, ele processa as chamadas ODBC e instruções SQL. Por exemplo, drivers dBASE são drivers baseados em arquivo como dBASE não fornece que um mecanismo de banco de dados autônomo o driver pode usar. É importante observar que os desenvolvedores de drivers baseados em arquivo devem gravar seus próprios mecanismos de banco de dados.  
  
-   **Drivers baseados em DBMS** o driver acessa os dados físicos por meio de um mecanismo de banco de dados separado. Nesse caso, o driver processa apenas chamadas ODBC; ele passa instruções SQL para o mecanismo de banco de dados para processamento. Por exemplo, drivers Oracle são drivers baseados em DBMS porque Oracle tem um mecanismo de banco de dados independente, que o driver usa. Onde reside o mecanismo de banco de dados é irrelevante. Ele pode residir no mesmo computador que o driver ou em um computador diferente na rede; ele ainda poderá ser acessado por meio de um gateway.  
  
 Arquitetura do driver é geralmente interessante somente gravadores de driver; ou seja, a arquitetura do driver geralmente não faz diferença para o aplicativo. No entanto, a arquitetura pode afetar se um aplicativo pode usar SQL DBMS específico. Por exemplo, o Microsoft Access fornece um mecanismo de banco de dados autônomo. Se um driver do Microsoft Access for baseada em DBMS — ela acessa os dados por meio desse mecanismo — o aplicativo pode passar instruções SQL do Microsoft Access para o mecanismo de processamento.  
  
 No entanto, se o driver for baseada em arquivo — ou seja, ele contém um mecanismo de proprietário que acessa o arquivo. mdb do Access do Microsoft® diretamente, qualquer tentativa de passar instruções SQL específicas do Microsoft Access para o mecanismo é provavelmente resultará em erros de sintaxe. O motivo é que o mecanismo de proprietário é implementar apenas ODBC SQL.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Drivers baseados em arquivo](../../odbc/reference/file-based-drivers.md)  
  
-   [Drivers baseados em DBMS](../../odbc/reference/dbms-based-drivers.md)  
  
-   [Exemplo de rede](../../odbc/reference/network-example.md)  
  
-   [Outras arquiteturas do driver](../../odbc/reference/other-driver-architectures.md)

