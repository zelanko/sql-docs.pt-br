---
title: Dados retornados por funções de catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14499071bd180a7ea709fda3eb26aeae46f229c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077020"
---
# <a name="data-returned-by-catalog-functions"></a>Dados retornados pelas funções de catálogo
Cada função de catálogo retorna dados como um conjunto de resultados. Esse conjunto de resultados não é diferente de nenhum outro conjunto de resultados. Normalmente, ele é gerado por uma instrução **Select** parametrizada predefinida que é embutida em código no driver ou armazenada em um procedimento na fonte de dados. Para obter informações sobre como recuperar dados de um conjunto de resultados, consulte [foi um conjunto de resultados criado?](../../../odbc/reference/develop-app/was-a-result-set-created.md).  
  
 O conjunto de resultados para cada função de catálogo é descrito na entrada de referência para essa função. Além das colunas listadas, o conjunto de resultados pode conter colunas específicas do driver após a última coluna predefinida. Essas colunas (se houver) são descritas na documentação do driver.  
  
 Os aplicativos devem associar colunas específicas do driver em relação ao final do conjunto de resultados. Ou seja, eles devem calcular o número de uma coluna específica do driver como o número da última coluna recuperada com **SQLNumResultCols** o número de colunas que ocorrem após a coluna necessária. Isso economiza ter de alterar o aplicativo quando novas colunas são adicionadas ao conjunto de resultados em versões futuras do ODBC ou do driver. Para que esse esquema funcione, os drivers devem adicionar novas colunas específicas de driver antes de colunas antigas de driver antigo, de modo que os números de coluna não sejam alterados em relação ao final do conjunto de resultados.  
  
 Os identificadores que são retornados no conjunto de resultados não são colocados entre aspas, mesmo que contenham caracteres especiais. Por exemplo, suponha que o caractere de aspas de identificador (que é específico de driver e retornado por meio de **SQLGetInfo**) seja uma aspa dupla (") e a tabela contas a pagar contenha uma coluna denominada nome do cliente. Na linha retornada por **SQLColumns** para essa coluna, o valor da coluna TABLE_NAME é contas a pagar, não "contas a pagar", e o valor da coluna column_name é nome do cliente, não "nome do cliente". Para recuperar os nomes de clientes na tabela contas a pagar, o aplicativo citaria esses nomes:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 Para obter mais informações, consulte [identificadores entre aspas](../../../odbc/reference/develop-app/quoted-identifiers.md).  
  
 As funções de catálogo são baseadas em um modelo de autorização do tipo SQL no qual uma conexão é feita com base em um nome de usuário e senha, e somente os dados para os quais o usuário tem um privilégio são retornados. A proteção por senha de arquivos individuais, que não se ajustam a esse modelo, é definida pelo driver.  
  
 Os conjuntos de resultados retornados pelas funções de catálogo quase nunca são atualizáveis, e os aplicativos não devem esperar ser capazes de alterar a estrutura do banco de dados alterando-os nesses conjuntos de resultados.
