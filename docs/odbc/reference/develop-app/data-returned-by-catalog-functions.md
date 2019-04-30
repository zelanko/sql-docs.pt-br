---
title: Dados retornados pelas funções de catálogo | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 10e3726d26e03da2f9f731babc105244dbf1ff05
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267724"
---
# <a name="data-returned-by-catalog-functions"></a>Dados retornados pelas funções de catálogo
Cada função de catálogo retorna dados como um conjunto de resultados. Esse conjunto de resultados não é diferente de qualquer outro conjunto de resultados. Geralmente, é gerado por um modelo predefinido, parametrizadas **selecionar** instrução que é armazenado em um procedimento na fonte de dados ou embutido no driver. Para obter informações sobre como recuperar dados de um conjunto de resultados, consulte [foi um resultado definido criado?](../../../odbc/reference/develop-app/was-a-result-set-created.md).  
  
 Conjunto de resultados para cada função de catálogo é descrito na entrada de referência para a função. Além das colunas listadas, o conjunto de resultados pode conter colunas específicas do driver depois da última coluna predefinida. Essas colunas (se houver) são descritas na documentação do driver.  
  
 Os aplicativos devem associar colunas específicas do driver em relação ao final do conjunto de resultados. Ou seja, eles devem calcular o número de uma coluna específica do driver como o número da última coluna - recuperado com **SQLNumResultCols** – menos o número de colunas que ocorrem após a coluna necessária. Isso economiza ter que alterar o aplicativo quando novas colunas são adicionadas ao resultado definido em futuras versões do ODBC ou o driver. Para este esquema trabalhar, drivers devem adicionar novas colunas específicas do driver antes de colunas antigas de específicos de driver para que os números da coluna não são alterados em relação ao final do conjunto de resultados.  
  
 Identificadores que são retornados no conjunto de resultados não estão entre aspas, mesmo se eles contiverem caracteres especiais. Por exemplo, suponha que o identificador de caractere de aspas (que é específico do driver e retornado por meio **SQLGetInfo**) é uma marca de aspas duplas (") e a tabela de contas a pagar contém uma coluna chamada Customer Name. Na linha retornada por **SQLColumns** desta coluna, o valor da coluna do TABLE_NAME é contas a pagar, não "contas a pagar", e o valor da coluna COLUMN_NAME é o nome do cliente, não "nome do cliente". Para recuperar os nomes dos clientes na tabela de contas a pagar, o aplicativo poderia citar esses nomes:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 Para obter mais informações, consulte [identificadores entre aspas](../../../odbc/reference/develop-app/quoted-identifiers.md).  
  
 As funções de catálogo são com base em um modelo de autorização do tipo SQL no qual uma conexão é feita com base em um nome de usuário e senha, e apenas os dados para o qual o usuário tem um privilégio são retornados. Proteção por senha dos arquivos individuais, que não se encaixam nesse modelo, é definido pelo driver.  
  
 Os conjuntos de resultados retornados pelas funções de catálogo quase nunca são atualizáveis e aplicativos não devem esperar ser capaz de alterar a estrutura do banco de dados, alterando os dados nesses conjuntos de resultados.
