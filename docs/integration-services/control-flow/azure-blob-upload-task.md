---
title: Tarefa de Upload do Blob do Azure | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobuptask.f1
- sql14.dts.designer.afpblobuptask.f1
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bdc915d459144cd2c745f0ca97df55380f819138
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947398"
---
# <a name="azure-blob-upload-task"></a>Tarefa de Carregamento de Blobs do Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


A **Tarefa de Upload de Blobs do Azure** permite que um pacote SSIS carregue arquivos para um armazenamento de blobs do Azure.
    
Para adicionar uma **Tarefa de Upload de Blobs do Azure**, arraste-a e solte-a no Designer SSIS, e clique duas vezes ou com o botão direito do mouse em **Editar** para ver a caixa de diálogo **Editor da Tarefa de Upload de Blobs do Azure** .  
  
 A **Tarefa de Upload de Blobs do Azure** é um componente do [SSIS (SQL Server Integration Services) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 A tabela a seguir fornece descrições para os campos nessa caixa de diálogo.  

|**Campo**|**Descrição**|  
|---|---|  
|AzureStorageConnection|Especifique um Gerenciador de Conexão de Armazenamento do Azure existente ou crie um novo referindo-se a uma Conta de Armazenamento do Azure, que aponta para onde os arquivos de blob estão hospedados.|  
|BlobContainer|Especifica o nome do contêiner de blobs que contém os arquivos carregados como blobs.|  
|BlobDirectory|Especifica o diretório de blob em que o arquivo carregado é armazenado como um blob de blocos. O diretório de Blob é uma estrutura hierárquica virtual. Se o blob já existir, ele será substituído.|  
|LocalDirectory|Especifique o diretório local que contém os arquivos a serem carregados.|  
|SearchRecursively|Especifique se é necessário pesquisar recursivamente dentro dos subdiretórios.|  
|FileName|Especifica um filtro de nome para selecionar arquivos com o padrão de nome especificado. Por exemplo, `MySheet*.xls\*` inclui arquivos como `MySheet001.xls` e `MySheetABC.xlsx`.|  
|TimeRangeFrom/TimeRangeTo|Especifica um filtro de intervalo de tempo. Arquivos modificados após **TimeRangeFrom** e antes de **TimeRangeTo** são incluídos.|  
