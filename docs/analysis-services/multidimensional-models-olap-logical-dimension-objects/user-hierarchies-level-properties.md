---
title: Propriedades - hierarquias de usuário de nível | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 903ece979d44dedd6353919af28bdb6c82986e16
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="user-hierarchies---level-properties"></a>Hierarquias de usuário - propriedades de nível
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
  
  
