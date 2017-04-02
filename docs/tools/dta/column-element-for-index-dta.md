---
title: "Elemento de coluna para &#237;ndice (DTA) | Microsoft Docs"
ms.custom: ""
ms.date: "03/09/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "XML"
helpviewer_keywords: 
  - "Elemento Column"
ms.assetid: ba9fac20-26bd-4333-940e-842c15241b46
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# Elemento de coluna para &#237;ndice (DTA)
  Especifica as colunas onde o índice é criado para uma configuração especificada pelo usuário.  
  
## Sintaxe  
  
```  
  
<Create>  
  <Index>  
    <Name>...</Name>  
    <Column [Type | SortOrder]>  
     ...code removed here...  
     </Column>  
```  
  
## Atributos do elemento  
  
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
  
## Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhuma.|  
|**Valor padrão**|Nenhuma.|  
|**Ocorrência**|Pode especificar até 1024 colunas para o elemento **Index** .|  
  
## Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Index &#40;DTA&#41;](../../tools/dta/index-element-dta.md)|  
|**Elementos filho**|[Elemento Name para coluna &#40;DTA&#41;](../../tools/dta/name-element-for-column-dta.md)|  
  
## Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivo de entrada XML com configuração especificada pelo usuário (DTA)](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  