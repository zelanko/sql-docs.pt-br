---
description: Objetos ADOX
title: Objetos ADOX | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- objects [ADOX]
- ADOX, objects
ms.assetid: 3f5287e9-f62c-40c4-bb59-985102be956e
author: rothja
ms.author: jroth
ms.openlocfilehash: c38b184164109ee3e6fed18a439cd904119a3ec6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985657"
---
# <a name="adox-objects"></a>Objetos ADOX
## <a name="adox-object-summary"></a>Resumo do objeto ADOX  
  
|Objeto|Descrição|  
|------------|-----------------|  
|[Catálogo](./catalog-object-adox.md)|Contém coleções que descrevem o catálogo de esquema de uma fonte de dados.|  
|[Coluna](./column-object-adox.md)|Representa uma coluna de uma tabela, índice ou chave.|  
|[Grupo](./group-object-adox.md)|Representa uma conta de grupo que tem permissões de acesso em um banco de dados protegido.|  
|[Index](./index-object-adox.md)|Representa um índice de uma tabela de banco de dados.|  
|[Chave](./key-object-adox.md)|Representa um campo de chave primária, estrangeira ou exclusiva de uma tabela de banco de dados.|  
|[Procedimento](./procedure-object-adox.md)|Representa um procedimento armazenado.|  
|[Table](./table-object-adox.md)|Representa uma tabela de banco de dados, incluindo colunas, índices e chaves.|  
|[Usuário](./user-object-adox.md)|Representa uma conta de usuário que tem permissões de acesso em um banco de dados protegido.|  
|[Exibir](./view-object-adox.md)|Representa um conjunto filtrado de registros ou uma tabela virtual.|  
  
 As relações entre esses objetos são ilustradas no [modelo de objeto do ADOX](./adox-object-model.md).  
  
 Cada objeto pode estar contido em sua coleção correspondente. Por exemplo, um objeto **Table** pode estar contido em uma coleção [Tables](./tables-collection-adox.md) . Para obter mais informações, consulte [coleções do ADOX](./adox-collections.md) ou um tópico de coleção específico.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API do ADOX](./adox-object-model.md?view=sql-server-ver15)   
 [Coleções do ADOX](./adox-collections.md)   
 [Modelo de objeto ADOX](./adox-object-model.md)   
 [Extensões ADO para segurança e linguagem de definição de dados (ADOX)](../../guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)