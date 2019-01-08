---
title: Elemento de coluna para índice (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Column element
ms.assetid: ba9fac20-26bd-4333-940e-842c15241b46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ef7972014dff498172b9c016b3a7debb79a054fa
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52770248"
---
# <a name="column-element-for-index-dta"></a>Elemento de coluna para índice (DTA)
  Especifica as colunas onde o índice é criado para uma configuração especificada pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Create>  
  <Index>  
    <Name>...</Name>  
    <Column [Type | SortOrder]>  
     ...code removed here...  
     </Column>  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|Atributo da coluna|Descrição|  
|----------------------|-----------------|  
|`Type`|Opcional. Especifica o tipo de coluna de índice. Use um tipo de dados de **cadeia de caracteres** para especificar esse atributo com um dos seguintes valores permitidos:<br /><br /> `KeyColumn`:<br />                  Especifica que a coluna é referenciada por uma chave de índice. Use a sintaxe a seguir para definir esse atributo:<br />`<Column Type="KeyColumn">`<br />Para obter mais informações sobre colunas de chave, veja [Índices clusterizados e não clusterizados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md).<br /><br /> `IncludedColumn`: Especifica que a coluna é uma coluna incluída (ao invés de uma coluna de chave). Use a sintaxe a seguir para definir esse atributo:<br />`<Column Type="IncludedColumn">`<br />Para obter mais informações sobre colunas incluídas, veja [Criar índices com colunas incluídas](../../relational-databases/indexes/create-indexes-with-included-columns.md).|  
|`SortOrder`|Opcional. Especifica a ordem de escolha da coluna. Use um tipo de dados **de cadeia de caracteres** para especificar uma ordem **"Crescente"** ou **"Decrescente"** como segue:<br /><br /> `<Column SortOrder="Ascending">`|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Pode especificar até 1024 colunas para o elemento `Index`.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Index &#40;DTA&#41;](index-element-dta.md)|  
|**Elementos filho**|[Elemento Name para coluna &#40;DTA&#41;](name-element-for-column-dta.md)|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivo de entrada XML com configuração especificada pelo usuário (DTA)](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
