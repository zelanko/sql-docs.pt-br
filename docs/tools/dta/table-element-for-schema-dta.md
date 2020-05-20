---
title: Elemento de tabela para esquema (DTA)
description: No utilitário dta, o elemento Tabela de Schema especifica a tabela do ajuste. Este artigo descreve esse elemento.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Table element [DTA]
ms.assetid: a59e8319-05d1-47f3-af39-7d970ab8e7dc
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: c7c6e1c260d91f5c835117463ac82495ec7873f8
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83151519"
---
# <a name="table-element-for-schema-dta"></a>Elemento de tabela para esquema (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Especifica a tabela para ajuste.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Schema>  
...code removed here...  
    <Table>...</Table>  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|**NumberOfRows**|Opcional. Inteiro que permite simular tabelas de tamanhos diferentes.|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, entre 1 e 255 caracteres.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Lista tantas tabelas quanto for apropriado para sua carga de trabalho.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Schema para Database &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
|**Elementos filho**|[Elemento Name para Table &#40;DTA&#41;](../../tools/dta/name-element-for-table-dta.md)|  
  
## <a name="remarks"></a>Comentários  
 Se você não especificar um elemento **Table** , o Orientador de Otimização do Mecanismo de Banco de Dados assumirá que todas as tabelas no banco de dados especificado podem ser ajustadas.  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso, veja [Elemento Server&#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
