---
title: Exibir diferenças de dados
description: Saiba como comparar dois bancos de dados e veja quais as diferenças entre os objetos de banco de dados deles. Confira como exibir registros em objetos e como filtrar a exibição.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.datacompare.f1
ms.assetid: f88d3350-2eaf-44cc-96a8-84008b6cd071
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 750909ea5344d5972ffdc8a2db418d8c482231f5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895760"
---
# <a name="how-to-view-data-differences"></a>Como fazer: Exibir diferenças de dados

Depois que você comparar os dados em dois bancos de dados, verá cada *objeto de banco de dados* que você comparou e seu status. Você também pode exibir os resultados para os registros dentro de cada objeto, agrupados por status.  
  
Depois que você exibir as diferenças, poderá atualizar o *destino* para corresponder à *origem* para alguns ou todos os objetos ou registros que forem diferentes, ausentes ou novos.  
  
### <a name="to-view-data-differences"></a>Para exibir diferenças de dados  
  
1.  Compare os dados em uma origem e destino.  
  
2.  (Opcional) Siga um ou ambos destes procedimentos:  
  
    -   Por padrão, os resultados para todos os objetos aparecem, independentemente de seu status. Para exibir apenas os objetos que tiverem um status específico, clique em uma opção na lista **Filtrar**.  
  
    -   Para exibir resultados para registros dentro de um objeto específico, clique no objeto no painel de resultados principal e clique em uma guia no painel Exibir Registros. Cada guia exibe todos os registros dentro desse objeto que têm um status específico: diferente, somente na origem, somente no destino e idêntico. Os dados são exibidos por registro e coluna.  
  
## <a name="see-also"></a>Consulte Também  
[Como: Usar comparação de esquema para comparar definições de banco de dados diferentes](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
