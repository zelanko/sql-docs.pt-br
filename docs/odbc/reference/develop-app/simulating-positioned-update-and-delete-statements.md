---
title: "Simulando posicionado instruções Update e Delete | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- row identifiers [ODBC]
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: b24ed59f-f25b-4646-a135-5f3596abc1a4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 99d022dd56700a3e6441413eb43c06bc1c51cb70
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="simulating-positioned-update-and-delete-statements"></a>Simulando posicionada instruções Update e Delete
Se a fonte de dados não oferecem suporte à atualização posicionada e instruções delete, o driver pode simular a eles. Por exemplo, a biblioteca de cursores ODBC simula atualização posicionada e instruções delete. A estratégia geral para simular posicionada instruções update e delete é converter instruções posicionadas às pesquisada. Isso é feito, substituindo o **WHERE CURRENT OF** cláusula com uma pesquisa **onde** cláusula que identifica a linha atual.  
  
 Por exemplo, porque a coluna CustID identifica exclusivamente cada linha na tabela Customers, o posicionamento instrução delete  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 pode ser convertido em  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 O driver pode usar um dos seguintes *identificadores de linha* no **onde** cláusula:  
  
-   Colunas cujos valores servem para identificar exclusivamente cada linha na tabela. Por exemplo, chamar **SQLSpecialColumns** com SQL_BEST_ROWID retorna a coluna ou conjunto ideal de colunas que servem para essa finalidade.  
  
-   Pseudo colunas, fornecidas por algumas fontes de dados, com a finalidade de identificar exclusivamente cada linha. Eles também podem ser recuperáveis chamando **SQLSpecialColumns**.  
  
-   Um índice exclusivo, se disponível.  
  
-   Todas as colunas no conjunto de resultados.  
  
 Exatamente quais colunas de um driver deve usar o **onde** cláusula ele constrói depende do driver. Em alguns dados de fontes, determinar um identificador de linha podem ser dispendiosas. No entanto, ele é mais rápido executar e garante que uma instrução simulada atualiza ou exclui no máximo uma linha. Dependendo dos recursos do DBMS subjacente, usar um identificador de linha pode ser caro para configurar. No entanto, ele é mais rápido executar e garante que uma instrução simulada irá atualizar ou excluir apenas uma linha. A opção de usar todas as colunas no conjunto de resultados é geralmente mais fácil configurar. No entanto, é mais lento executar e, se as colunas não identificar exclusivamente uma linha, pode resultar em linhas atualizadas ou excluídas acidentalmente, especialmente quando define a lista de seleção para o resultado não contém todas as colunas existentes na tabela subjacente.  
  
 Dependendo de qual das estratégias acima o driver dá suporte a, um aplicativo pode escolher qual estratégia de que deseja que o driver para uso com o atributo de instrução SQL_ATTR_SIMULATE_CURSOR. Embora possa parecer estranho para um aplicativo de risco, inadvertidamente, atualizar ou excluir uma linha, o aplicativo pode remover esse risco, garantindo que as colunas no conjunto de resultados identificam exclusivamente cada linha no conjunto de resultados. Isso economiza o driver de esforço fazer isso.  
  
 Se o driver opta por usar um identificador de linha, ele intercepta a **SELECT FOR UPDATE** instrução que cria o conjunto de resultados. Se as colunas na lista de seleção não identificar efetivamente uma linha, o driver adiciona as colunas necessárias ao final da lista de seleção. Algumas fontes de dados tem uma única coluna que sempre identifica uma linha, como a coluna ROWID no Oracle; Se essa coluna estiver disponível, o driver usa esse. Caso contrário, o driver chama **SQLSpecialColumns** para cada tabela no **FROM** cláusula para recuperar uma lista das colunas que identificam exclusivamente cada linha. Uma restrição comum que resulta dessa técnica é que a simulação de cursor falha se houver mais de uma tabela no **FROM** cláusula.  
  
 Independentemente de como o driver identifica linhas, ele extrai geralmente o **para atualização de** cláusula desativar o **SELECT FOR UPDATE** instrução antes de enviá-la para a fonte de dados. O **para atualizar de** cláusula é usada apenas com posicionado atualização e instruções delete. Fontes de dados que não oferecem suporte a posicionado atualização e instruções delete geralmente não oferecem suporte a ele.  
  
 Quando o aplicativo envia uma atualização posicionada ou uma instrução delete para execução, o driver substitui o **WHERE CURRENT OF** cláusula com um **onde** cláusula que contém o identificador de linha. Os valores dessas colunas são recuperados de um cache mantido pelo driver para cada coluna, ele usa o **onde** cláusula. Depois que o driver substituiu o **onde** cláusula, ele envia a instrução para a fonte de dados para execução.  
  
 Por exemplo, suponha que o aplicativo envia a instrução a seguir para criar um conjunto de resultados:  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 Se o aplicativo definiu SQL_ATTR_SIMULATE_CURSOR para solicitar uma garantia de exclusividade e se a fonte de dados não fornecer uma coluna pseudo que sempre identifica uma linha, o driver chama **SQLSpecialColumns** para o Tabela de clientes, descobre CustID é a chave para a tabela Customers e adiciona esse à lista de seleção e extrai o **para atualização de** cláusula:  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 Se o aplicativo não solicitou uma garantia de exclusividade, o driver remove apenas o **para atualização de** cláusula:  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 Suponha que o aplicativo percorre o conjunto de resultados e envia a seguinte instrução de atualização posicionada para execução, onde Cust é o nome do cursor sobre o conjunto de resultados:  
  
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

