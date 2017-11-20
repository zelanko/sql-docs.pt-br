---
title: Bloquear cursores | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7747f421fe4a7356086cf27ecf62739f34acdd17
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="block-cursors"></a>Cursores em bloco
Muitos aplicativos gastam uma quantidade significativa de tempo para trazer os dados pela rede. Parte desse tempo é gasto na verdade trazer os dados pela rede e parte dele é gasto na sobrecarga de rede, como a chamada feita pelo driver para solicitar uma linha de dados. A última hora pode ser reduzida se o aplicativo faça uso eficiente de *bloco,* ou *fat,* *cursores,* que pode retornar mais de uma linha por vez.  
  
 Um aplicativo sempre tem a opção de usar um cursor em bloco. Em fontes de dados do qual pode ser buscada apenas uma linha por vez, os cursores em bloco devem ser simuladas no driver. Isso pode ser feito executando várias buscas de única linha. Embora isso seja improvável fornecer os ganhos de desempenho, ele abre oportunidades para aplicativos. Esses aplicativos terão aumentos de desempenho, em seguida, como DBMSs implementam cursores em bloco nativamente e os drivers associados a esses DBMSs expõem-los.  
  
 As linhas retornadas em uma única busca com um cursor em bloco são chamadas de *linhas*. É importante não confundir o conjunto de linhas com o conjunto de resultados. O conjunto de resultados é mantido na fonte de dados, enquanto o conjunto de linhas é mantido em buffers do aplicativo. Embora o conjunto de resultados é fixo, o conjunto de linhas não é — altera a posição e o conteúdo de cada vez que um novo conjunto de linhas é buscado. Assim como um cursor de única linha, como os pontos de cursor de somente avanço SQL tradicionais em uma linha atual, um cursor em bloco aponta para o conjunto de linhas, que pode ser pensado como *linhas atuais*.  
  
 Para executar operações que operam em uma única linha quando várias linhas foram buscadas, o aplicativo deve indicar qual linha é a linha atual. A linha atual é necessária por chamadas para **SQLGetData** posicionado atualização e instruções delete. Quando um cursor em bloco primeiro retorna um conjunto de linhas, a linha atual é a primeira linha do conjunto de linhas. Para alterar a linha atual, o aplicativo chama **SQLSetPos** ou **SQLBulkOperations** (para atualização pelo indicador). A ilustração a seguir mostra a relação do conjunto de resultados, conjunto de linhas, a linha atual, o cursor de conjunto de linhas e cursor em bloco. Para obter mais informações, consulte [usando cursores em bloco](../../../odbc/reference/develop-app/using-block-cursors.md), mais adiante nesta seção e [posicionado instruções Update e excluir](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) e [atualizando dados com SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
 ![Buscando o próximo, anterior, primeiro e último conjuntos de linhas](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 Se um cursor é um bloco é independente de se ele é rolável. Por exemplo, a maioria do trabalho em um aplicativo de relatório é gasto recuperando e imprimir linhas. Por isso, ele será funciona de forma rápida com um somente de encaminhamento, cursor em bloco. Ele usa um cursor somente de avanço para evitar a despesa de um cursor rolável e um cursor em bloco para reduzir o tráfego de rede.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Colunas de associação para uso com cursores em bloco](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [Usando cursores em bloco](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [Matriz de status da linha](../../../odbc/reference/develop-app/row-status-array.md)

