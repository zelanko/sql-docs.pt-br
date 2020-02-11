---
title: Arquitetura do driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd9bbb74d77a0b56b6b1f1aa5d8f1a6b5e97f5aa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915472"
---
# <a name="driver-architecture"></a>Arquitetura do driver
A arquitetura do driver se enquadra em duas categorias, dependendo de qual software processa as instruções SQL:  
  
-   **Drivers baseados em arquivo** O driver acessa os dados físicos diretamente. Nesse caso, o driver atua como o driver e a fonte de dados; ou seja, ele processa chamadas ODBC e instruções SQL. Por exemplo, os drivers do dBASE são drivers baseados em arquivo porque o dBASE não fornece um mecanismo de banco de dados autônomo que o driver pode usar. É importante observar que os desenvolvedores de drivers baseados em arquivo devem gravar seus próprios mecanismos de banco de dados.  
  
-   **Drivers baseados em DBMS** O driver acessa os dados físicos por meio de um mecanismo de banco de dados separado. Nesse caso, o driver processa apenas chamadas ODBC; Ele passa instruções SQL para o mecanismo de banco de dados para processamento. Por exemplo, os drivers do Oracle são drivers baseados em DBMS porque a Oracle tem um mecanismo de banco de dados autônomo que o driver usa. O local em que o mecanismo de banco de dados reside não é material. Ele pode residir no mesmo computador que o driver ou em um computador diferente na rede; Ele pode até ser acessado por meio de um gateway.  
  
 A arquitetura do driver geralmente é interessante apenas para os gravadores de driver; ou seja, a arquitetura do driver geralmente não faz nenhuma diferença para o aplicativo. No entanto, a arquitetura pode afetar se um aplicativo pode usar o SQL específico do DBMS. Por exemplo, o Microsoft Access fornece um mecanismo de banco de dados autônomo. Se um driver do Microsoft Access for baseado em DBMS, ele acessará os dados por meio desse mecanismo. o aplicativo pode passar instruções SQL do Microsoft Access para o mecanismo para processamento.  
  
 No entanto, se o driver for baseado em arquivo – ou seja, ele conterá um mecanismo proprietário que acessa o arquivo. mdb do Microsoft® Access diretamente-qualquer tentativa de passar instruções SQL específicas do Microsoft Access para o mecanismo provavelmente resultará em erros de sintaxe. O motivo é que o mecanismo proprietário provavelmente implementará somente o ODBC SQL.  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Drivers baseados em arquivo](../../odbc/reference/file-based-drivers.md)  
  
-   [Drivers baseados em DBMS](../../odbc/reference/dbms-based-drivers.md)  
  
-   [Exemplo de rede](../../odbc/reference/network-example.md)  
  
-   [Outras arquiteturas do driver](../../odbc/reference/other-driver-architectures.md)
