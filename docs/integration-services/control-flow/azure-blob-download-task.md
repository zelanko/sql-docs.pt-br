---
title: Tarefa de Download do Blob do Azure | Microsoft Docs
ms.custom: 
ms.date: 07/25/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpblobdltask.f1
- sql14.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 95ea7de4600551cc994e82dd3408cb4ea608685c
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="azure-blob-download-task"></a>Tarefa de Download do Blob do Azure
A Tarefa de Download do Blob do Azure permite que um pacote SSIS baixe arquivos de um armazenamento de blob do Azure.

Para adicionar uma **Tarefa de Download do Blob do Azure**, arraste e solte-a no Designer SSIS e clique duas vezes ou com o botão direito do mouse e clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa de Download do Blob do Azure** a seguir.  
  
 O **a tarefa de Download de Blob do Azure** é um componente do [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
 A tabela a seguir fornece uma descrição para os campos nessa caixa de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Description**|  
|AzureStorageConnection|Especifique um Gerenciador de Conexão de Armazenamento do Azure existente ou crie um novo referindo-se a uma Conta de Armazenamento do Azure, que aponta para onde os arquivos de blob estão hospedados.|  
|BlobContainer|Especifica o nome do contêiner de Blob que contém os arquivos de Blob a serem baixados.|  
|BlobDirectory|Especifica o diretório de Blob que contém os arquivos de Blob a serem baixados. O diretório de Blob é uma estrutura hierárquica virtual.|  
|LocalDirectory|Especifica o diretório local onde os arquivos de blob baixados são armazenados.|  
|FileName|Especifica um filtro de nome para selecionar arquivos com o padrão de nome especificado. Por exemplo, `MySheet*.xls\*` inclui arquivos como `MySheet001.xls` e `MySheetABC.xlsx`.|  
|TimeRangeFrom/TimeRangeTo|Especifica um filtro de intervalo de tempo. Arquivos modificados após **TimeRangeFrom** e antes de **TimeRangeTo** são incluídos.|  
  
  

