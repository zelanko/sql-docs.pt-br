---
title: Propriedades personalizadas ADO NET | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e062a9ab-1e6b-4061-845a-4f8a0552b09d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 77b941d4f1460b81acf2e90185f6e1a4d9ecbde9
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277515"
---
# <a name="ado-net-custom-properties"></a>Propriedades personalizadas do ADO NET
  **Propriedades personalizadas de fontes**  
  
 A origem do ADO NET tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da origem do ADO NET. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|CommandTimeOut|Cadeia de caracteres|Um valor que especifica quanto segundos faltam para que o comando SQL expire. Um valor de 0 indica que o comando nunca expirará.|  
|SqlCommand|Cadeia de caracteres|A instrução SQL usada pela origem do ADO NET para extrair dados.<br /><br /> Quando o pacote é carregado, é possível atualizar esta propriedade de forma dinâmica com a instrução SQL que será usada pela origem do ADO NET. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md) e [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md).|  
|AllowImplicitStringConversion|Booliano|Um valor que indica se o seguinte acontece:<br /><br /> -Nenhuma geração de erro de validação se não houver correspondência entre tipos de metadados externos e tipos de coluna de saída que são cadeias de caracteres (DT_WSTR ou DT_NTEXT).<br /><br /> -Conversão implícita de tipos de metadados externos para o tipo de dados String usado pela coluna de saída.<br /><br /> <br /><br /> O valor padrão é TRUE.<br /><br /> Para obter mais informações, consulte [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).|  
  
 A saída e as colunas de saída da origem do ADO NET não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Propriedades personalizadas de destino**  
  
 O destino [!INCLUDE[vstecado](../../includes/vstecado-md.md)] tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino [!INCLUDE[vstecado](../../includes/vstecado-md.md)] . Todas as propriedades são de leitura/gravação. Essas propriedades não estão disponíveis no **Editor de Destino ADO NET**, mas podem ser definidas com o **Editor Avançado**.  
  
|Propriedade|Tipo de Dados|Descrição|  
|--------------|---------------|-----------------|  
|BatchSize|Integer|O número de linhas em um lote enviado ao servidor. O valor **0** indica que o tamanho do lote corresponde ao tamanho do buffer interno. O valor padrão dessa propriedade é **0**.|  
|CommandTimeOut|Integer|O número máximo de segundos em que o comando SQL pode ser executado antes que o tempo limite seja excedido. O valor **0** indica que não há limite de tempo. O valor padrão dessa propriedade é **0**.|  
|TableOrViewName|Cadeia de caracteres|O nome da tabela ou exibição de destino.|  
  
 Para obter mais informações, consulte [ADO NET Destination](../../integration-services/data-flow/ado-net-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
