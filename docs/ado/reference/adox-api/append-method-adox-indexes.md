---
title: Método Append (índices ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 6996f3a0a3ad9f2ffa727a6cbd7b48d3fbf32777
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764057"
---
# <a name="append-method-adox-indexes"></a>Método Append (Índices do ADOX)
Adiciona um novo objeto de [índice](../../../ado/reference/adox-api/index-object-adox.md) à coleção de [índices](../../../ado/reference/adox-api/indexes-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Index*  
 O objeto de **índice** a ser acrescentado ou o nome do índice a ser criado e acrescentado.  
  
 *Colunas*  
 Opcional. Um valor de **variante** que especifica os nomes das colunas a serem indexadas. O parâmetro *Columns* corresponde ao (s) valor (es) da propriedade [Name](../../../ado/reference/adox-api/name-property-adox.md) de um objeto ou objetos [Column](../../../ado/reference/adox-api/column-object-adox.md) .  
  
## <a name="remarks"></a>Comentários  
 O parâmetro *Columns* pode ter o nome de uma coluna ou uma matriz de nomes de coluna.  
  
 Ocorrerá um erro se o provedor não der suporte à criação de índices.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Indexes Append (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Método Append (colunas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Método Append (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Método Append (chaves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Método Append (procedimentos do ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Método Append (tabelas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Método Append (usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
