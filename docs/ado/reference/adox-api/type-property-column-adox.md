---
description: Propriedade Type (Column) (ADOX)
title: Propriedade Type (coluna) (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 70d8700f953a87fa3326f6a1c0985be1f6ca3dac
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769215"
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