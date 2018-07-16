---
title: Propriedades personalizadas ADO NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e062a9ab-1e6b-4061-845a-4f8a0552b09d
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 177e0cda681e81082e5b52fc324880f04a5d608c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37195626"
---
# <a name="ado-net-custom-properties"></a>Propriedades personalizadas do ADO NET
  **Propriedades personalizadas de fontes**  
  
 A origem do ADO NET tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da origem do ADO NET. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Description|  
|-------------------|---------------|-----------------|  
|CommandTimeOut|Cadeia de caracteres|Um valor que especifica quanto segundos faltam para que o comando SQL expire. Um valor de 0 indica que o comando nunca expirará.|  
|SqlCommand|Cadeia de caracteres|A instrução SQL usada pela origem do ADO NET para extrair dados.<br /><br /> Quando o pacote é carregado, é possível atualizar esta propriedade de forma dinâmica com a instrução SQL que será usada pela origem do ADO NET. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md) e [Usar expressões de propriedade em pacotes](../expressions/use-property-expressions-in-packages.md).|  
|AllowImplicitStringConversion|Booliano|Um valor que indica se o seguinte acontece:<br /><br /> Nenhuma geração de erro de validação se não houver correspondência entre tipos de metadados externos e tipos de coluna de saída que são cadeias de caracteres (DT_WSTR ou DT_NTEXT).<br /><br /> Conversão implícita de tipos de metadados externos para tipo de dados de cadeia de caracteres usado pela coluna de saída.<br /><br /> <br /><br /> O valor padrão é TRUE.<br /><br /> Para obter mais informações, consulte [ADO NET Source](ado-net-source.md).|  
  
 A saída e as colunas de saída da origem do ADO NET não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [ADO NET Source](ado-net-source.md).  
  
 **Propriedades personalizadas de destino**  
  
 O destino [!INCLUDE[vstecado](../../includes/vstecado-md.md)] tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino [!INCLUDE[vstecado](../../includes/vstecado-md.md)] . Todas as propriedades são de leitura/gravação. Essas propriedades não estão disponíveis no **Editor de Destino ADO NET**, mas podem ser definidas com o **Editor Avançado**.  
  
|Propriedade|Tipo de Dados|Description|  
|--------------|---------------|-----------------|  
|BatchSize|Integer|O número de linhas em um lote enviado ao servidor. O valor **0** indica que o tamanho do lote corresponde ao tamanho do buffer interno. O valor padrão dessa propriedade é **0**.|  
|CommandTimeOut|Integer|O número máximo de segundos em que o comando SQL pode ser executado antes que o tempo limite seja excedido. O valor **0** indica que não há limite de tempo. O valor padrão dessa propriedade é **0**.|  
|TableOrViewName|Cadeia de caracteres|O nome da tabela ou exibição de destino.|  
  
 Para obter mais informações, consulte [ADO NET Destination](ado-net-destination.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades comuns](../common-properties.md)  
  
  
