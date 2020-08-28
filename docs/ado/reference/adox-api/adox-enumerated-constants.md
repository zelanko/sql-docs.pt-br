---
description: Constantes enumeradas ADOX
title: Constantes enumeradas do ADOX | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADOX]
ms.assetid: 9d91f511-d46f-44ef-97ef-77bf93836186
author: rothja
ms.author: jroth
ms.openlocfilehash: 1def9c0445551376aec56c36c554b9c74b15c02f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985707"
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