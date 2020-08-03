---
title: Conjuntos de resultados de automação | Microsoft Docs
description: Saiba que, se uma propriedade de automação de OLE ou método retorna dados em uma matriz com uma ou duas dimensões, a matriz é retornada ao cliente como um conjunto de resultados.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [SQL Server], OLE Automation
- two-dimensional arrays
- one-dimensional arrays
- result sets [SQL Server], OLE Automation
- OLE Automation [SQL Server], result sets
- arrays [SQL Server]
ms.assetid: b2f99e33-2303-427c-94b9-9d55f8e2a6ab
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8e3498ed53137443b647e2d1e93fbec5c7d49ef5
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332580"
---
# <a name="ole-automation-result-sets"></a>Conjuntos de resultado de automação OLE
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Se uma propriedade de automação OLE ou método retorna dados em uma matriz com uma ou duas dimensões, a matriz é retornada ao cliente como um conjunto de resultados:  
  
-   Uma matriz unidimensional é retornada ao cliente como um conjunto de resultados de uma linha, com tantas colunas quanto houver elementos na matriz. Por exemplo, uma matriz (10) é retornada como uma única linha de 10 colunas.  
  
-   Uma matriz bidimensional é retornada ao cliente como um conjunto de resultados com tantas colunas quanto houver elementos na primeira dimensão da matriz e com tantas linhas quanto houver elementos na segunda dimensão da matriz. Por exemplo, uma matriz (2,3) é retornada como 2 colunas em 3 linhas.  
  
 Quando o valor de retorno de uma propriedade ou o valor de retorno de um método for uma matriz, sp_OAGetProperty ou sp_OAMethod retornará um conjunto de resultados ao cliente. (Os parâmetros de saída de método não podem ser matrizes.) Esses procedimentos examinam todos os valores de dados na matriz para determinar os tipos de dados apropriados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os tamanhos dos dados a serem usados para cada coluna no conjunto de resultados. Para uma coluna específica, esses procedimentos usam o tipo de dados e o tamanho necessários para representar todos os valores de dados nesta coluna.  
  
 Quando todos os valores de dados em uma coluna compartilharem o mesmo tipo de dados, esse tipo de dados será usado para a coluna inteira. Quando os valores de dados em uma coluna são de tipos de dados diferentes, o tipo de dados da coluna inteira é escolhido com base na tabela a seguir. Para usar a tabela a seguir, localize um tipo de dados ao longo do eixo da linha esquerda e um segundo tipo de dados ao longo do eixo da coluna superior. A interseção da linha com a coluna descreve o tipo de dados da coluna do conjunto de resultados.  
  
|   | **int** | **float** | **money** | **datetime** | **varchar** | **nvarchar** |
| - | ------- | --------- | --------- | ------------ | ----------- | ------------ |
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Procedimentos armazenados de Automação OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
 [Opção de configuração de servidor Ole Automation Procedures](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)  
  
  
