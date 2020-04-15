---
title: Cursors Dinâmicos ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], dynamic
- dynamic cursors [ODBC]
ms.assetid: de709fd3-9eb2-44e1-a2f0-786e2b9602a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f94b83ef1458cd9f8368d1bea3a39682bd80b1a2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302318"
---
# <a name="odbc-dynamic-cursors"></a>Cursores dinâmicos ODBC
Um cursor dinâmico é exatamente isso: dinâmico. Ele pode detectar quaisquer alterações feitas na adesão, ordem e valores do resultado definido após a abertura do cursor. Por exemplo, suponha que um cursor dinâmico busque duas linhas e outro aplicativo então atualize uma dessas linhas e exclua a outra. Se o cursor dinâmico tentar rebuscar essas linhas, ele não encontrará a linha excluída, mas retornará os novos valores para a linha atualizada.  
  
 Os cursores dinâmicos detectam todas as atualizações, exclusões e inserções, tanto suas próprias quanto as feitas por outros. (Isso está sujeito ao nível de isolamento da transação, conforme definido pelo atributo de conexão SQL_ATTR_TXN_ISOLATION.) A matriz de status de linha especificada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR reflete essas alterações e pode conter SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR, SQL_ROW_UPDATED e SQL_ROW_ADDED. Ele não pode retornar SQL_ROW_DELETED porque um cursor dinâmico não retorna linhas excluídas fora do conjunto de linhas e, portanto, não reconhece mais a existência da linha excluída no conjunto de resultados ou seu elemento correspondente na matriz de status da linha. SQL_ROW_ADDED é retornado somente quando uma linha é atualizada por uma chamada para **SQLSetPos**, não quando é atualizada por outro cursor.  
  
 Uma forma de implementar cursores dinâmicos no banco de dados é criando um índice seletivo que define a adesão e a ordenação do conjunto de resultados. Como o índice é atualizado quando outros fazem alterações, um cursor baseado em tal índice é sensível a todas as alterações. A seleção adicional dentro do conjunto de resultados definido por este índice é possível processando ao longo do índice.  
  
 Os cursores dinâmicos podem ser simulados exigindo que o conjunto de resultados seja ordenado por uma chave única. Com tal restrição, os buscarsão são feitos executando uma declaração **SELECT** cada vez que o cursor busca linhas. Por exemplo, suponha que o conjunto de resultados seja definido por esta declaração:  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 Para buscar o próximo conjunto de linhas neste conjunto de resultados, o cursor simulado define os parâmetros na seguinte declaração **SELECT** para os valores na última linha do conjunto de linhas atual e, em seguida, executa-o:  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 Esta declaração cria um segundo conjunto de resultados, o primeiro conjunto de linhas é o próximo conjunto de linhas no conjunto de resultados original - neste caso, o conjunto de linhas na tabela Clientes. O cursor retorna este conjunto de linhas para o aplicativo.  
  
 É interessante notar que um cursor dinâmico implementado dessa forma realmente cria muitos conjuntos de resultados, o que permite detectar alterações no conjunto de resultados original. A aplicação nunca fica sabeda da existência desses conjuntos de resultados auxiliares; ele simplesmente aparece como se o cursor é capaz de detectar alterações no conjunto de resultados originais.
