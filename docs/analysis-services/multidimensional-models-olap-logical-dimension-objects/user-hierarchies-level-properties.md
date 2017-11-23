---
title: "Propriedades - hierarquias de usuário de nível | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
ms.assetid: dabb7335-887b-442a-b67c-4901ba1242b7
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dea548f76a6197f557a520bfa0153133643bed3a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="user-hierarchies---level-properties"></a>Hierarquias de usuário - propriedades de nível
  A tabela a seguir lista e descreve as propriedades de um nível em uma hierarquia definida pelo usuário.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|Description|Contém a descrição do nível.|  
|HideMemberIf|Indica se, e quando, um membro em um nível ficará oculto pelos aplicativos cliente. Essa propriedade pode ter os seguintes valores:<br /><br /> Never<br /> Membros nunca são ocultados. Este é o valor padrão.<br /><br /> OnlyChildWithNoName<br /> Um membro é ocultado quando o membro for o único filho de seu pai e seu nome estiver vazio.<br /><br /> OnlyChildWithParentName<br /> Um membro é ocultado quando o membro for o único filho de seu pai e seu nome for idêntico ao de seu pai.<br /><br /> NoName<br /> Um membro é ocultado quando o nome do membro estiver vazio.<br /><br /> ParentName<br /> Um membro é ocultado quando o nome do membro for idêntico ao de seu pai.|  
|ID|Contém o identificador exclusivo (ID) do nível.|  
|Nome|Contém o nome amigável do nível. Por padrão, o nome de um nível é igual ao nome do atributo de origem.|  
|SourceAttribute|Contém o nome do atributo de origem no qual o nível tem como base.|  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades de hierarquia de usuário](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
