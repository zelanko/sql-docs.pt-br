---
title: Propriedades personalizadas de arquivo bruto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 38acf6fd70bebf5033fde5dcf33fe5b2a6ac6722
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754818"
---
# <a name="raw-file-custom-properties"></a>Propriedades personalizadas de arquivo bruto
  **Propriedades personalizadas de fontes**  
  
 A fonte Arquivo Bruto tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da fonte de Arquivo Bruto. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|AccessMode|Inteiro (enumeração)|O modo usado para acessar os dados brutos. Os valores possíveis são `File name` (0) e `File name from variable` (1). O valor padrão é `File name` (0).|  
|FileName|Cadeia de caracteres|O caminho e o nome do arquivo do arquivo de origem.|  
  
 A saída e as colunas de saída da fonte Arquivo Bruto não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Raw File Source](raw-file-source.md).  
  
 **Propriedades personalizadas de destino**  
  
 O destino Arquivo Bruto tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Arquivo Bruto. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|AccessMode|Inteiro (enumeração)|Um valor que especifica se a propriedade FileName contém um nome de arquivo ou o nome de uma variável que contenha um nome de arquivo. As opções são `File name` (0) e `File name from variable` (1).|  
|FileName|Cadeia de caracteres|O nome do arquivo no qual o destino Arquivo Bruto grava.|  
|WriteOption|Inteiro (enumeração)|Um valor que especifica se o destino Arquivo Bruto exclui um arquivo existente de mesmo nome. As opções são `Create Always` (0), `Create Once` (1), `Truncate and Append` (3) e `Append` (2). O valor padrão dessa propriedade é `Create Always` (0).|  
  
> [!NOTE]  
>  Uma operação de acréscimo requer que os metadados dos dados acrescentados correspondam aos metadados dos dados já existentes no arquivo.  
  
 A entrada e as colunas de entrada do destino Arquivo Bruto não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Raw File Destination](raw-file-destination.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades comuns](../common-properties.md)  
  
  
