---
description: Propriedade Name (ADOX)
title: Propriedade Name (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::PutName
- _Table::GetName
- _Key::Name
- _Key::get_Name
- _Column::GetName
- _Index::Name
- _Index::put_Name
- _Column::PutName
- _Key::put_Name
- _Table::put_Name
- _User25::PutName
- _Index::get_Name
- _Column::get_Name
- _Group25::Name
- _Group25::get_Name
- _Column::Name
- _User25::get_Name
- _Table::Name
- _Group25::GetName
- _Index::PutName
- _Column::put_Name
- _Key::GetName
- _Table::get_Name
- _User25::Name
- _User25::put_Name
- _Index::GetName
- _User25::GetName
helpviewer_keywords:
- Name property [ADOX]
ms.assetid: 81b92baf-b6b9-4f4e-9f33-4503795518cd
author: rothja
ms.author: jroth
ms.openlocfilehash: dd3a9fd328ce332c409d613ad468b96f0b94d31e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983907"
---
# <a name="name-property-adox"></a>Propriedade Name (ADOX)
Indica o nome do objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia de caracteres** .  
  
## <a name="remarks"></a>Comentários  
 Os nomes não precisam ser exclusivos em uma coleção.  
  
 A propriedade **Name** é leitura/gravação em objetos de [coluna](./column-object-adox.md), [grupo](./group-object-adox.md), [chave](./key-object-adox.md), [índice](./index-object-adox.md), [tabela](./table-object-adox.md)e [usuário](./user-object-adox.md) . A propriedade **Name** é somente leitura em objetos de [Catálogo](./catalog-object-adox.md), [procedimento](./procedure-object-adox.md)e [exibição](./view-object-adox.md) .  
  
 Para objetos de leitura/gravação (**coluna**, **grupo**, **chave**, **índice**, **tabela** e objetos de **usuário** ), o valor padrão é uma cadeia de caracteres vazia ("").  
  
> [!NOTE]
>  Para chaves, essa propriedade é somente leitura em objetos de **chave** já anexados a uma coleção. Para tabelas, essa propriedade é somente leitura para objetos de **tabela** já anexados a uma coleção.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Column (ADOX)](./column-object-adox.md)  
        [Objeto Group (ADOX)](./group-object-adox.md)  
        [Objeto Index (ADOX)](./index-object-adox.md)  
    :::column-end:::
    :::column:::
        [Objeto Key (ADOX)](./key-object-adox.md)  
        [Objeto Procedure (ADOX)](./procedure-object-adox.md)  
        [Objeto Property (ADO)](../ado-api/property-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Table (ADOX)](./table-object-adox.md)  
        [Objeto User (ADOX)](./user-object-adox.md)  
        [Objeto View (ADOX)](./view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Name e métodos de acréscimo de colunas e tabelas (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](./parentcatalog-property-example-vb.md)