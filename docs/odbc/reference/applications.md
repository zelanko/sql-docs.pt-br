---
title: Aplicativos | Microsoft Docs
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
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f2a2e9924d032e3ccc32d613a1799c3abd84880f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="applications"></a>Aplicativos
Um *aplicativo* é um programa que chama a API de ODBC para acessar dados. Embora muitos tipos de aplicativos são possíveis, a maioria se enquadram em três categorias, que são usadas como exemplos em todo este guia.  
  
-   **Aplicativos genéricos** também conhecidos como aplicativos têm embalagem ou aplicativos disponíveis no mercado. Aplicativos genéricos são projetados para trabalhar com uma variedade de diferentes DBMSs. Exemplos incluem uma planilha ou pacote de estatísticas que usa ODBC para importar dados para análise posterior e um processador de texto que usa ODBC para obter uma lista de endereçamento de um banco de dados.  
  
     Uma subcategoria importante de aplicativos genéricos é ambientes de desenvolvimento de aplicativos, como PowerBuilder ou Microsoft® Visual Basic®. Embora os aplicativos construídos com esses ambientes provavelmente funcionará apenas com um único DBMS, o ambiente em si precisa trabalhar com vários DBMSs.  
  
     O que todos os aplicativos genéricos têm em comum é que são altamente interoperáveis entre DBMSs e eles precisam usar o ODBC de maneira relativamente genérica. Para obter mais informações sobre interoperabilidade, consulte [escolhendo um nível de interoperabilidade](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md).  
  
-   **Aplicativos verticais** aplicativos verticais executar um único tipo de tarefa, como entrada de ordem ou controle de dados de produção e trabalhar com um esquema de banco de dados que é controlado pelo desenvolvedor do aplicativo. Para um determinado cliente, o aplicativo funciona com um único DBMS. Por exemplo, uma pequena empresa pode usar o aplicativo com dBase, enquanto uma grande empresa poderá usá-lo com o Oracle.  
  
     O aplicativo usa o ODBC de modo que o aplicativo não estiver associado a qualquer um DBMS, embora ele pode ser ligado a um número limitado de DBMSs que fornecem funcionalidade semelhante. Portanto, o desenvolvedor do aplicativo pode vender o aplicativo independentemente do DBMS. Aplicativos verticais são interoperáveis quando eles são desenvolvidos, mas às vezes são modificados para incluir código noninteroperable depois que o cliente escolher um DBMS.  
  
-   **Aplicativos personalizados** aplicativos personalizados são usados para executar uma tarefa específica em uma única empresa. Por exemplo, um aplicativo em uma grande empresa poderá coletar dados de vendas de várias divisões (cada um deles usa um DBMS diferente) e criar um único relatório. ODBC é usado porque ele é uma interface comum e salva os programadores precisa aprender várias interfaces. Esses aplicativos geralmente não são interoperáveis e são gravados DBMSs e drivers específicos.  
  
 Um número de tarefas é comuns a todos os aplicativos, independentemente de como usar o ODBC. Juntos, eles definem em grande parte do fluxo de qualquer aplicativo ODBC. As tarefas são:  
  
-   Selecionar uma fonte de dados e conectar-se a ele.  
  
-   Enviando uma instrução SQL para execução.  
  
-   Recuperando resultados (se houver).  
  
-   Erros de processamento.  
  
-   Confirmar ou reverter a transação envolve a instrução SQL.  
  
-   Desconectando da fonte de dados.  
  
 Como a maioria dos dados para o trabalho de acesso é feito com o SQL, a tarefa primária para as quais aplicativos usam o ODBC é enviar instruções SQL e recuperar os resultados (se houver) gerados por essas instruções. Outras tarefas para que os aplicativos usam ODBC incluem determinar e ajustando a recursos de driver e navegando o catálogo de banco de dados.
