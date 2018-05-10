---
title: Origem do arquivo HDFS | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hdfsfilesrc.f1
ms.assetid: f8cda200-c389-4a2e-8ee9-5d59b326aac1
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d4f3866b56645b9e484f07ac775f4b642defc5d0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="hdfs-file-source"></a>Origem do arquivo HDFS
  O componente de origem do arquivo HDFS permite que um pacote do SSIS leia dados de um arquivo HDFS. Os formatos de arquivo com suporte são texto e Avro. (Não há suporte para fontes de dados ORC.)  
  
 Para configurar a origem do arquivo HDFS, arraste e solte o arquivo de origem HDFS no designer de fluxo de dados e clique duas vezes no componente para abrir o editor.  
  
 ![Editor de origem do arquivo HDFS](../../integration-services/data-flow/media/hdfs-file-source.png "Editor de origem do arquivo HDFS")  
  
## <a name="options"></a>Opções  
 Configure as seguintes opções na guia **Geral** da caixa de diálogo **Editor de Origem de Arquivo Hadoop** .  
  
|Campo|Description|  
|-----------|-----------------|  
|**Conexão do Hadoop**|Especifique um gerenciador de conexões do Hadoop existente ou crie um novo. Esse gerenciador de conexões indica onde os arquivos HDFS estão hospedados.|  
|**Caminho do Arquivo**|Especifique o nome do arquivo HDFS.|  
|**Formato do arquivo**|Especifique o formato do arquivo HDFS. As opções disponíveis são Texto e Avro. (Não há suporte para fontes de dados ORC.)|  
|**Caractere delimitador de coluna**|Se você selecionar o formato Texto, especifique o caractere delimitador de coluna.|  
|**Nomes de coluna na primeira linha de dados**|Se você selecionar o formato Texto, indique se a primeira linha no arquivo conterá nomes de coluna.|  
  
 Depois de configurar essas opções, selecione a guia **Colunas** para mapear colunas de origem para colunas de destino no fluxo de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de conexões do Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Destino de Arquivo HDFS](../../integration-services/data-flow/hdfs-file-destination.md)  
  
  
