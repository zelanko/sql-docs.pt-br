---
description: Cursores em bloco
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
ms.openlocfilehash: 5dece0e3ecfc5ef4f3116361a202cfa2d10863ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476818"
---
# <a name="block-cursors"></a>Cursores em bloco
Muitos aplicativos passam uma quantidade significativa de tempo levando os dados pela rede. Parte desse tempo é gasto na verdade, colocando os dados na rede e parte dele é gasto na sobrecarga da rede, como a chamada feita pelo driver para solicitar uma linha de dados. A última vez pode ser reduzida se o aplicativo faz uso eficiente de *bloco,* ou *Fat,* *cursores* , que podem retornar mais de uma linha por vez.  
  
 Um aplicativo sempre tem a opção de usar um cursor de bloco. Em fontes de dados das quais apenas uma linha de cada vez pode ser buscada, os cursores de bloco devem ser simulados no driver. Isso pode ser feito executando várias buscas de linha única. Embora isso seja improvável de fornecer ganhos de desempenho, ele abre oportunidades para aplicativos. Esses aplicativos terão o desempenho aumentado, pois os DBMSs implementam os cursores de bloco nativamente e os drivers associados a esses DBMS os expõem.  
  
 As linhas retornadas em uma única busca com um cursor de bloco são chamadas de *conjunto de linhas*. É importante não confundir o conjunto de linhas com o resultado. O conjunto de resultados é mantido na fonte de dados, enquanto o conjunto de linhas é mantido em buffers de aplicativo. Embora o conjunto de resultados seja corrigido, o conjunto de linhas não é, ele altera a posição e o conteúdo sempre que um novo conjunto de linhas é buscado. Assim como um cursor de linha única, como o cursor tradicional de somente encaminhamento do SQL, aponta para uma linha atual, um cursor de bloco aponta para o conjunto de linhas, que pode ser considerado como *linhas atuais*.  
  
 Para executar operações que operam em uma única linha quando várias linhas foram buscadas, o aplicativo deve primeiro indicar qual linha é a linha atual. A linha atual é exigida por chamadas para **SQLGetData** e as instruções UPDATE e DELETE posicionadas. Quando um cursor em bloco retorna primeiro um conjunto de linhas, a linha atual é a primeira linha do conjunto de linhas. Para alterar a linha atual, o aplicativo chama **SQLSetPos** ou **SQLBulkOperations** (para atualizar por indicador). A ilustração a seguir mostra a relação do conjunto de resultados, conjunto de linhas, linha atual, cursor do conjunto de linhas e cursor de bloco. Para obter mais informações, consulte [usando cursores de bloco](../../../odbc/reference/develop-app/using-block-cursors.md), mais adiante nesta seção e [posicionando instruções UPDATE e Delete](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) e [atualizando dados com SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
 ![Buscando os conjuntos de linhas próximo, anterior, primeiro e último](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 Se um cursor é um cursor de bloco independente de ser rolável. Por exemplo, a maior parte do trabalho em um aplicativo de relatório é gasta com a recuperação e a impressão de linhas. Por isso, ele funcionará mais rapidamente com um cursor de bloqueio somente de avanço. Ele usa um cursor de somente avanço para evitar a despesa de um cursor rolável e um cursor de bloco para reduzir o tráfego de rede.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Colunas de associação para uso com cursores em bloco](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [Usar cursores em bloco](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [Matriz de status da linha](../../../odbc/reference/develop-app/row-status-array.md)
