---
title: Remover UDTs com os tipos de dados reservados GEOMETRY e GEOGRAPHY | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], UDTs
- geography data type [SQL Server], UDTs
ms.assetid: a167ce3a-50b4-4e77-a884-adb23b586c72
caps.latest.revision: 12
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e557c8c41596045390127ad066681a2f5c872875
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208516"
---
# <a name="remove-udts-named-after-the-reserved-geometry-and-geography-data-types"></a>Remover UDTs com o mesmo nome dos tipos de dados reservados GEOMETRY e GEOGRAPHY
  O Supervisor de Atualização detectou um tipo definido pelo usuário (UDT) que tem o mesmo nome de um termo reservado para os tipos de dados `geometry` ou `geography`. Os tipos de dados `geometry` e `geography` fazem parte do recurso de dados espaciais.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 Os termos usados para tipos de dados espaciais não devem ser utilizados como nomes de UDTs de alias ou CLR.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Remova o UDT que tem o mesmo nome do tipo de dados e recrie o UDT com um nome não reservado.  
  
## <a name="external-resources"></a>Recursos externos  
 [Criando um tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
