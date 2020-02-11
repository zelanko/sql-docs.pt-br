---
title: Vinculando colunas do conjunto de resultados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: becda51a0fac924fce31e6cb15331321990d8a42
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68134998"
---
# <a name="binding-result-set-columns"></a>Associar colunas de conjunto de resultados
Os aplicativos podem associar tantas ou poucas colunas do conjunto de resultados que escolherem, incluindo a associação de nenhuma coluna. Quando uma linha de dados é buscada, o driver retorna os dados para as colunas associadas ao aplicativo. Se o aplicativo associa todas as colunas no conjunto de resultados depende do aplicativo. Por exemplo, os aplicativos que geram relatórios geralmente têm um formato fixo; esses aplicativos criam um conjunto de resultados contendo todas as colunas usadas no relatório e, em seguida, associam e recuperam os dados para todas essas colunas. Os aplicativos que exibem telas cheia de dados às vezes permitem que o usuário decida quais colunas exibir; esses aplicativos criam um conjunto de resultados contendo todas as colunas que o usuário pode querer, mas associam e recuperam os dados somente para as colunas escolhidas pelo usuário.  
  
 Os dados podem ser recuperados de colunas desassociadas chamando **SQLGetData**. Isso é normalmente chamado para recuperar dados longos, que geralmente excedem o comprimento de um único buffer e devem ser recuperados em partes.  
  
 As colunas podem ser associadas a qualquer momento, mesmo depois que as linhas forem buscadas. No entanto, as novas associações não entram em vigor até a próxima vez que uma linha for buscada; Eles não são aplicados a dados de linhas já buscadas.  
  
 Uma variável permanece associada a uma coluna até que uma variável diferente seja associada à coluna, até que a coluna seja desassociada chamando **SQLBindCol** com um ponteiro nulo como o endereço da variável, até que todas as colunas sejam desassociadas chamando **SQLFreeStmt** com a opção SQL_UNBIND ou até que a instrução seja liberada. Por esse motivo, o aplicativo deve ter certeza de que todas as variáveis associadas permanecem válidas desde que estejam associadas. Para obter mais informações, consulte [alocando e liberando buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Como as associações de coluna são apenas informações associadas à estrutura da instrução, elas podem ser definidas em qualquer ordem. Eles também são independentes do conjunto de resultados. Por exemplo, suponha que um aplicativo associe as colunas do conjunto de resultados gerado pela seguinte instrução SQL:  
  
```  
SELECT * FROM Orders  
```  
  
 Se o aplicativo executar a instrução SQL novamente  
  
```  
SELECT * FROM Lines  
```  
  
 no mesmo identificador de instrução, as associações de coluna para o primeiro conjunto de resultados ainda estão em vigor porque essas são as associações armazenadas na estrutura da instrução. Na maioria dos casos, essa é uma prática de programação ruim e deve ser evitada. Em vez disso, o aplicativo deve chamar **SQLFreeStmt** com a opção SQL_UNBIND para desassociar todas as colunas antigas e, em seguida, associar as novas.
