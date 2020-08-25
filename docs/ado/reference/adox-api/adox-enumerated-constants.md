---
description: Constantes enumeradas ADOX
title: Constantes enumeradas do ADOX | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADOX]
ms.assetid: 9d91f511-d46f-44ef-97ef-77bf93836186
author: rothja
ms.author: jroth
ms.openlocfilehash: 553924a51845c7ac49bfb76bab27f75c7d4e4742
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771605"
---
# <a name="adox-enumerated-constants"></a>Constantes enumeradas ADOX
Para auxiliar a depuração, as constantes enumeradas do ADOX listam um valor para cada constante. No entanto, esse valor é puramente consultivo e pode mudar de uma versão do ADOX para outra. Seu código só deve depender do nome, não do valor real, das constantes enumeradas.  
  
 As constantes enumeradas a seguir são definidas.  
  
|Enumeração|Descrição|  
|-----------------|-----------------|  
|[ActionEnum](./actionenum.md)|Especifica o tipo de ação a ser executada quando **SetPermissions** é chamada.|  
|[AllowNullsEnum](./allownullsenum.md)|Especifica se os registros com valores nulos são indexados.|  
|[ColumnAttributesEnum](./columnattributesenum.md)|Especifica as características de uma **coluna**.|  
|[DataTypeEnum](../ado-api/datatypeenum.md)|Especifica o tipo de dados de um **campo**, **parâmetro**ou **Propriedade**.|  
|[InheritTypeEnum](./inherittypeenum.md)|Especifica como os objetos herdarão as permissões definidas com **SetPermissions**.|  
|[KeyTypeEnum](./keytypeenum.md)|Especifica o tipo de **chave**: primária, estrangeira ou exclusiva.|  
|[ObjectTypeEnum](./objecttypeenum.md)|Especifica o tipo de objeto de banco de dados para o qual definir permissões ou propriedade.|  
|[RightsEnum](./rightsenum.md)|Especifica os direitos ou permissões para um grupo ou usuário em um objeto.|  
|[RuleEnum](./ruleenum.md)|Especifica a regra a ser seguida quando uma **chave** é excluída.|  
|[SortOrderEnum](./sortorderenum.md)|Especifica a sequência de classificação para uma coluna indexada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADOX](./adox-object-model.md?view=sql-server-ver15)   
 [Extensões ADO para segurança e linguagem de definição de dados (ADOX)](../../guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)