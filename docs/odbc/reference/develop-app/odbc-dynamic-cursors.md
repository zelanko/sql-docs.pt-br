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
ms.openlocfilehash: 628de07f90de47efb0546dff84c03f56efb0674c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086299"
---
# <a name="odbc-dynamic-cursors"></a>Cursores dinâmicos ODBC
Um cursor dinâmico é apenas isso: dinâmico. Ele pode detectar quaisquer alterações feitas na associação, na ordem e nos valores do conjunto de resultados depois que o cursor for aberto. Por exemplo, suponha que um cursor dinâmico busque duas linhas e outro aplicativo então atualize uma dessas linhas e exclua a outra. Se o cursor dinâmico tentar buscar novamente essas linhas, ele não encontrará a linha excluída, mas retornará os novos valores para a linha atualizada.  
  
 Cursores dinâmicos detectam todas as atualizações, exclusões e inserções, as próprias e as feitas por outras pessoas. (Isso está sujeito ao nível de isolamento da transação, conforme definido pelo atributo de conexão SQL_ATTR_TXN_ISOLATION.) A matriz de status de linha especificada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR reflete essas alterações e pode conter SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR, SQL_ROW_UPDATED e SQL_ROW_ADDED. Ele não pode retornar SQL_ROW_DELETED porque um cursor dinâmico não retorna linhas excluídas fora do conjunto de linhas e, portanto, não reconhece mais a existência da linha excluída no conjunto de resultados ou seu elemento correspondente na matriz de status de linha. SQL_ROW_ADDED é retornado somente quando uma linha é atualizada por uma chamada para **SQLSetPos**, não quando ela é atualizada por outro cursor.  
  
 Uma maneira de implementar cursores dinâmicos no banco de dados é criar um índice seletivo que defina a associação e a ordenação do conjunto de resultados. Como o índice é atualizado quando outros fazem alterações, um cursor baseado em tal índice é sensível a todas as alterações. A seleção adicional dentro do conjunto de resultados definido por esse índice é possível pelo processamento ao longo do índice.  
  
 Cursores dinâmicos podem ser simulados exigindo que o conjunto de resultados seja ordenado por uma chave exclusiva. Com essa restrição, as buscas são feitas pela execução de uma instrução **Select** sempre que o cursor busca linhas. Por exemplo, suponha que o conjunto de resultados seja definido por esta instrução:  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 Para buscar o próximo conjunto de linhas neste conjunto de resultados, o cursor simulado define os parâmetros na instrução **Select** a seguir para os valores na última linha do conjunto de linhas atual e, em seguida, executa-o:  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 Essa instrução cria um segundo conjunto de resultados, o primeiro conjunto de linhas do qual é o próximo conjunto de linhas no conjunto de resultados original-nesse caso, o conjunto de linhas na tabela Customers. O cursor retorna esse conjunto de linhas para o aplicativo.  
  
 É interessante observar que um cursor dinâmico implementado dessa maneira realmente cria muitos conjuntos de resultados, o que permite que ele detecte alterações no conjunto de resultados original. O aplicativo nunca aprende a existência desses conjuntos de resultados auxiliares; Ele simplesmente aparece como se o cursor fosse capaz de detectar alterações no conjunto de resultados original.
