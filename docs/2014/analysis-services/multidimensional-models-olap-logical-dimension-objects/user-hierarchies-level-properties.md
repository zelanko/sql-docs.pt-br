---
title: Propriedades de nível | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
ms.assetid: dabb7335-887b-442a-b67c-4901ba1242b7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c55a596461e03ce91a822e4578f7de56fe27f8f1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702202"
---
# <a name="level-properties"></a>Propriedades de nível 
  A tabela a seguir lista e descreve as propriedades de um nível em uma hierarquia definida pelo usuário.  
  
|Propriedade|DESCRIÇÃO|  
|--------------|-----------------|  
|DESCRIÇÃO|Contém a descrição do nível.|  
|HideMemberIf|Indica se, e quando, um membro em um nível ficará oculto pelos aplicativos cliente. Essa propriedade pode ter os seguintes valores:<br /><br /> Never<br /> Membros nunca são ocultados. Esse é o valor padrão.<br /><br /> OnlyChildWithNoName<br /> Um membro é ocultado quando o membro for o único filho de seu pai e seu nome estiver vazio.<br /><br /> OnlyChildWithParentName<br /> Um membro é ocultado quando o membro for o único filho de seu pai e seu nome for idêntico ao de seu pai.<br /><br /> NoName<br /> Um membro é ocultado quando o nome do membro estiver vazio.<br /><br /> ParentName<br /> Um membro é ocultado quando o nome do membro for idêntico ao de seu pai.|  
|ID|Contém o identificador exclusivo (ID) do nível.|  
|Nome|Contém o nome amigável do nível. Por padrão, o nome de um nível é igual ao nome do atributo de origem.|  
|SourceAttribute|Contém o nome do atributo de origem no qual o nível tem como base.|  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades de hierarquia do usuário](user-hierarchies-properties.md)  
  
  
