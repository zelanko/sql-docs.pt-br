---
title: Colunas de conjunto de resultados de vinculação | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 558ceb79d42d82477b70a028395de82cc023c170
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306357"
---
# <a name="binding-result-set-columns"></a>Associar colunas de conjunto de resultados
Os aplicativos podem vincular quantas ou poucas colunas do conjunto de resultados quiserem, incluindo a vinculação de nenhuma coluna. Quando uma linha de dados é buscada, o motorista retorna os dados para as colunas vinculadas ao aplicativo. Se o aplicativo vincula todas as colunas no conjunto de resultados depende do aplicativo. Por exemplo, aplicativos que geram relatórios geralmente têm um formato fixo; tais aplicativos criam um conjunto de resultados contendo todas as colunas usadas no relatório e, em seguida, vinculam e recuperam os dados de todas essas colunas. Aplicativos que exibem telas cheias de dados às vezes permitem que o usuário decida quais colunas exibir; tais aplicativos criam um conjunto de resultados contendo todas as colunas que o usuário pode querer, mas vinculam e recuperam os dados apenas para as colunas escolhidas pelo usuário.  
  
 Os dados podem ser recuperados a partir de colunas não vinculadas ligando para **SQLGetData**. Isso é comumente chamado para recuperar dados longos, que muitas vezes excedem o comprimento de um único buffer e devem ser recuperados em partes.  
  
 As colunas podem ser ligadas a qualquer momento, mesmo depois de linhas terem sido buscadas. No entanto, as novas ligações não surtem efeito até a próxima vez que uma linha for buscada; eles não são aplicados a dados de linhas já buscadas.  
  
 Uma variável permanece vinculada a uma coluna até que uma variável diferente esteja vinculada à coluna, até que a coluna seja desvinculada ligando para **SQLBindCol** com um ponteiro nulo como endereço da variável, até que todas as colunas sejam desvinculadas ligando para **SQLFreeStmt** com a opção SQL_UNBIND, ou até que a declaração seja liberada. Por essa razão, o aplicativo deve ter certeza de que todas as variáveis vinculadas permanecem válidas enquanto estiverem vinculadas. Para obter mais informações, consulte [Alocando e Liberando Buffers](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Como as vinculações da coluna são apenas informações associadas à estrutura da declaração, elas podem ser definidas em qualquer ordem. Eles também são independentes do conjunto de resultados. Por exemplo, suponha que um aplicativo vincule as colunas do conjunto de resultados gerado pela seguinte declaração SQL:  
  
```  
SELECT * FROM Orders  
```  
  
 Se o aplicativo executar a declaração SQL  
  
```  
SELECT * FROM Lines  
```  
  
 na mesma alça de declaração, as amarras da coluna para o primeiro conjunto de resultados ainda estão em vigor porque essas são as amarras armazenadas na estrutura da declaração. Na maioria dos casos, esta é uma prática de programação ruim e deve ser evitada. Em vez disso, o aplicativo deve chamar **SQLFreeStmt** com a opção SQL_UNBIND de desvincular todas as colunas antigas e, em seguida, vincular novas.
