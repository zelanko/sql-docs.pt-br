---
title: Cursores dinâmicos ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64215cff750e39dc78ad1a695bbe553d900f4120
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52541869"
---
# <a name="odbc-dynamic-cursors"></a>Cursores dinâmicos ODBC
Um cursor dinâmico é exatamente isso: dinâmico. Ele pode detectar as alterações feitas para a associação, pedido e valores do conjunto de resultados depois que o cursor é aberto. Por exemplo, suponha que duas linhas de busca de um cursor dinâmico e o outro aplicativo, em seguida, atualiza uma dessas linhas e exclui a outra. Se o cursor dinâmico, em seguida, tenta buscar essas linhas novamente, ele não localizará a linha excluída, mas retornará os novos valores para a linha atualizada.  
  
 Cursores dinâmicos detectam todas as atualizações, exclusões e inserções, ambos seus próprios e aquelas feitas por outras pessoas. (Isso está sujeito ao isolamento de nível da transação, conforme definido pelo atributo SQL_ATTR_TXN_ISOLATION conexão.) A matriz de status de linha especificada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR reflete essas alterações e pode conter SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR, SQL_ROW_UPDATED e SQL_ROW_ADDED. Ele não pode retornar SQL_ROW_DELETED porque um cursor dinâmico não retorna linhas excluídas fora do conjunto de linhas e, portanto, não reconhece a existência da linha excluída no conjunto de resultados ou seu elemento correspondente na matriz de status de linha. SQL_ROW_ADDED é retornado somente quando uma linha é atualizada por uma chamada para **SQLSetPos**, não quando ele é atualizado por outro cursor.  
  
 Uma maneira de implementar cursores dinâmicos no banco de dados é criando um índice seletivo que define a associação e ordenação do resultado definida. Porque o índice é atualizado quando outros fazem alterações, um cursor com base em tal índice é sensível a todas as alterações. Seleção adicionais dentro do conjunto de resultados definido por este índice é possível pelo processamento ao longo do índice.  
  
 Cursores dinâmicos podem ser simulados exigindo que o conjunto de resultados a ser ordenada por uma chave exclusiva. Com a restrição, buscas são feitas, executando uma **selecionar** instrução cada vez que o cursor busca linhas. Por exemplo, suponha que o conjunto de resultados é definido por essa instrução:  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 Para buscar o próximo conjunto de linhas no conjunto de resultados, o cursor simulado define os parâmetros a seguir **selecionar** instrução para os valores da última linha do conjunto de linhas atual e então a executa:  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 Essa instrução cria um segundo conjunto de resultados, o primeiro conjunto de linhas que do qual é o próximo conjunto de linhas no conjunto de resultados original - nesse caso, o conjunto de linhas na tabela Customers. O cursor retorna este conjunto de linhas para o aplicativo.  
  
 É interessante observar que um cursor dinâmico implementado dessa maneira cria, na verdade, muitos conjuntos de resultados, que permite que ele detectar alterações ao conjunto de resultados original. O aplicativo nunca aprende da existência desses conjuntos de resultados auxiliar; ele simplesmente aparece como se o cursor é capaz de detectar alterações ao conjunto de resultados original.
