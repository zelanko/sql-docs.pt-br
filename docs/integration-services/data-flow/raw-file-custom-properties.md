---
description: Propriedades personalizadas de arquivo bruto
title: Propriedades personalizadas de arquivo bruto | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 45e439343713ac98dfd293a21af90d75e1275847
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457269"
---
# <a name="raw-file-custom-properties"></a>Propriedades personalizadas de arquivo bruto

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **Propriedades personalizadas de fontes**  
  
 A fonte Arquivo Bruto tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da fonte de Arquivo Bruto. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|AccessMode|Inteiro (enumeração)|O modo usado para acessar os dados brutos. Os valores possíveis são **Nome do arquivo** (0) e **Nome do arquivo da variável** (1). O valor padrão é **Nome do arquivo** (0).|  
|FileName|Cadeia de caracteres|O caminho e o nome do arquivo do arquivo de origem.|  
  
 A saída e as colunas de saída da fonte Arquivo Bruto não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Raw File Source](../../integration-services/data-flow/raw-file-source.md).  
  
 **Propriedades personalizadas de destino**  
  
 O destino Arquivo Bruto tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Arquivo Bruto. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|AccessMode|Inteiro (enumeração)|Um valor que especifica se a propriedade FileName contém um nome de arquivo ou o nome de uma variável que contenha um nome de arquivo. As opções são **Nome do arquivo** (0) e **Nome do arquivo da variável** (1).|  
|FileName|Cadeia de caracteres|O nome do arquivo no qual o destino Arquivo Bruto grava.|  
|WriteOption|Inteiro (enumeração)|Um valor que especifica se o destino Arquivo Bruto exclui um arquivo existente de mesmo nome. As opções são **Criar sempre** (0), **Criar uma vez** (1), **Truncar e acrescentar** (3) e **Acrescentar** (2). O valor padrão dessa propriedade é **Criar sempre** (0).|  
  
> [!NOTE]  
>  Uma operação de acréscimo requer que os metadados dos dados acrescentados correspondam aos metadados dos dados já existentes no arquivo.  
  
 A entrada e as colunas de entrada do destino Arquivo Bruto não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
