---
description: Método Append (Índices do ADOX)
title: Método Append (índices ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
author: rothja
ms.author: jroth
ms.openlocfilehash: 00b37055efe15f204049d02c337b54c228468419
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985507"
---
# <a name="append-method-adox-indexes"></a>Método Append (Índices do ADOX)
Adiciona um novo objeto de [índice](./index-object-adox.md) à coleção de [índices](./indexes-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Index*  
 O objeto de **índice** a ser acrescentado ou o nome do índice a ser criado e acrescentado.  
  
 *Colunas*  
 Opcional. Um valor de **variante** que especifica os nomes das colunas a serem indexadas. O parâmetro *Columns* corresponde ao (s) valor (es) da propriedade [Name](./name-property-adox.md) de um objeto ou objetos [Column](./column-object-adox.md) .  
  
## <a name="remarks"></a>Comentários  
 O parâmetro *Columns* pode ter o nome de uma coluna ou uma matriz de nomes de coluna.  
  
 Ocorrerá um erro se o provedor não der suporte à criação de índices.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Indexes (ADOX)](./indexes-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Indexes Append (VB)](./indexes-append-method-example-vb.md)   
 [Método Append (colunas ADOX)](./append-method-adox-columns.md)   
 [Método Append (grupos ADOX)](./append-method-adox-groups.md)   
 [Método Append (chaves ADOX)](./append-method-adox-keys.md)   
 [Método Append (procedimentos do ADOX)](./append-method-adox-procedures.md)   
 [Método Append (tabelas ADOX)](./append-method-adox-tables.md)   
 [Método Append (usuários do ADOX)](./append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](./append-method-adox-views.md)