---
title: Propriedades personalizadas da origem XML | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9acfe256755294f134decddc31a7cbb9c7966f78
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="xml-source-custom-properties"></a>Propriedades personalizadas da origem XML
  A origem XML contém propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da origem XML. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|O modo usado para acessar os dados XML.|  
|UseInlineSchema|Booliano|Um valor que indica se deve ser usada uma definição de esquema embutido dentro da origem XML. O valor padrão dessa propriedade é **False**.|  
|XMLData|Cadeia de caracteres|O arquivo ou variáveis dos quais é possível recuperar os dados XML.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
|XMLSchemaDefinition|Cadeia de caracteres|O caminho e nome de arquivo do arquivo de definição de esquema (.xsd).<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
  
 A tabela a seguir descreve as propriedades personalizadas da saída da origem XML. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Description|  
|-------------------|---------------|-----------------|  
|RowsetID|Cadeia de caracteres|Um valor que identifica o conjunto de linhas associado à saída.|  
  
 As colunas de saída da origem XML não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [XML Source](../../integration-services/data-flow/xml-source.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
