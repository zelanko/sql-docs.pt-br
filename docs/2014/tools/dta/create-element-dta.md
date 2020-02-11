---
title: Elemento Create (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Create element (DTA)
ms.assetid: 9d076c90-f933-45f4-b6d9-447793f6528b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7ec9ad9569326e4a9b3e890af4b5f909e36e5c5b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63149486"
---
# <a name="create-element-dta"></a>Criar elemento (DTA)
  Contém informações sobre estruturas de índices, estatísticas e de heap em uma configuração especificada pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Recommendation>  
    <Create>  
    ...code removed here...  
    </Create>  
</Recommendation>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|DESCRIÇÃO|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Necessária uma vez para cada tipo de estrutura física de design (estruturas de índices, estatísticas ou de heap).|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Recommendation &#40;DTA&#41;](recommendation-element-dta.md)|  
|**Elementos filho**|[Elemento Index &#40;DTA&#41;](index-element-dta.md)<br /><br /> `Statistics`Elemento (consulte [Orientador de otimização do mecanismo de banco de dados esquema XML](https://schemas.microsoft.com/sqlserver/) para obter informações)<br /><br /> `Heap`Elemento (consulte [Orientador de otimização do mecanismo de banco de dados esquema XML](https://schemas.microsoft.com/sqlserver/) para obter informações)|  
  
## <a name="remarks"></a>Comentários  
 Esse elemento tem o nome **CreateTypecomplexType** no esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. É usado criar estruturas de índices, estatísticas e de heap em uma configuração especificada pelo usuário. Não confunda esse elemento `Create` com os outros tipos que podem ser usados para criar exibições (`CreateViewType`) ou particionamento (`CreatePType`). Consulte o [Orientador de otimização do mecanismo de banco de dados esquema XML](https://schemas.microsoft.com/sqlserver/) para obter informações sobre esses outros `Create` tipos de elemento.  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivo de entrada XML com configuração especificada pelo usuário (DTA)](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
