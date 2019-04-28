---
title: Aplicativos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc655740701822d8c6ff9595327b906ee9a67026
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62734992"
---
# <a name="applications"></a>Aplicativos
Uma *aplicativo* é um programa que chama a API ODBC para acessar os dados. Embora muitos tipos de aplicativos são possíveis, a maioria se enquadram em três categorias, que são usadas como exemplos ao longo deste guia.  
  
-   **Aplicativos genéricos** também conhecidos como configuração inicial pelo usuário de aplicativos ou aplicativos prontos para uso. Aplicativos genéricos são projetados para trabalhar com uma variedade de diferentes DBMSs. Exemplos incluem uma planilha ou pacote de estatísticas que usa o ODBC para importar dados para análise posterior e um processador de texto que usa ODBC para obter uma lista de endereçamento de um banco de dados.  
  
     Uma subcategoria importante de aplicativos genéricos é ambientes de desenvolvimento de aplicativos, como PowerBuilder ou Microsoft® Visual Basic®. Embora os aplicativos construídos com esses ambientes provavelmente funcionará apenas com um DBMS único, o ambiente em si precisa trabalhar com vários DBMSs.  
  
     O que todos os aplicativos genéricos têm em comum é que são altamente interoperáveis entre DBMSs e eles precisam usar o ODBC de uma maneira relativamente genérica. Para obter mais informações sobre a interoperabilidade, consulte [escolhendo um nível de interoperabilidade](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md).  
  
-   **Aplicativos verticais** aplicativos verticais executar um único tipo de tarefa, como entrada de ordem ou dados de fabricação, de controle e trabalhar com um esquema de banco de dados que é controlado pelo desenvolvedor do aplicativo. Para um determinado cliente, o aplicativo funciona com um único DBMS. Por exemplo, uma pequena empresa pode usar o aplicativo com dBase, embora uma grande empresa pode usá-lo com a Oracle.  
  
     O aplicativo usa o ODBC de forma que o aplicativo não está vinculado a qualquer um DBMS, embora ele pode ser associado a um número limitado de DBMSs que fornecem funcionalidade semelhante. Portanto, o desenvolvedor de aplicativos pode vender o aplicativo independentemente do DBMS. Aplicativos verticais são interoperáveis quando eles são desenvolvidos, mas, às vezes, são modificados para incluir código noninteroperable depois que o cliente escolher um DBMS.  
  
-   **Aplicativos personalizados** aplicativos personalizados são usados para executar uma tarefa específica em uma única empresa. Por exemplo, um aplicativo em uma grande empresa pode coletar dados de vendas de várias divisões (cada um deles usa um DBMS diferente) e criar um único relatório. ODBC é usado porque ele é uma interface comum e evita que os programadores precisam aprender diversas interfaces. Esses aplicativos geralmente não são interoperáveis e são gravados em drivers e DBMSs específicos.  
  
 Um número de tarefas é comuns a todos os aplicativos, independentemente de como usar o ODBC. Juntas, elas definem principalmente o fluxo de qualquer aplicativo ODBC. As tarefas são:  
  
-   Selecionar uma fonte de dados e se conectar a ele.  
  
-   Enviando uma instrução SQL para execução.  
  
-   Recuperando resultados (se houver).  
  
-   Erros de processamento.  
  
-   Confirmar ou reverter a transação incluir a instrução SQL.  
  
-   Desconectando da fonte de dados.  
  
 Como a maioria dos trabalho de acesso de dados é feito com o SQL, a tarefa principal para os quais aplicativos usam o ODBC é enviar instruções SQL e recuperar os resultados (se houver) gerados por essas instruções. Outras tarefas para os quais aplicativos usam ODBC incluem determinando e ajustar-se aos recursos de driver e procurar o catálogo de banco de dados.
