---
title: Aplicações | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9184986883f64bd082ca1db472d887609d3071bd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306547"
---
# <a name="applications"></a>Aplicativos
Um *aplicativo* é um programa que chama a API ODBC para acessar dados. Embora muitos tipos de aplicações sejam possíveis, a maioria se enquadra em três categorias, que são usadas como exemplos ao longo deste guia.  
  
-   **Aplicações genéricas** Estes também são referidos como aplicativos embrulhados para encolher ou aplicativos fora da prateleira. Aplicações genéricas são projetadas para trabalhar com uma variedade de DBMSs diferentes. Exemplos incluem uma planilha ou pacote de estatísticas que usa o ODBC para importar dados para análise suplementar e um processador de texto que usa ODBC para obter uma lista de discussão de um banco de dados.  
  
     Uma subcategoria importante de aplicativos genéricos são os ambientes de desenvolvimento de aplicativos, como PowerBuilder ou Microsoft® Visual Basic®. Embora os aplicativos construídos com esses ambientes provavelmente funcionem apenas com um único DBMS, o ambiente em si precisa trabalhar com vários DBMSs.  
  
     O que todas as aplicações genéricas têm em comum é que elas são altamente interoperáveis entre os DBMSs e precisam usar o ODBC de forma relativamente genérica. Para obter mais informações sobre interoperabilidade, consulte [Escolher um Nível de Interoperabilidade](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md).  
  
-   **Aplicações verticais** Os aplicativos verticais realizam um único tipo de tarefa, como a entrada de pedidos ou o rastreamento de dados de fabricação, e trabalham com um esquema de banco de dados controlado pelo desenvolvedor do aplicativo. Para um determinado cliente, o aplicativo funciona com um único DBMS. Por exemplo, uma pequena empresa pode usar o aplicativo com dBase, enquanto uma grande empresa pode usá-lo com o Oracle.  
  
     O aplicativo usa ODBC de tal forma que o aplicativo não está vinculado a nenhum DBMS, embora possa estar vinculado a um número limitado de DBMSs que fornecem funcionalidade semelhante. Assim, o desenvolvedor de aplicativos pode vender o aplicativo independentemente do DBMS. As aplicações verticais são interoperáveis quando são desenvolvidas, mas às vezes são modificadas para incluir código não interoperável uma vez que o cliente tenha escolhido um DBMS.  
  
-   **Aplicativos personalizados** Aplicativos personalizados são usados para executar uma tarefa específica em uma única empresa. Por exemplo, um aplicativo em uma grande empresa pode coletar dados de vendas de várias divisões (cada uma das quais usa um DBMS diferente) e criar um único relatório. O ODBC é usado porque é uma interface comum e salva programadores de ter que aprender várias interfaces. Esses aplicativos geralmente não são interoperáveis e são escritos para DBMSs e drivers específicos.  
  
 Uma série de tarefas são comuns a todos os aplicativos, não importa como eles usam ODBC. Juntos, eles definem em grande parte o fluxo de qualquer aplicação ODBC. As tarefas são:  
  
-   Selecionando uma fonte de dados e conectando-se a ela.  
  
-   Enviando uma declaração SQL para execução.  
  
-   Recuperando resultados (se houver).  
  
-   Erros de processamento.  
  
-   Comprometendo ou revertendo a transação que encerra a declaração SQL.  
  
-   Desconectando-se da fonte de dados.  
  
 Como a maioria dos trabalhos de acesso a dados é feita com o SQL, a tarefa principal para a qual os aplicativos usam o ODBC é enviar instruções SQL e recuperar os resultados (se houver) gerados por essas declarações. Outras tarefas para as quais os aplicativos usam o ODBC incluem determinar e ajustar aos recursos do driver e navegar no catálogo do banco de dados.
