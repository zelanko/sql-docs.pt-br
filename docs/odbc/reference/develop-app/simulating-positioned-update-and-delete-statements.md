---
title: Simulando declarações de atualização posicionada e exclusão | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301987"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>Simular instruções de exclusão e atualização posicionadas
Se a fonte de dados não suportar instruções de atualização posicionadas e exclusão, o driver poderá simulá-las. Por exemplo, a biblioteca do cursor ODBC simula atualizações posicionadas e excluem instruções. A estratégia geral para simular instruções de atualização posicionadas e exclusão é converter declarações posicionadas para as pesquisadas. Isso é feito substituindo a cláusula **WHERE CURRENT OF** por uma cláusula **PESQUISADA WHERE** que identifica a linha atual.  
  
 Por exemplo, como a coluna CustID identifica exclusivamente cada linha na tabela Clientes, a declaração de exclusão posicionada  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 pode ser convertido para  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 O driver pode usar um dos *seguintes identificadores* de linha na cláusula **WHERE:**  
  
-   Colunas cujos valores servem para identificar exclusivamente cada linha na tabela. Por exemplo, chamar **SQLSpecialColumns** com SQL_BEST_ROWID retorna a coluna ideal ou conjunto de colunas que servem a esse propósito.  
  
-   Pseudo-colunas, fornecidas por algumas fontes de dados, com o propósito de identificar exclusivamente cada linha. Estes também podem ser recuperáveis chamando **SQLSpecialColumns**.  
  
-   Um índice único, se disponível.  
  
-   Todas as colunas no conjunto de resultados.  
  
 Exatamente quais colunas um motorista deve usar na cláusula **WHERE** que ele constrói depende do motorista. Em algumas fontes de dados, determinar um identificador de linha pode ser caro. No entanto, é mais rápido para executar e garante que uma declaração simulada atualiza ou exclui no máximo uma linha. Dependendo das capacidades do DBMS subjacente, usar um identificador de linha pode ser caro de configurar. No entanto, é mais rápido para executar e garante que uma declaração simulada atualizará ou excluirá apenas uma linha. A opção de usar todas as colunas no conjunto de resultados geralmente é muito mais fácil de configurar. No entanto, é mais lento para executar e, se as colunas não identificarem uma linha exclusivamente, pode resultar em linhas sendo atualizadas ou excluídas involuntariamente, especialmente quando a lista de seleção para o conjunto de resultados não contém todas as colunas existentes na tabela subjacente.  
  
 Dependendo de qual das estratégias anteriores o motorista suporta, um aplicativo pode escolher qual estratégia deseja que o motorista use com o atributo de declaração SQL_ATTR_SIMULATE_CURSOR. Embora possa parecer estranho para um aplicativo correr o risco de atualizar ou excluir uma linha sem querer, o aplicativo pode remover esse risco, garantindo que as colunas no conjunto de resultados identifiquem com exclusividade cada linha no conjunto de resultados. Isso poupa o motorista do esforço de ter que fazer isso.  
  
 Se o driver optar por usar um identificador de linha, ele interceptará a declaração **SELECT FOR UPDATE** que cria o conjunto de resultados. Se as colunas na lista de seleção não identificarem efetivamente uma linha, o driver adicionará as colunas necessárias ao final da lista de seleção. Algumas fontes de dados têm uma única coluna que sempre identifica uma linha com exclusividade, como a coluna ROWID no Oracle; se tal coluna estiver disponível, o driver usa isso. Caso contrário, o driver chama **SQLSpecialColumns** para cada tabela na cláusula **FROM** para recuperar uma lista das colunas que identificam exclusivamente cada linha. Uma restrição comum que resulta dessa técnica é que a simulação do cursor falha se houver mais de uma tabela na cláusula **DE.**  
  
 Não importa como o driver identifica linhas, ele geralmente tira a cláusula **FOR UPDATE OF** da declaração SELECT FOR **UPDATE** antes de enviá-la para a fonte de dados. A **cláusula FOR UPDATE OF** é usada apenas com instruções de atualização e exclusão posicionadas. Fontes de dados que não suportam instruções de atualização posicionadas e excluem declarações geralmente não suportam isso.  
  
 Quando o aplicativo envia uma declaração de atualização posicionada ou exclusão para execução, o driver substitui a cláusula **WHERE CURRENT OF** por uma cláusula **WHERE** contendo o identificador de linha. Os valores dessas colunas são recuperados de um cache mantido pelo driver para cada coluna que ele usa na cláusula **WHERE.** Após o driver ter substituído a cláusula **WHERE,** ele envia a declaração para a fonte de dados para execução.  
  
 Por exemplo, suponha que o aplicativo envie a seguinte declaração para criar um conjunto de resultados:  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 Se o aplicativo tiver definido SQL_ATTR_SIMULATE_CURSOR para solicitar uma garantia de exclusividade e se a fonte de dados não fornecer uma pseudo-coluna que sempre identifica uma linha, o driver chama **SQLSpecialColumns** para a tabela Clientes, descobre que custID é a chave da tabela Clientes e adiciona isso à lista de seleção e tira a cláusula **PARA ATUALIZAÇÃO DA** TABELA:  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 Se o aplicativo não tiver solicitado uma garantia de exclusividade, o driver tira apenas a **cláusula PARA ATUALIZAÇÃO DA** CLÁUSULA:  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 Suponha que o aplicativo role o conjunto de resultados e envie a seguinte declaração de atualização posicionada para execução, onde Cust é o nome do cursor sobre o conjunto de resultados:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 Se o aplicativo não tiver solicitado uma garantia de exclusividade, o driver substitui a cláusula **WHERE** e vincula o parâmetro CustID à variável em seu cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 Se o aplicativo não tiver solicitado uma garantia de exclusividade, o motorista substitui a cláusula **WHERE** e vincula os parâmetros Nome, Endereço e Telefone nesta cláusula às variáveis em seu cache:  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
