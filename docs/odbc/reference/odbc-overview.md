---
title: "Visão geral do ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9c69180bcf3babcfaaef5d513d6c47954478ef39
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-overview"></a>Visão geral do ODBC
Conectividade de banco de dados aberto (ODBC) é uma interface de programação de aplicativo amplamente aceito (API) para acesso ao banco de dados. Ele é baseado nas especificações do Open Group e ISO/IEC Interface de nível de chamada (CLI) para o banco de dados APIs e usa a linguagem SQL (Structured Query) como sua linguagem de acesso de banco de dados.  
  
 ODBC é projetado para máximo *interoperabilidade* -ou seja, a capacidade de um único aplicativo para acessar os sistemas de gerenciamento de outro banco de dados (DBMSs) com o mesmo código-fonte. Aplicativos de banco de dados chamam funções na interface do ODBC, que são implementadas em módulos específicos ao banco de dados chamados *drivers*. O uso de drivers isola os aplicativos de chamadas de banco de dados específicos da mesma forma que os drivers de impressora isolar programas de processamento de texto de comandos específicos da impressora. Como drivers são carregados em tempo de execução, um usuário só precisa adicionar um novo driver para acessar um DBMS novo; não é necessário recompilar ou vincular novamente o aplicativo.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Por que o ODBC foi criado?](../../odbc/reference/why-was-odbc-created.md)  
  
-   [O que é o ODBC?](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC e a CLI padrão](../../odbc/reference/odbc-and-the-standard-cli.md)
