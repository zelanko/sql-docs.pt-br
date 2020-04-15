---
title: Visão geral da ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a0515a882cd7d1c97a60e9262942bd7c397b0b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298286"
---
# <a name="odbc-overview"></a>Visão geral do ODBC
Open Database Connectivity (ODBC) é uma interface de programação de aplicativos (API) amplamente aceita para acesso ao banco de dados. Baseia-se nas especificações de Call-Level Interface (CLI) do Open Group e ISO/IEC para APIs de banco de dados e usa o SQL (Structured Query Language, linguagem de consulta estruturada) como linguagem de acesso ao banco de dados.  
  
 O ODBC foi projetado para *interoperabilidade* máxima - ou seja, a capacidade de um único aplicativo acessar diferentes sistemas de gerenciamento de banco de dados (DBMSs) com o mesmo código-fonte. Os aplicativos de banco de dados chamam funções na interface ODBC, que são implementadas em módulos específicos de banco de dados chamados *drivers*. O uso de drivers isola os aplicativos de chamadas específicas de banco de dados da mesma forma que os drivers de impressora isolam programas de processamento de texto de comandos específicos da impressora. Como os drivers são carregados em tempo de execução, o usuário só precisa adicionar um novo driver para acessar um novo DBMS; não é necessário recompilar ou revincular o aplicativo.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Por que o ODBC foi criado?](../../odbc/reference/why-was-odbc-created.md)  
  
-   [O que é o ODBC?](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC e a CLI padrão](../../odbc/reference/odbc-and-the-standard-cli.md)
