---
description: Propriedade Type (Column) (ADOX)
title: Propriedade Type (coluna) (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::Type
- _Column::GetType
- _Column::get_Type
- _Column::put_Type
- _Column::PutType
helpviewer_keywords:
- Type property [ADOX]
ms.assetid: 5c6718b6-f728-478a-8afb-5d17b0a91d1f
author: rothja
ms.author: jroth
ms.openlocfilehash: dffb08de42e3c38a9c0a28e8cad33af95f0d8926
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983167"
---
# <a name="type-property-column-adox"></a>Propriedade Type (Column) (ADOX)
Indica o tipo de dados de uma coluna.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **longo** que pode ser uma das constantes [DataTypeEnum](../ado-api/datatypeenum.md) . O valor padrão é **adVarWChar**.  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade é de leitura/gravação até que o objeto de [coluna](./column-object-adox.md) seja anexado a uma coleção ou a outro objeto, após o qual ele é somente leitura.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Column (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade ParentCatalog (VB)](./parentcatalog-property-example-vb.md)   
 [Propriedade Type (chave) (ADOX)](./type-property-key-adox.md)   
 [Propriedade Type (Table) (ADOX)](./type-property-table-adox.md)