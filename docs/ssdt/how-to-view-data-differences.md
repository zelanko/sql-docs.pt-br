---
title: Como exibir diferenças de dados | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql.data.tools.datacompare.f1
ms.assetid: f88d3350-2eaf-44cc-96a8-84008b6cd071
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a7025a59d6db451bb008bca72909bed16b1803da
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093597"
---
# <a name="how-to-view-data-differences"></a>Como: exibir diferenças de dados
Depois que você comparar os dados em dois bancos de dados, verá cada *objeto de banco de dados* que você comparou e seu status. Você também pode exibir os resultados para os registros dentro de cada objeto, agrupados por status.  
  
Depois que você exibir as diferenças, poderá atualizar o *destino* para corresponder à *origem* para alguns ou todos os objetos ou registros que forem diferentes, ausentes ou novos.  
  
### <a name="to-view-data-differences"></a>Para exibir diferenças de dados  
  
1.  Compare os dados em uma origem e destino.  
  
2.  (Opcional) Siga um ou ambos destes procedimentos:  
  
    -   Por padrão, os resultados para todos os objetos aparecem, independentemente de seu status. Para exibir apenas os objetos que tiverem um status específico, clique em uma opção na lista **Filtrar**.  
  
    -   Para exibir resultados para registros dentro de um objeto específico, clique no objeto no painel de resultados principal e clique em uma guia no painel Exibir Registros. Cada guia exibe todos os registros dentro desse objeto que têm um status específico: diferente, somente na origem, somente no destino e idêntico. Os dados são exibidos por registro e coluna.  
  
## <a name="see-also"></a>Consulte Também  
[Como usar comparação de esquema para comparar definições de banco de dados diferentes](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
