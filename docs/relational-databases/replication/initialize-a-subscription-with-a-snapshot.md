---
title: "Inicializar uma assinatura com um instantâneo | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 85768c39b282ccfda1df1e68d42a1f6b3985bc46
ms.lasthandoff: 04/11/2017

---
# <a name="initialize-a-subscription-with-a-snapshot"></a>Inicializar uma assinatura com um instantâneo
  Após uma publicação ter sido criada, um instantâneo inicial é tipicamente criado e copiado para a pasta de instantâneo (isso acontece por padrão para publicações de mesclagem criadas com o Assistente para Novas Publicações). Isso é então aplicado ao Assinante pelo Agente de Distribuição (para publicações transacionais e instantâneas) ou o Agente de Mesclagem (para publicações de mesclagem) durante a sincronização inicial da assinatura. O processo de instantâneo depende do tipo de publicação:  
  
-   Se o instantâneo destinar-se a uma publicação instantânea, a uma publicação transacional ou a uma publicação de mesclagem que não use filtros com parâmetros, o instantâneo conterá o esquema e os dados em arquivos do BPC (programa de cópia em massa), assim como restrições, propriedades estendidas, índices, gatilhos e tabelas de sistema necessárias para a replicação. Para mais informações sobre criação e aplicação do instantâneo, consulte [Criar e aplicar o instantâneo](../../relational-databases/replication/create-and-apply-the-snapshot.md).  
  
-   Se o instantâneo for uma publicação de mesclagem que usa filtros com parâmetros, o instantâneo será criado usando um processo de duas partes. Primeiro é criado um instantâneo do esquema que contém os scripts de replicação e o esquema dos objetos publicados, mas não os dados. Cada assinatura é então inicializada com um instantâneo que inclui os scripts e o esquema copiados do instantâneo do esquema e os dados pertencentes à partição de assinatura. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 O instantâneo consiste de arquivos diferentes que dependem do tipo de replicação e os artigos em sua publicação. Esses arquivos são copiados para a pasta padrão de instantâneo quando o Distribuidor foi configurado ou para uma pasta alternativa de instantâneo especificada quando a publicação foi criada.  
  
|Tipo de replicação|Arquivos comuns de instantâneo|  
|-------------------------|---------------------------|  
|Replicação de instantâneo ou replicação transacional|esquema (.sch); dados (.bcp); restrições e índices (.dri); restrições (.idx); gatilhos (.trg): para atualizar só os Assinantes; arquivos de instantâneo compactados (.cab).|  
|Replicação de mesclagem|esquema (.sch); dados (.bcp); restrições e índices (.dri); gatilhos (.trg); dados da tabela do sistema (.sys); tabelas em conflito (.cft); arquivos de instantâneo compactados (.cab).|  
  
 Se uma transferência de instantâneo for interrompida, ela retomará automaticamente de onde parou e não reenviará nenhum arquivo que já tenha sido transferido completamente. A unidade de entrega para o Agente de Instantâneo é o arquivo bcp para cada artigo de publicação, então, os arquivos que são parcialmente entregues deverão ser reenviados completamente. Entretanto, continuar o instantâneo de onde parou pode reduzir significantemente a quantia de dados transmitidos e assegurar uma entrega de instantâneo a tempo mesmo se a conexão não for confiável.  
  
## <a name="snapshot-options"></a>Opções de instantâneo  
 Há várias opções disponíveis ao inicializar uma assinatura com um instantâneo. Você pode:  
  
-   Especificar um local alternativo para a pasta de instantâneo em vez do ou além do local da pasta de instantâneo padrão. Para obter mais informações, consulte [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
-   Compacte instantâneos para armazenamento em mídias removíveis ou para transferência em uma rede lenta. Para obter mais informações, consulte [Compressed Snapshots](../../relational-databases/replication/compressed-snapshots.md).  
  
-   Execute scripts de Transact-SQL antes ou depois que o instantâneo seja aplicado. Para mais informações, consulte [Executar scripts antes e depois da aplicação do instantâneo](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).  
  
-   Transfira arquivos de instantâneo usando o Protocolo de Transferência de Arquivo (FTP). Para obter mais informações, consulte [Transferir instantâneos pelo FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
## <a name="see-also"></a>Consulte também  
 [Inicializar uma assinatura](../../relational-databases/replication/initialize-a-subscription.md)   
 [Proteger a pasta de instantâneos](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
