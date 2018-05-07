---
title: Cursores dinâmicos ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], dynamic
- dynamic cursors [ODBC]
ms.assetid: de709fd3-9eb2-44e1-a2f0-786e2b9602a6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 706bf3a92122e025977d092c06668fc646f2b6e8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-dynamic-cursors"></a>Cursores dinâmicos do ODBC
Um cursor dinâmico é exatamente isso: dinâmico. Ele pode detectar todas as alterações feitas a associação, ordem e os valores do conjunto de resultados depois que o cursor é aberto. Por exemplo, suponha que duas linhas de busca de um cursor dinâmico e outro aplicativo, em seguida, atualiza uma dessas linhas e exclui a outra. Se o cursor dinâmico, em seguida, tenta buscar essas linhas novamente, ele não localizará a linha excluída, mas retornará os novos valores para a linha atualizada.  
  
 Cursores dinâmicos detectam todas as atualizações, exclusões e inserções, ambos seus próprios e as alterações feitas por outras pessoas. (Isso é sujeito o isolamento nível da transação, conforme definido pelo atributo de conexão SQL_ATTR_TXN_ISOLATION.) A matriz de status de linha especificada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR reflete as alterações e pode conter SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR, SQL_ROW_UPDATED e SQL_ROW_ADDED. Ele não pode retornar SQL_ROW_DELETED porque um cursor dinâmico não retorna linhas excluídas fora do conjunto de linhas e, portanto, não reconhece a existência de seu elemento correspondente na matriz de status de linha ou a linha excluída no conjunto de resultados. SQL_ROW_ADDED é retornado somente quando uma linha é atualizada por uma chamada para **SQLSetPos**, não quando ele é atualizado por outro cursor.  
  
 Uma maneira de implementar os cursores dinâmicos no banco de dados é criando um índice seletivo que define a associação e a ordenação do resultado definida. Porque o índice é atualizado quando outros fazem alterações, um cursor com base em um índice é sensível à todas as alterações. Seleção adicionais no conjunto de resultados definido por esse índice é possível pelo processamento ao longo do índice.  
  
 Cursores dinâmicos podem ser simulados exigindo que o conjunto de resultados a ser ordenada por uma chave exclusiva. Com a restrição, buscas são feitas executando um **selecione** instrução cada vez que o cursor busca linhas. Por exemplo, suponha que o conjunto de resultados é definido por essa instrução:  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 Para buscar o próximo conjunto de linhas no conjunto de resultados, o cursor simulado define os parâmetros a seguir **selecione** instrução para os valores da última linha do conjunto de linhas atual e então a executa:  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 Essa instrução cria um segundo conjunto de resultados, o primeiro conjunto de linhas do que é o próximo conjunto de linhas no conjunto de resultados original — nesse caso, o conjunto de linhas na tabela Customers. O cursor retorna este conjunto de linhas para o aplicativo.  
  
 É interessante observar que um cursor dinâmico implementado dessa maneira cria vários conjuntos de resultados, que permite que ele detectar alterações ao conjunto de resultados original. O aplicativo nunca aprende da existência desses conjuntos de resultados auxiliar; ele simplesmente aparece como se o cursor é capaz de detectar alterações ao conjunto de resultados original.
