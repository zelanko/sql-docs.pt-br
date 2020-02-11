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
ms.openlocfilehash: f15b5e8eb6eb7c63ab771030f0c31e8c9ff92724
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135684"
---
# <a name="applications"></a>Aplicativos
Um *aplicativo* é um programa que chama a API ODBC para acessar dados. Embora muitos tipos de aplicativos sejam possíveis, a maioria se enquadra em três categorias, que são usadas como exemplos em todo este guia.  
  
-   **Aplicativos genéricos** Eles também são chamados de aplicativos com redução de encolhimento ou aplicativos prontos para serem acessados. Os aplicativos genéricos são projetados para funcionar com uma variedade de DBMSs diferentes. Os exemplos incluem uma planilha ou um pacote de estatísticas que usa o ODBC para importar dados para análise adicional e um processador de texto que usa o ODBC para obter uma lista de endereçamento de um banco de dados.  
  
     Uma subcategoria importante de aplicativos genéricos são os ambientes de desenvolvimento de aplicativos, como o PowerBuilder ou o Microsoft® Visual Basic®. Embora os aplicativos construídos com esses ambientes provavelmente funcionem apenas com um único DBMS, o próprio ambiente precisa trabalhar com vários DBMSs.  
  
     O que todos os aplicativos genéricos têm em comum é que eles são altamente interoperáveis entre DBMSs e precisam usar o ODBC de maneira relativamente genérica. Para obter mais informações sobre interoperabilidade, consulte [escolhendo um nível de interoperabilidade](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md).  
  
-   **Aplicativos verticais** Os aplicativos verticais executam um único tipo de tarefa, como entrada de pedido ou rastreamento de dados de fabricação, e trabalham com um esquema de banco de dados que é controlado pelo desenvolvedor do aplicativo. Para um cliente específico, o aplicativo funciona com um único DBMS. Por exemplo, uma pequena empresa pode usar o aplicativo com o dBase, enquanto uma grande empresa pode usá-lo com a Oracle.  
  
     O aplicativo usa o ODBC de forma que o aplicativo não esteja vinculado a um DBMS, embora possa estar vinculado a um número limitado de DBMSs que fornecem funcionalidade semelhante. Portanto, o desenvolvedor do aplicativo pode vender o aplicativo independentemente do DBMS. Os aplicativos verticais são interoperáveis quando são desenvolvidos, mas às vezes são modificados para incluir o código noninteroperable depois que o cliente escolhe um DBMS.  
  
-   **Aplicativos personalizados** Os aplicativos personalizados são usados para executar uma tarefa específica em uma única empresa. Por exemplo, um aplicativo em uma grande empresa pode coletar dados de vendas de várias divisões (cada uma delas usa um DBMS diferente) e criar um único relatório. O ODBC é usado porque é uma interface comum e evita que os programadores precisem aprender várias interfaces. Esses aplicativos geralmente não são interoperáveis e são gravados em DBMSs e drivers específicos.  
  
 Várias tarefas são comuns a todos os aplicativos, independentemente de como usam o ODBC. Juntos, eles definem amplamente o fluxo de qualquer aplicativo ODBC. As tarefas são:  
  
-   Selecionando uma fonte de dados e conectando-se a ela.  
  
-   Enviando uma instrução SQL para execução.  
  
-   Recuperando resultados (se houver).  
  
-   Erros de processamento.  
  
-   Confirmando ou revertendo a transação que está delimitando a instrução SQL.  
  
-   Desconectando da fonte de dados.  
  
 Como a maior parte do trabalho de acesso a dados é feita com o SQL, a tarefa principal para a qual os aplicativos usam o ODBC é enviar instruções SQL e recuperar os resultados (se houver) gerados por essas instruções. Outras tarefas para as quais os aplicativos usam ODBC incluem a determinação e o ajuste de recursos de driver e a navegação no catálogo de banco de dados.
