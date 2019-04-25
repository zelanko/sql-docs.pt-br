---
title: Simulando posicionado instruções Update e Delete | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d98d40ae24c68f90a304edb0293febfe76fac2c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62445888"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>Simular instruções de exclusão e atualização posicionadas
Se a fonte de dados não dão suporte à atualização posicionada e instruções delete, o driver pode simular a eles. Por exemplo, a biblioteca de cursores ODBC simula atualização posicionadas e instruções delete. A estratégia geral para simular as instruções de exclusão e atualização posicionadas é converter as instruções posicionadas para aqueles pesquisada. Isso é feito substituindo o **WHERE CURRENT OF** cláusula com um pesquisada **onde** cláusula que identifica a linha atual.  
  
 Por exemplo, porque a coluna CustID identifica exclusivamente cada linha na tabela Customers, o posicionadas instrução delete  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 pode ser convertido em  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 O driver pode usar um dos seguintes *identificadores de linha* na **onde** cláusula:  
  
-   Colunas cujos valores servem para identificar exclusivamente cada linha na tabela. Por exemplo, chamar **SQLSpecialColumns** com SQL_BEST_ROWID retorna a coluna ou conjunto ideal de colunas que servem para essa finalidade.  
  
-   Colunas pseudo fornecidas por fontes de dados, para fins de identificação exclusivamente cada linha. Eles também podem ser recuperáveis, chamando **SQLSpecialColumns**.  
  
-   Um índice exclusivo, se disponível.  
  
-   Todas as colunas no conjunto de resultados.  
  
 Exatamente quais colunas deve ser usar um driver na **onde** cláusula ele constrói depende do driver. Em alguns dados, fontes, determinando um identificador de linha podem ser dispendiosas. No entanto, ele é executado mais rápido e garante que uma instrução simulada atualiza ou exclui no máximo uma linha. Dependendo dos recursos do DBMS subjacente, usar um identificador de linha pode ser caro para configurar. No entanto, ele é executado mais rápido e garante que uma instrução simulada irá atualizar ou excluir apenas uma linha. A opção de usar todas as colunas no conjunto de resultados é geralmente muito mais fácil de configurar. No entanto, é mais lento executar e, se as colunas não identificar exclusivamente uma linha, pode resultar em linhas que estão sendo atualizados ou excluídos acidentalmente, especialmente quando a lista de seleção para o resultado definido não contém todas as colunas que existem na tabela subjacente.  
  
 Dependendo de qual das estratégias acima o driver dá suporte a, um aplicativo pode escolher qual estratégia que ele deseja que o driver a ser usado com o atributo de instrução SQL_ATTR_SIMULATE_CURSOR. Embora possa parecer estranho para um aplicativo de risco, inadvertidamente, atualizar ou excluir uma linha, o aplicativo pode remover esse risco, garantindo que as colunas no conjunto de resultados identificam exclusivamente cada linha no conjunto de resultados. Isso economiza o driver o esforço fazer isso.  
  
 Se o driver optar por usar um identificador de linha, ele intercepta a **SELECT FOR UPDATE** instrução que cria o conjunto de resultados. Se as colunas na lista de seleção não identificar com eficiência uma linha, o driver adiciona as colunas necessárias ao final da lista de seleção. Algumas fontes de dados tem uma única coluna que sempre identifica uma linha, como a coluna ROWID no Oracle; Se uma coluna desse tipo estiver disponível, o driver usa isso. Caso contrário, o driver chama **SQLSpecialColumns** para cada tabela na **FROM** cláusula para recuperar uma lista das colunas que identificam exclusivamente cada linha. Uma restrição comum que é o resultado dessa técnica é que a simulação de cursor falha se não houver mais de uma tabela na **FROM** cláusula.  
  
 Não importa como o driver identifica linhas, ela geralmente retira o **FOR UPDATE OF** cláusula desativado o **SELECT FOR UPDATE** instrução antes de enviá-la para a fonte de dados. O **para atualizar de** cláusula é usada apenas com posicionada atualizar e excluir instruções. Fontes de dados que não dão suporte a posicionado update e delete instruções geralmente não dão suporte a ele.  
  
 Quando o aplicativo envia uma atualização posicionada ou uma instrução delete para execução, o driver substitui o **WHERE CURRENT OF** cláusula com um **onde** cláusula que contém o identificador de linha. Os valores dessas colunas são recuperados de um cache mantido pelo driver para cada coluna que ele usa o **onde** cláusula. Depois que o driver substituiu o **onde** cláusula, ele envia a instrução para a fonte de dados para execução.  
  
 Por exemplo, suponha que o aplicativo envia a instrução a seguir para criar um conjunto de resultados:  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 Se o aplicativo definiu SQL_ATTR_SIMULATE_CURSOR para solicitar uma garantia de exclusividade e se a fonte de dados não fornecer uma coluna de pseudo que sempre identifica uma linha, o driver chama **SQLSpecialColumns** para o Tabela de clientes, descobre que CustID é a chave para a tabela Customers e adiciona isso à lista de seleção e retira a **FOR UPDATE OF** cláusula:  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 Se o aplicativo não solicitou uma garantia de exclusividade, o driver remove apenas o **FOR UPDATE OF** cláusula:  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 Suponha que o aplicativo percorre o conjunto de resultados e envia a seguinte instrução de atualização posicionada para execução, onde o Cust é o nome do cursor sobre o conjunto de resultados:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 Se o aplicativo não solicitou uma garantia de exclusividade, o driver substitui o **onde** cláusula e associa o parâmetro CustID à variável em seu cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 Se o aplicativo não solicitou uma garantia de exclusividade, o driver substitui o **onde** cláusula e associa os parâmetros de nome, endereço e telefone esta cláusula para as variáveis em seu cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
