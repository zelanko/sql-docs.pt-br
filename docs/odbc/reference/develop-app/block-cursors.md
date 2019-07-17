---
title: Bloquear cursores | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e0ea6ff655140c979f400f67a59cd7259bac9e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118816"
---
# <a name="block-cursors"></a>Cursores em bloco
Muitos aplicativos gastam uma quantidade significativa de tempo de trazer dados pela rede. Parte desse tempo é gasto na verdade, trazer os dados pela rede e parte dela é gasto na sobrecarga de rede, como a chamada feita pelo driver para solicitar uma linha de dados. A hora do último pode ser reduzida se o aplicativo faz uso eficiente de *bloco,* ou *fat* *cursores,* que pode retornar mais de uma linha por vez.  
  
 Um aplicativo sempre tem a opção de usar um cursor em bloco. Em fontes de dados do qual pode ser buscada apenas uma linha por vez, os cursores em bloco devem ser simuladas no driver. Isso pode ser feito executando vários buscas de única linha. Embora isso seja improvável que fornecem os ganhos de desempenho, ele abre oportunidades para aplicativos. Esses aplicativos, em seguida, experimentará aumentos de desempenho como DBMSs implementam cursores em bloco nativamente e os drivers associados a esses DBMSs expõem-los.  
  
 As linhas retornadas em uma única busca com um cursor em bloco são chamadas de *conjunto de linhas*. É importante para não confundir o conjunto de linhas com o conjunto de resultados. O conjunto de resultados é mantido na fonte de dados, enquanto o conjunto de linhas é mantido em buffers do aplicativo. Enquanto o conjunto de resultados for corrigido, o conjunto de linhas não é: ele muda de posição e conteúdo de cada vez que um novo conjunto de linhas é buscado. Assim como um cursor de uma única linha, como os pontos de cursor de somente avanço SQL tradicionais para uma linha atual, um cursor em bloco aponta para o conjunto de linhas, que pode ser considerado como *linhas atuais*.  
  
 Para executar operações que operam em uma única linha quando várias linhas foram buscadas, o aplicativo deve indicar qual linha é a linha atual. A linha atual é necessária por chamadas para **SQLGetData** e posicionado atualizar e excluir instruções. Quando um cursor em bloco primeiro retorna um conjunto de linhas, a linha atual é a primeira linha do conjunto de linhas. Para alterar a linha atual, o aplicativo chama **SQLSetPos** ou **SQLBulkOperations** (para atualizar pelo indicador). A ilustração a seguir mostra a relação do conjunto de resultados, conjunto de linhas, a linha atual, o cursor de conjunto de linhas e cursor em bloco. Para obter mais informações, consulte [usando cursores em bloco](../../../odbc/reference/develop-app/using-block-cursors.md)mais adiante nesta seção, e [posicionado instruções Update e excluir](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) e [atualizando dados com SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
 ![Em seguida, busca prévia, primeiro e último conjuntos de linhas](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 Se um cursor é um cursor em bloco é independente de se ele é rolável. Por exemplo, a maioria do trabalho em um aplicativo de relatório é gasto recuperando e linhas de impressão. Por isso, ele será funciona de forma rápida com um somente de avanço, cursor em bloco. Ele usa um cursor somente de avanço para evitar a despesa de um cursor rolável e um cursor em bloco para reduzir o tráfego de rede.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Colunas de associação para uso com cursores em bloco](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [Usando cursores em bloco](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [Matriz de status da linha](../../../odbc/reference/develop-app/row-status-array.md)
