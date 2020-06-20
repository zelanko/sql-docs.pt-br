---
title: Remover UDTs nomeados após os tipos de dados reservados GEOMETRY e geography | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], UDTs
- geography data type [SQL Server], UDTs
ms.assetid: a167ce3a-50b4-4e77-a884-adb23b586c72
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 4977d45d53e1114edc8e04ad504963bae0b9eb9d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059114"
---
# <a name="remove-udts-named-after-the-reserved-geometry-and-geography-data-types"></a>Remover UDTs com o mesmo nome dos tipos de dados reservados GEOMETRY e GEOGRAPHY
  O Supervisor de Atualização detectou um tipo definido pelo usuário (UDT) que tem o mesmo nome de um termo reservado para os tipos de dados `geometry` ou `geography`. Os tipos de dados `geometry` e `geography` fazem parte do recurso de dados espaciais.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 Os termos usados para tipos de dados espaciais não devem ser utilizados como nomes de UDTs de alias ou CLR.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Remova o UDT que tem o mesmo nome do tipo de dados e recrie o UDT com um nome não reservado.  
  
## <a name="external-resources"></a>Recursos externos  
 [Criar um tipo definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
