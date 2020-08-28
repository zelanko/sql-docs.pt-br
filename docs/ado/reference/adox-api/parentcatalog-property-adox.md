---
description: Propriedade ParentCatalog (ADOX)
title: Propriedade ParentCatalog (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User::get_ParentCatalog
- _Column::ParentCatalog
- _Table::put_ParentCatalog
- _Group::put_ParentCatalog
- _Column::get_ParentCatalog
- _Table::PutParentCatalog
- _Group::putref_ParentCatalog
- _Group::ParentCatalog
- _Column::PutParentCatalog
- _Column::put_ParentCatalog
- _Group::get_ParentCatalog
- _User::put_ParentCatalog
- _User::putref_ParentCatalog
- _Table::get_ParentCatalog
- _Group::PutParentCatalog
- _Table::ParentCatalog
- _Column::GetParentCatalog
- _Table::PutRefParentCatalog
- _User::GetParentCatalog
- _Table::GetParentCatalog
- _Table::putref_ParentCatalog
- _User::PutParentCatalog
- _User::ParentCatalog
- _User::PutRefParentCatalog
- _Group::GetParentCatalog
- _Group::PutRefParentCatalog
helpviewer_keywords:
- ParentCatalog property [ADOX]
ms.assetid: a0bb2ed8-d4cb-4f92-8de7-769bbe0e6273
author: rothja
ms.author: jroth
ms.openlocfilehash: 07e4cdabe09b2bc4af8e849ef367df65c23711ca
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983767"
---
# <a name="parentcatalog-property-adox"></a>Propriedade ParentCatalog (ADOX)
Especifica o catálogo pai de uma tabela, um usuário ou um objeto de coluna para fornecer acesso às propriedades específicas do provedor.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define e retorna um objeto de [Catálogo](./catalog-object-adox.md) . A definição de **ParentCatalog** para um **Catálogo** aberto permite o acesso a propriedades específicas do provedor antes de acrescentar uma tabela ou coluna a uma coleção de **catálogos** .  
  
## <a name="remarks"></a>Comentários  
 Alguns provedores de dados permitem que os valores de propriedade específicos do provedor sejam gravados somente na criação: ou seja, quando uma tabela ou coluna é anexada à sua coleção de **Catálogo** . Para acessar essas propriedades antes de acrescentar esses objetos a um **Catálogo**, especifique primeiro o **Catálogo** na propriedade **ParentCatalog** .  
  
 Um erro ocorre quando a tabela ou coluna é anexada a um **Catálogo** diferente do **ParentCatalog**.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Column (ADOX)](./column-object-adox.md)  
    :::column-end:::
    :::column:::
        [Objeto Table (ADOX)](./table-object-adox.md)  
    :::column-end:::
    :::column:::
        [Objeto User (ADOX)](./user-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade ParentCatalog (VB)](./parentcatalog-property-example-vb.md)