---
title: Simulando instruções UPDATE e DELETE posicionadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- row identifiers [ODBC]
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: b24ed59f-f25b-4646-a135-5f3596abc1a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1eb498a99180d145147e67c8955eeb7a0027024
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301987"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>Simular instruções de exclusão e atualização posicionadas
Se a fonte de dados não oferecer suporte a instruções UPDATE e DELETE posicionadas, o driver poderá simular isso. Por exemplo, a biblioteca de cursores ODBC simula as instruções UPDATE e DELETE posicionadas. A estratégia geral para simular as instruções UPDATE e DELETE posicionadas é converter instruções posicionadas em itens pesquisados. Isso é feito substituindo a cláusula **Where Current of** por uma cláusula **Where** pesquisada que identifica a linha atual.  
  
 Por exemplo, como a coluna CustID identifica exclusivamente cada linha na tabela Customers, a instrução DELETE posicionada  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 pode ser convertido em  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 O driver pode usar um dos seguintes *identificadores de linha* na cláusula **Where** :  
  
-   Colunas cujos valores servem para identificar exclusivamente cada linha na tabela. Por exemplo, chamar **SQLSpecialColumns** com SQL_BEST_ROWID retorna a coluna ou conjunto de colunas ideal que atende a essa finalidade.  
  
-   Pseudo colunas, fornecidas por algumas fontes de dados, com a finalidade de identificar exclusivamente cada linha. Eles também podem ser recuperáveis chamando **SQLSpecialColumns**.  
  
-   Um índice exclusivo, se disponível.  
  
-   Todas as colunas no conjunto de resultados.  
  
 Exatamente quais colunas um driver deve usar na cláusula **Where** que ele constrói depende do driver. Em algumas fontes de dados, determinar um identificador de linha pode ser dispendioso. No entanto, é mais rápido executar e garantir que uma instrução simulada atualize ou exclua no máximo uma linha. Dependendo dos recursos do DBMS subjacente, o uso de um identificador de linha pode ser caro para configurar. No entanto, é mais rápido executar e garantir que uma instrução simulada atualizará ou excluirá apenas uma linha. A opção de usar todas as colunas no conjunto de resultados geralmente é muito mais fácil de configurar. No entanto, é mais lento executar e, se as colunas não identificarem uma linha exclusivamente, podem resultar em linhas sendo atualizadas ou excluídas não intencionalmente, especialmente quando a lista de seleção do conjunto de resultados não contiver todas as colunas existentes na tabela subjacente.  
  
 Dependendo de quais das estratégias anteriores o driver dá suporte, um aplicativo pode escolher qual estratégia ele deseja que o Driver use com o atributo instrução SQL_ATTR_SIMULATE_CURSOR. Embora possa parecer estranho que um aplicativo seja arriscado a atualizar ou excluir uma linha de forma não intencional, o aplicativo pode remover esse risco, garantindo que as colunas no conjunto de resultados identifiquem exclusivamente cada linha no conjunto de resultados. Isso economiza o driver ao esforço de ter que fazer isso.  
  
 Se o driver optar por usar um identificador de linha, ele interceptará a instrução **SELECT for Update** que cria o conjunto de resultados. Se as colunas na lista de seleção não identificarem efetivamente uma linha, o driver adicionará as colunas necessárias ao final da lista de seleção. Algumas fontes de dados têm uma única coluna que identifica sempre uma linha exclusivamente, como a coluna de ROWID no Oracle; Se essa coluna estiver disponível, o driver o usará. Caso contrário, o driver chama **SQLSpecialColumns** para cada tabela na cláusula **from** para recuperar uma lista das colunas que identificam exclusivamente cada linha. Uma restrição comum resultante dessa técnica é que a simulação de cursor falhará se houver mais de uma tabela na cláusula **from** .  
  
 Não importa como o driver identifica as linhas, ele normalmente retira a cláusula **for Update of para** fora da instrução **SELECT for Update** antes de enviá-la à fonte de dados. A cláusula **for Update of** é usada somente com instruções UPDATE e DELETE posicionadas. As fontes de dados que não dão suporte a instruções UPDATE e DELETE posicionadas geralmente não dão suporte a ela.  
  
 Quando o aplicativo envia uma instrução UPDATE ou DELETE posicionada para execução, o driver substitui a cláusula **Where Current of** por uma cláusula **Where** que contém o identificador de linha. Os valores dessas colunas são recuperados de um cache mantido pelo driver para cada coluna usada na cláusula **Where** . Depois que o driver substituiu a cláusula **Where** , ele envia a instrução para a fonte de dados para execução.  
  
 Por exemplo, suponha que o aplicativo envie a seguinte instrução para criar um conjunto de resultados:  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 Se o aplicativo tiver definido SQL_ATTR_SIMULATE_CURSOR para solicitar uma garantia de exclusividade e se a fonte de dados não fornecer uma pseudoclasse que sempre identifica exclusivamente uma linha, o driver chamará **SQLSpecialColumns** para a tabela Customers, descobrirá que CustID é a chave para a tabela Customers e a adicionará à lista Select e revelará o **para atualização da** cláusula:  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 Se o aplicativo não tiver solicitado uma garantia de exclusividade, o driver retirará apenas a **para a atualização da** cláusula:  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 Suponha que o aplicativo Percorra o conjunto de resultados e envie a seguinte instrução de atualização posicionada para execução, em que cust é o nome do cursor sobre o conjunto de resultados:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 Se o aplicativo não tiver solicitado uma garantia de exclusividade, o driver substituirá a cláusula **Where** e associará o parâmetro CustID à variável em seu cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 Se o aplicativo não tiver solicitado uma garantia de exclusividade, o driver substituirá a cláusula **Where** e associará os parâmetros Name, address e Phone nesta cláusula às variáveis em seu cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
