---
title: Propriedades personalizadas da origem XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2646a9e3a5387b63d5d5784f67d4613adb22266d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201776"
---
# <a name="xml-source-custom-properties"></a>Propriedades personalizadas da origem XML
  A origem XML contém propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da origem XML. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|O modo usado para acessar os dados XML.|  
|UseInlineSchema|Booliano|Um valor que indica se deve ser usada uma definição de esquema embutido dentro da origem XML. O valor padrão dessa propriedade é `False`.|  
|XMLData|Cadeia de caracteres|O arquivo ou variáveis dos quais é possível recuperar os dados XML.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
|XMLSchemaDefinition|Cadeia de caracteres|O caminho e nome de arquivo do arquivo de definição de esquema (.xsd).<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
  
 A tabela a seguir descreve as propriedades personalizadas da saída da origem XML. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Description|  
|-------------------|---------------|-----------------|  
|RowsetID|Cadeia de caracteres|Um valor que identifica o conjunto de linhas associado à saída.|  
  
 As colunas de saída da origem XML não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [XML Source](xml-source.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades comuns](../common-properties.md)  
  
  
