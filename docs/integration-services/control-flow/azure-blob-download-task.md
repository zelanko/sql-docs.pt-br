---
title: Tarefa de Download do Blob do Azure | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobdltask.f1
- sql14.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fc83e4d8e39c5521fd897ceeec07755f62b5765d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294323"
---
# <a name="azure-blob-download-task"></a>Tarefa de Download do Blob do Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


A Tarefa de Download do Blob do Azure permite que um pacote SSIS baixe arquivos de um armazenamento de blob do Azure.

Para adicionar uma **Tarefa de Download de Blobs do Azure**, arraste-a e solte-a no Designer SSIS, e clique duas vezes ou com o botão direito do mouse em **Editar** para ver a caixa de diálogo **Editor da Tarefa de Download de Blobs do Azure** .  
  
 A **Tarefa de Download do Blob do Azure** é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para o Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
 A tabela a seguir fornece uma descrição para os campos nessa caixa de diálogo.  

|**Campo**|**Descrição**|  
|---|---|
|AzureStorageConnection|Especifique um Gerenciador de Conexão de Armazenamento do Azure existente ou crie um novo referindo-se a uma Conta de Armazenamento do Azure, que aponta para onde os arquivos de blob estão hospedados.|  
|BlobContainer|Especifica o nome do contêiner de Blob que contém os arquivos de Blob a serem baixados.|  
|BlobDirectory|Especifica o diretório de Blob que contém os arquivos de Blob a serem baixados. O diretório de Blob é uma estrutura hierárquica virtual.|  
|SearchRecursively|Especifica se é necessário pesquisar recursivamente dentro dos subdiretórios.|  
|LocalDirectory|Especifica o diretório local em que os arquivos de blob baixados são armazenados.|  
|FileName|Especifica um filtro de nome para selecionar arquivos com o padrão de nome especificado. Por exemplo, `MySheet*.xls\*` inclui arquivos como `MySheet001.xls` e `MySheetABC.xlsx`.|  
|TimeRangeFrom/TimeRangeTo|Especifica um filtro de intervalo de tempo. Arquivos modificados após **TimeRangeFrom** e antes de **TimeRangeTo** são incluídos.|  
