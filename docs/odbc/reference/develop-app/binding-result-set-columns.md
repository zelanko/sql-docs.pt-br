---
title: "Colunas do conjunto de resultados de associação | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 156d7a4fa40e28f2526b5ab3f5fd1a5bef19c003
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="binding-result-set-columns"></a>Colunas do conjunto de resultados de associação
Os aplicativos podem associar como muitas ou poucas colunas do conjunto de resultados como quiser, incluindo sem colunas de associação em todos os. Quando uma linha de dados for encontrada, o driver retorna os dados para as colunas associadas ao aplicativo. Se o aplicativo associa todas as colunas no conjunto de resultados depende do aplicativo. Por exemplo, aplicativos que geram relatórios geralmente têm um formato fixo; Esses aplicativos criar um conjunto de resultados que contém todas as colunas usadas no relatório e, em seguida, vincular e recuperam os dados de todas essas colunas. Aplicativos que exibem as telas de dados, às vezes, permitir que o usuário decidir quais colunas serão exibidas; Esses aplicativos criam um conjunto de resultados contendo todas as colunas, o usuário pode desejar, mas vincular e recuperar os dados somente para as colunas escolhidos pelo usuário.  
  
 Dados podem ser recuperados de colunas desassociadas chamando **SQLGetData**. Isso é geralmente chamado para recuperar dados longos, que geralmente excedem o comprimento de um único buffer e devem ser recuperados em partes.  
  
 Colunas podem ser associadas a qualquer momento, mesmo depois que linhas foram buscadas. No entanto, as novas associações não entram em vigor até a próxima vez em que uma linha é buscada; eles não são aplicados aos dados de linhas buscadas já.  
  
 Uma variável permanece associada a uma coluna até que outra variável é vinculada à coluna, até que a coluna é desassociada chamando **SQLBindCol** com um ponteiro nulo como o endereço da variável, até que todas as colunas são desassociadas chamando **SQLFreeStmt** com a opção SQL_UNBIND ou até que a instrução seja liberada. Por esse motivo, o aplicativo deve ser-se de que todas as variáveis associadas permaneçam válidas enquanto eles estão associados. Para obter mais informações, consulte [Allocating e liberar Buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Como as associações de coluna são apenas informações associadas com a estrutura da instrução, eles podem ser definidos em qualquer ordem. Eles também são independentes do conjunto de resultados. Por exemplo, suponha que um aplicativo associa as colunas do conjunto de resultados gerado pela instrução SQL a seguir:  
  
```  
SELECT * FROM Orders  
```  
  
 Se o aplicativo executa a instrução SQL  
  
```  
SELECT * FROM Lines  
```  
  
 no identificador da instrução, as associações de coluna para o primeiro conjunto de resultados ainda estão em vigor porque essas são as associações armazenadas na estrutura de instrução. Na maioria dos casos, isso é uma prática de programação ruim e deve ser evitado. Em vez disso, o aplicativo deve chamar **SQLFreeStmt** com a opção SQL_UNBIND para desassociar todas as colunas antigas e, em seguida, associar novas.
