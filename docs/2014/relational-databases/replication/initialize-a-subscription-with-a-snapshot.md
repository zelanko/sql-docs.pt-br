---
title: Inicializar uma assinatura com um instantâneo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 23ad4cd92d186f43fb1a9dd81e1dbb0727170367
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131106"
---
# <a name="initialize-a-subscription-with-a-snapshot"></a>Inicializar uma assinatura com um instantâneo
  Após uma publicação ter sido criada, um instantâneo inicial é tipicamente criado e copiado para a pasta de instantâneo (isso acontece por padrão para publicações de mesclagem criadas com o Assistente para Novas Publicações). Isso é então aplicado ao Assinante pelo Agente de Distribuição (para publicações transacionais e instantâneas) ou o Agente de Mesclagem (para publicações de mesclagem) durante a sincronização inicial da assinatura. O processo de instantâneo depende do tipo de publicação:  
  
-   Se o instantâneo destinar-se a uma publicação instantânea, a uma publicação transacional ou a uma publicação de mesclagem que não use filtros com parâmetros, o instantâneo conterá o esquema e os dados em arquivos do BPC (programa de cópia em massa), assim como restrições, propriedades estendidas, índices, gatilhos e tabelas de sistema necessárias para a replicação. Para mais informações sobre criação e aplicação do instantâneo, consulte [Criar e aplicar o instantâneo](create-and-apply-the-snapshot.md).  
  
-   Se o instantâneo for uma publicação de mesclagem que usa filtros com parâmetros, o instantâneo será criado usando um processo de duas partes. Primeiro é criado um instantâneo do esquema que contém os scripts de replicação e o esquema dos objetos publicados, mas não os dados. Cada assinatura é então inicializada com um instantâneo que inclui os scripts e o esquema copiados do instantâneo do esquema e os dados pertencentes à partição de assinatura. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 O instantâneo consiste de arquivos diferentes que dependem do tipo de replicação e os artigos em sua publicação. Esses arquivos são copiados para a pasta padrão de instantâneo quando o Distribuidor foi configurado ou para uma pasta alternativa de instantâneo especificada quando a publicação foi criada.  
  
|Tipo de replicação|Arquivos comuns de instantâneo|  
|-------------------------|---------------------------|  
|Replicação de instantâneo ou replicação transacional|esquema (.sch); dados (.bcp); restrições e índices (.dri); restrições (.idx); gatilhos (.trg): para atualizar só os Assinantes; arquivos de instantâneo compactados (.cab).|  
|Replicação de mesclagem|esquema (.sch); dados (.bcp); restrições e índices (.dri); gatilhos (.trg); dados da tabela do sistema (.sys); tabelas em conflito (.cft); arquivos de instantâneo compactados (.cab).|  
  
 Se uma transferência de instantâneo for interrompida, ela retomará automaticamente de onde parou e não reenviará nenhum arquivo que já tenha sido transferido completamente. A unidade de entrega para o Agente de Instantâneo é o arquivo bcp para cada artigo de publicação, então, os arquivos que são parcialmente entregues deverão ser reenviados completamente. Entretanto, continuar o instantâneo de onde parou pode reduzir significantemente a quantia de dados transmitidos e assegurar uma entrega de instantâneo a tempo mesmo se a conexão não for confiável.  
  
## <a name="snapshot-options"></a>Opções de instantâneo  
 Há várias opções disponíveis ao inicializar uma assinatura com um instantâneo. Você pode:  
  
-   Especificar um local alternativo para a pasta de instantâneo em vez do ou além do local da pasta de instantâneo padrão. Para obter mais informações, consulte [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md).  
  
-   Compacte instantâneos para armazenamento em mídias removíveis ou para transferência em uma rede lenta. Para obter mais informações, consulte [Compressed Snapshots](compressed-snapshots.md).  
  
-   Execute scripts de Transact-SQL antes ou depois que o instantâneo seja aplicado. Para mais informações, consulte [Executar scripts antes e depois da aplicação do instantâneo](snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).  
  
-   Transfira arquivos de instantâneo usando o Protocolo de Transferência de Arquivo (FTP). Para obter mais informações, consulte [Transferir instantâneos pelo FTP](transfer-snapshots-through-ftp.md).  
  
## <a name="see-also"></a>Consulte também  
 [Inicializar uma assinatura](initialize-a-subscription.md)   
 [Proteger a pasta de instantâneos](security/secure-the-snapshot-folder.md)  
  
  
