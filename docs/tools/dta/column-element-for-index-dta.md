---
title: Elemento de coluna para índice (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Column element
ms.assetid: ba9fac20-26bd-4333-940e-842c15241b46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6fa488250a0dd7d49a47c22c09401395ac5e1949
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684174"
---
# <a name="column-element-for-index-dta"></a>Elemento de coluna para índice (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
 **Tipo**: opcional. Especifica o tipo de coluna de índice. Use um tipo de dados de **cadeia de caracteres** para especificar esse atributo com um dos seguintes valores permitidos:  
  
-   **KeyColumn**  
  
     Especifica que a coluna é referenciada por uma chave de índice. Use a sintaxe a seguir para definir esse atributo:  
  
    ```  
    <Column Type="KeyColumn">  
    ```  
  
     Para obter mais informações sobre colunas de chave, veja [Índices clusterizados e não clusterizados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md).  
  
-   **IncludedColumn**  
  
     Especifica que a coluna é uma coluna incluída (ao invés de uma coluna de chave). Use a sintaxe a seguir para definir esse atributo:  
  
    ```  
    <Column Type="IncludedColumn">  
    ```  
  
     Para obter mais informações sobre colunas incluídas, veja [Criar índices com colunas incluídas](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
 **SortOrder**: opcional. Especifica a ordem de escolha da coluna. Use um tipo de dados **de cadeia de caracteres** para especificar uma ordem **"Crescente"** ou **"Decrescente"** como segue:  
  
```  
<Column SortOrder="Ascending">  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Pode especificar até 1024 colunas para o elemento **Index** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Index &#40;DTA&#41;](../../tools/dta/index-element-dta.md)|  
|**Elementos filho**|[Elemento Name para coluna &#40;DTA&#41;](../../tools/dta/name-element-for-column-dta.md)|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivo de entrada XML com configuração especificada pelo usuário (DTA)](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
