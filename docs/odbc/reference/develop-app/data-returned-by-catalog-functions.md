---
title: "Dados retornados pelas funções de catálogo | Microsoft Docs"
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
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b05067010701d1751056cb99089708b5cbeb67f9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="data-returned-by-catalog-functions"></a>Dados retornados pelas funções de catálogo
Cada função de catálogo retorna dados como um conjunto de resultados. Esse conjunto de resultados não é diferente de qualquer outro conjunto de resultados. Geralmente é gerado por um predefinidas com parâmetros **selecione** instrução que é armazenado em um procedimento na fonte de dados ou embutido no driver. Para obter informações sobre como recuperar dados de um conjunto de resultados, consulte [foi um resultado definido criado?](../../../odbc/reference/develop-app/was-a-result-set-created.md).  
  
 O conjunto de resultados para cada função de catálogo é descrito na entrada de referência para essa função. Além das colunas listadas, o conjunto de resultados pode conter colunas específicas do driver após a última coluna predefinida. Essas colunas (se houver) são descritas na documentação do driver.  
  
 Os aplicativos devem associar colunas específicas do driver em relação ao final do conjunto de resultados. Ou seja, eles devem calcular o número de uma coluna específica do driver como o número da última coluna — recuperados com **SQLNumResultCols** — menos o número de colunas que ocorrem após a coluna necessária. Isso economiza precisar alterar o aplicativo quando novas colunas são adicionadas ao resultado definido em futuras versões do ODBC ou o driver. Este esquema trabalhar, drivers devem adicionar novas colunas específicas do driver antes das colunas específicas do driver antigas para que os números da coluna não são alterados em relação ao final do conjunto de resultados.  
  
 Os identificadores que são retornados no conjunto de resultados não estão entre aspas, mesmo se eles contiverem caracteres especiais. Por exemplo, suponha que o identificador de caractere de aspas (que é específico do driver e retornado por meio de **SQLGetInfo**) é uma aspas duplas (") e a tabela de contas a pagar contém uma coluna chamada Customer Name. Na linha retornada por **SQLColumns** para esta coluna, o valor da coluna TABLE_NAME é contas a pagar, não "contas a pagar", e o valor da coluna Nome da coluna é o nome do cliente, não "Customer Name". Para recuperar os nomes dos clientes na tabela de contas a pagar, o aplicativo deve colocar entre aspas esses nomes:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 Para obter mais informações, consulte [identificadores entre aspas](../../../odbc/reference/develop-app/quoted-identifiers.md).  
  
 As funções de catálogo são com base em um modelo de autorização do tipo SQL na qual uma conexão é feita com base em um nome de usuário e senha, e apenas os dados para o qual o usuário tem um privilégio são retornados. Proteção por senha de arquivos individuais, que não se ajustem a esse modelo, é definido pelo driver.  
  
 Os conjuntos de resultados retornados pelas funções de catálogo quase nunca são atualizáveis e aplicativos não devem esperar poder alterar a estrutura do banco de dados, alterando os dados nesses conjuntos de resultados.
