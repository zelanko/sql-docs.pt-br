---
title: RightsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: RightsEnum
helpviewer_keywords: RightsEnum enumeration [ADOX]
ms.assetid: 55ee67c7-a583-42aa-849a-78264b4cb614
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ff15518703e8e8ec2d2c3ee67df691abb1974ac
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="rightsenum"></a>RightsEnum
Especifica os direitos ou permissões para um grupo ou usuário em um objeto.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adRightCreate**|16384 (& H4000)|O usuário ou grupo tem permissão para criar novos objetos deste tipo.|  
|**adRightDelete**|65536 (& H10000)|O usuário ou grupo tem permissão para excluir dados de um objeto. Para objetos, como **tabelas**, o usuário tem permissão para excluir os valores de dados de registros.|  
|**adRightDrop**|256 (& H100)|O usuário ou grupo tem permissão para remover objetos do catálogo. Por exemplo, **tabelas** pode ser excluído por um comando DROP TABLE SQL.|  
|**adRightExclusive**|512 (& H200)|O usuário ou grupo tem permissão para acessar o objeto exclusivamente.|  
|**adRightExecute**|536870912 (& H20000000)|O usuário ou grupo tem permissão para executar o objeto.|  
|**adRightFull**|268435456 (& H10000000)|O usuário ou grupo tem todas as permissões no objeto.|  
|**adRightInsert**|32768 (& H8000)|O usuário ou grupo tem permissão para inserir o objeto. Para objetos, como **tabelas**, o usuário tem permissão para inserir dados na tabela.|  
|**adRightMaximumAllowed**|33554432 (& H2000000)|O usuário ou grupo tem o número máximo de permissões permitidas pelo provedor. Permissões específicas dependem do provedor.|  
|**adRightNone**|0|O usuário ou grupo não tem permissões para o objeto.|  
|**adRightRead**|-2147483648 (& H80000000)|O usuário ou grupo tem permissão para ler o objeto. Para objetos, como [tabelas](../../../ado/reference/adox-api/table-object-adox.md), o usuário tem permissão para ler os dados na tabela.|  
|**adRightReadDesign**|1024 (& H400)|O usuário ou grupo tem permissão para ler o design do objeto.|  
|**adRightReadPermissions**|131072 (& H20000)|O usuário ou grupo pode exibir, mas não alterar as permissões específicas para um objeto no catálogo.|  
|**adRightReference**|8192 (& H2000)|O usuário ou grupo tem permissão para fazer referência ao objeto.|  
|**adRightUpdate**|1073741824 (& H40000000)|O usuário ou grupo tem permissão para atualizar o objeto. Para objetos, como **tabelas**, o usuário tem permissão para atualizar os dados na tabela.|  
|**adRightWithGrant**|4096 (& H1000)|O usuário ou grupo tem permissão para conceder permissões no objeto.|  
|**adRightWriteDesign**|2048 (& H800)|O usuário ou grupo tem permissão para modificar o design do objeto.|  
|**adRightWriteOwner**|524288 (& H80000)|O usuário ou grupo tem permissão para modificar o proprietário do objeto.|  
|**adRightWritePermissions**|262144 (& H40000)|O usuário ou grupo pode modificar as permissões específicas para um objeto no catálogo.|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Método GetPermissions (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|[Método SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
