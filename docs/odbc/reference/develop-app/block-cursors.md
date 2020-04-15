---
title: Cursors de bloco | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa35888ef93da9648fe6422bdc35ebf9da3a0525
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306347"
---
# <a name="block-cursors"></a>Cursores em bloco
Muitos aplicativos gastam uma quantidade significativa de tempo trazendo dados em toda a rede. Parte desse tempo é gasto realmente trazendo os dados através da rede, e parte dele é gasto em sobrecarga de rede, como a chamada feita pelo motorista para solicitar uma linha de dados. Este último tempo pode ser reduzido se a aplicação fizer uso eficiente de *blocos,* ou *gordura,* *cursores,* que podem retornar mais de uma linha de cada vez.  
  
 Um aplicativo sempre tem a opção de usar um cursor de bloco. Nas fontes de dados das quais apenas uma linha de cada vez pode ser buscada, os cursores de bloco devem ser simulados no driver. Isso pode ser feito realizando várias buscas de linha única. Embora isso seja improvável de proporcionar ganhos de desempenho, ele abre oportunidades para aplicações. Esses aplicativos sofrerão aumentos de desempenho à medida que os DBMSs implementarem cursores de bloco nativamente e os drivers associados a esses DBMSs os expõem.  
  
 As linhas retornadas em uma única busca com um cursor de bloco são chamadas *de conjunto de linhas*. É importante não confundir o conjunto de linhas com o conjunto de resultados. O conjunto de resultados é mantido na fonte de dados, enquanto o conjunto de linhas é mantido em buffers de aplicativos. Enquanto o conjunto de resultados é corrigido, o conjunto de linhas não é - ele muda de posição e conteúdo cada vez que um novo conjunto de linhas é buscado. Assim como um cursor de linha única, como o cursor tradicional somente para a frente SQL, aponta para uma linha atual, um cursor de bloco aponta para o conjunto de linhas, que pode ser considerado como *linhas atuais*.  
  
 Para executar operações que operam em uma única linha quando várias linhas foram buscadas, o aplicativo deve primeiro indicar qual linha é a linha atual. A linha atual é exigida por chamadas para **SQLGetData** e instruções de atualização e exclusão posicionadas. Quando um cursor de bloco retorna primeiro um conjunto de linhas, a linha atual é a primeira linha do conjunto de linhas. Para alterar a linha atual, o aplicativo chama **SQLSetPos** ou **SQLBulkOperations** (para atualizar por marcador). A ilustração a seguir mostra a relação do conjunto de resultados, conjunto de linhas, linha atual, cursor de conjunto de linhas e cursor de bloco. Para obter mais informações, consulte [Usando cursors de bloco,](../../../odbc/reference/develop-app/using-block-cursors.md)mais tarde nesta seção, e [Instruções de atualização e exclusão posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) e [dados de atualização com SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
 ![Buscando os conjuntos de linhas próximo, anterior, primeiro e último](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 Se um cursor é um cursor de bloco é independente de se ele é rolável. Por exemplo, a maior parte do trabalho em um aplicativo de relatório é gasto recuperando e imprimindo linhas. Por causa disso, ele funcionará mais rápido com um cursor de bloco somente para a frente. Ele usa um cursor somente para frente para evitar a despesa de um cursor rolável e um cursor de bloco para reduzir o tráfego da rede.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Colunas de associação para uso com cursores em bloco](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [Usar cursores em bloco](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [Matriz de status da linha](../../../odbc/reference/develop-app/row-status-array.md)
