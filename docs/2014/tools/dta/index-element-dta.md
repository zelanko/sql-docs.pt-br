---
title: Índice de elemento (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Index element (DTA)
ms.assetid: 447d3964-b387-40f6-9189-71386774c29e
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6f9391fb8b85e551f2f1904e164c7d86f2dcacc1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013245"
---
# <a name="index-element-dta"></a>Elemento de índice (DTA)
  Contém informações sobre um índice que você quer criar ou descartar para uma configuração especificada pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Recommendation>  
  <Create>  
    <Index [Clustered | Unique | Online | IndexSizeInMB | NumberOfRows             | QUOTED_IDENTIFIER | ARITHABORT | CONCAT_NULL_YIELDS_NULL             | ANSI_NULLS | ANSI_PADDING | ANSI_WARNINGS  
            | NUMERIC_ROUNDABORT]  
     ...code removed here...  
    </Index>  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|Atributo de índice|Tipo de dados|Description|  
|---------------------|---------------|-----------------|  
|`Clustered`|`boolean`|Opcional. Especifica um índice clusterizado. Defina como "verdadeiro" ou "falso". Por exemplo:<br /><br /> `<Index Clustered="true">`<br /><br /> Por padrão, esse atributo é definido como "falso".|  
|`Unique`|`boolean`|Opcional. Especifica um índice exclusivo. Defina como "verdadeiro" ou "falso". Por exemplo:<br /><br /> `<Index Unique="true">`<br /><br /> Por padrão, esse atributo é definido como "falso".|  
|`Online`|`boolean`|Opcional. Especifica um índice que pode executar operações enquanto o servidor estiver online, que requer espaço temporário em disco. Defina como "verdadeiro" ou "falso". Por exemplo:<br /><br /> `<Index Online="true">`<br /><br /> Por padrão, esse atributo é definido como "falso".<br /><br /> Para obter mais informações, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).|  
|`IndexSizeInMB`|`double`|Opcional. Especifica o tamanho máximo do índice em megabytes, por exemplo:<br /><br /> `<Index IndexSizeInMB="873.75">`<br /><br /> Sem configuração padrão.|  
|`NumberOfRows`|`integer`|Opcional. Simula tamanhos de índice diferentes que efetivamente simulam tamanhos de tabela diferentes. Por exemplo:<br /><br /> `<Index NumberOfRows="3000">`<br /><br /> Sem configuração padrão.|  
|`QUOTED_IDENTIFIER`|`boolean`|Opcional. Faz com que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siga as regras ISO relativas às aspas que delimitam identificadores e cadeias de caracteres literais. Esse atributo precisará ser habilitado caso o índice esteja em coluna computada ou exibição. Por exemplo, a sintaxe a seguir define esse atributo como:<br /><br /> `<Index QUOTED_IDENTIFIER [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql).|  
|`ARITHABORT`|`boolean`|Opcional. Causa o encerramento da consulta quando ocorre estouro ou erro de divisão por zero durante a execução da consulta. Esse atributo precisará ser habilitado caso o índice esteja em coluna computada ou exibição. Por exemplo, a sintaxe a seguir define esse atributo como:<br /><br /> `<Index ARITHABORT [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql).|  
|`CONCAT_NULL_YIELDS_`<br /><br /> `NULL`|`boolean`|Opcional. Controla se os resultados de concatenação serão ou não tratados como valores de cadeia de caracteres nulos ou vazios. Esse atributo precisará ser habilitado caso o índice esteja em coluna computada ou exibição. Por exemplo, a sintaxe a seguir define esse atributo como:<br /><br /> `<Index CONCAT_NULL_YIELDS_NULL [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql).|  
|`ANSI_NULLS`|`boolean`|Opcional. Especifica o comportamento compatível ISO dos operadores de comparação Igual a (=) e É diferente de (<>) quando usados com valores nulos. Esse atributo precisará ser habilitado caso o índice esteja em coluna computada ou exibição. Por exemplo, a sintaxe a seguir define esse atributo como:<br /><br /> `<Index ANSI_NULLS [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql).|  
|`ANSI_PADDING`|`boolean`|Opcional. Controla o modo como uma coluna armazena valores menores que o tamanho definido. Esse atributo precisará ser habilitado caso o índice esteja em coluna computada ou exibição. Por exemplo, a sintaxe a seguir define esse atributo como:<br /><br /> `<Index ANSI_PADDING [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql).|  
|`ANSI_WARNINGS`|`boolean`|Opcional. Especifica o comportamento padrão ISO para várias condições de erro. Esse atributo precisará ser habilitado caso o índice esteja em coluna computada ou exibição. Por exemplo, a sintaxe a seguir define esse atributo como:<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql).|  
|`NUMERIC_ROUNDABORT`|`boolean`|Opcional. Especifica o nível dos relatórios de erro gerados quando o arredondamento de uma expressão provoca perda de exatidão. Esse atributo precisará ser desabilitado caso o índice pertença a uma coluna computada ou exibição.<br /><br /> A sintaxe a seguir define esse atributo como:<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-numeric-roundabort-transact-sql).|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Exigido uma vez para cada um dos elementos `Create` ou `Drop` se nenhuma outra estrutura física de design for especificada com os elementos `Statistics` ou `Heap`.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Criar elemento &#40;DTA&#41;](create-element-dta.md)<br /><br /> `Drop` Elemento. Para obter mais informações, consulte o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados.|  
|**Elementos filho**|[Nome de elemento de índice &#40;DTA&#41;](name-element-for-index-dta.md)<br /><br /> [Elemento de coluna para índice &#40;DTA&#41;](column-element-for-index-dta.md)<br /><br /> `PartitionScheme` Elemento. Para obter mais informações, consulte o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados.<br /><br /> `PartitionColumn` Elemento. Para obter mais informações, consulte o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados.<br /><br /> [Elemento de grupo de arquivos para índice &#40;DTA&#41;](filegroup-element-for-index-dta.md)<br /><br /> `NumberOfReferences` Elemento. Para obter mais informações, consulte o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados.<br /><br /> `PercentUsage` Elemento. Para obter mais informações, consulte o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja a [Amostra de arquivo de entrada XML com a configuração especificada pelo usuário &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
