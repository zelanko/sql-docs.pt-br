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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0d9b63de04f79fd95c1b06d8e84d85c6f4fea02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305220"
---
# <a name="data-returned-by-catalog-functions"></a>Dados retornados pelas funções de catálogo
Cada função de catálogo retorna os dados como um conjunto de resultados. Este conjunto de resultados não é diferente de qualquer outro conjunto de resultados. Geralmente é gerado por uma declaração **SELECT** predefinida e parametrizada que é codificada no driver ou armazenada em um procedimento na fonte de dados. Para obter informações sobre como recuperar dados de um conjunto de resultados, consulte [Foi criado um conjunto de resultados?](../../../odbc/reference/develop-app/was-a-result-set-created.md).  
  
 O conjunto de resultados para cada função de catálogo é descrito na entrada de referência para essa função. Além das colunas listadas, o conjunto de resultados pode conter colunas específicas do driver após a última coluna predefinida. Essas colunas (se houver) estão descritas na documentação do driver.  
  
 Os aplicativos devem vincular colunas específicas do driver em relação ao final do conjunto de resultados. Ou seja, eles devem calcular o número de uma coluna específica do driver como o número da última coluna - recuperado com **SQLNumResultCols** - menos o número de colunas que ocorrem após a coluna necessária. Isso evita ter que mudar o aplicativo quando novas colunas são adicionadas ao resultado definido em versões futuras do ODBC ou do driver. Para que esse esquema funcione, os drivers devem adicionar novas colunas específicas para o driver antes de colunas antigas específicas do driver para que os números das colunas não mudem em relação ao final do conjunto de resultados.  
  
 Os identificadores que são devolvidos no conjunto de resultados não são citados, mesmo que contenham caracteres especiais. Por exemplo, suponha que o caractere de citação do identificador (que é específico do driver e devolvido através **do SQLGetInfo)** é uma marca de cotação dupla (") e a tabela Contas a pagar contém uma coluna chamada Nome do Cliente. Na linha devolvida pela **SQLColumns** para esta coluna, o valor da coluna TABLE_NAME é Contas A Pagar, e não "Contas a Pagar", e o valor da coluna COLUMN_NAME é Nome do Cliente, não "Nome do Cliente". Para recuperar os nomes dos clientes na tabela Contas a Pagar, o aplicativo citaria esses nomes:  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 Para obter mais informações, consulte [Identificadores citados](../../../odbc/reference/develop-app/quoted-identifiers.md).  
  
 As funções do catálogo são baseadas em um modelo de autorização semelhante ao SQL no qual uma conexão é feita com base em um nome de usuário e senha, e apenas os dados para os quais o usuário tem um privilégio são devolvidos. A proteção por senha de arquivos individuais, que não se encaixam neste modelo, é definida pelo driver.  
  
 Os conjuntos de resultados retornados pelas funções do catálogo quase nunca são updatable, e os aplicativos não devem esperar ser capazes de alterar a estrutura do banco de dados alterando os dados nesses conjuntos de resultados.
