---
title: Inicializar uma assinatura com um instantâneo | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 3624d1eef64f10ae93802c4a7514fd54edcc0e74
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76287923"
---
# <a name="initialize-a-subscription-with-a-snapshot"></a>Inicializar uma assinatura com um instantâneo
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Após uma publicação ter sido criada, um instantâneo inicial é tipicamente criado e copiado para a pasta de instantâneo (isso acontece por padrão para publicações de mesclagem criadas com o Assistente para Novas Publicações). Isso é então aplicado ao Assinante pelo Agente de Distribuição (para publicações transacionais e instantâneas) ou o Agente de Mesclagem (para publicações de mesclagem) durante a sincronização inicial da assinatura. O processo de instantâneo depende do tipo de publicação:  
  
-   Se o instantâneo destinar-se a uma publicação instantânea, a uma publicação transacional ou a uma publicação de mesclagem que não use filtros com parâmetros, o instantâneo conterá o esquema e os dados em arquivos do BPC (programa de cópia em massa), assim como restrições, propriedades estendidas, índices, gatilhos e tabelas de sistema necessárias para a replicação. Para mais informações sobre criação e aplicação do instantâneo, consulte [Criar e aplicar o instantâneo](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
-   Se o instantâneo for uma publicação de mesclagem que usa filtros com parâmetros, o instantâneo será criado usando um processo de duas partes. Primeiro é criado um instantâneo do esquema que contém os scripts de replicação e o esquema dos objetos publicados, mas não os dados. Cada assinatura é então inicializada com um instantâneo que inclui os scripts e o esquema copiados do instantâneo do esquema e os dados pertencentes à partição de assinatura. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 O instantâneo consiste de arquivos diferentes que dependem do tipo de replicação e os artigos em sua publicação. Esses arquivos são copiados para a pasta padrão de instantâneo quando o Distribuidor foi configurado ou para uma pasta alternativa de instantâneo especificada quando a publicação foi criada.  
  
|Tipo de replicação|Arquivos comuns de instantâneo|  
|-------------------------|---------------------------|  
|Replicação de instantâneo ou replicação transacional|esquema (.sch); dados (.bcp); restrições e índices (.dri); restrições (.idx); gatilhos (.trg): para atualizar só os Assinantes; arquivos de instantâneo compactados (.cab).|  
|Replicação de mesclagem|esquema (.sch); dados (.bcp); restrições e índices (.dri); gatilhos (.trg); dados da tabela do sistema (.sys); tabelas em conflito (.cft); arquivos de instantâneo compactados (.cab).|  
  
 Se uma transferência de instantâneo for interrompida, ela retomará automaticamente de onde parou e não reenviará nenhum arquivo que já tenha sido transferido completamente. A unidade de entrega para o Agente de Instantâneo é o arquivo bcp para cada artigo de publicação, então, os arquivos que são parcialmente entregues deverão ser reenviados completamente. Entretanto, continuar o instantâneo de onde parou pode reduzir significantemente a quantia de dados transmitidos e assegurar uma entrega de instantâneo a tempo mesmo se a conexão não for confiável.  
  
## <a name="snapshot-options"></a>Opções de instantâneo  
 Há várias opções disponíveis ao inicializar uma assinatura com um instantâneo. Você pode:  
  
-   Especificar um local alternativo para a pasta de instantâneo em vez do ou além do local da pasta de instantâneo padrão. Para obter mais informações, confira [Modificar opções de instantâneo](../../relational-databases/replication/snapshot-options.md).  
  
-   Compacte instantâneos para armazenamento em mídias removíveis ou para transferência em uma rede lenta. Para obter mais informações, consulte [Compressed Snapshots](../../relational-databases/replication/snapshot-options.md#compressed-snapshots). 

-   Execute scripts de Transact-SQL antes ou depois que o instantâneo seja aplicado. Para mais informações, consulte [Executar scripts antes e depois da aplicação do instantâneo](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).  
  
-   Transfira arquivos de instantâneo usando o Protocolo de Transferência de Arquivo (FTP). Para obter mais informações, consulte [Transferir instantâneos pelo FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Inicializar uma assinatura](../../relational-databases/replication/initialize-a-subscription.md)   
 [Proteger a pasta de instantâneos](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
