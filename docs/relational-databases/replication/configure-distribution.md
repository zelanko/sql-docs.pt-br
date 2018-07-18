---
title: Configurar a distribuição | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- remote Distributors [SQL Server replication]
- transactional replication, configuring distribution
- distribution databases [SQL Server replication], sizing
- Distributors [SQL Server replication], configuring
- distribution databases [SQL Server replication], about distribution databases
- distribution databases [SQL Server replication]
- merge replication [SQL Server replication], configuring distribution
ms.assetid: 94d52169-384e-4885-84eb-2304e967d9f7
caps.latest.revision: 44
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8020d133c6f0ea1025287846e7fc33e5686c1db0
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37352688"
---
# <a name="configure-distribution"></a>Configurar a distribuição
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O Distribuidor é um servidor que contém o banco de dados de distribuição, que armazena metadados e dados de histórico para todos os tipos de replicação e transações para replicação transacional. Para configurar a replicação, deve-se configurar um Distribuidor. Cada Publicador pode ser atribuído a uma única instância do Distribuidor, mas vários publicadores podem compartilhar um Distribuidor. O Distribuidor usa esses recursos adicionais no servidor onde fica localizado:  
  
-   Espaço em disco adicional, se os arquivos de instantâneo para a publicação forem armazenados no Distribuidor (o que geralmente acontece).  
  
-   Espaço em disco adicional para armazenar o banco de dados de distribuição.  
  
-   Uso de processador adicional por agentes de replicação para assinaturas push executadas no Distribuidor.  
  
 O servidor selecionado como Distribuidor deve ter espaço em disco adequado e potência no processador para dar suporte a replicação e a qualquer outra atividade naquele servidor. Ao configurar o Distribuidor, especifica-se o seguinte:  
  
-   Uma pasta de instantâneo usada, por padrão, para todos os Publicadores que usam esse Distribuidor. Certifique-se de que essa pasta já é compartilhada e tem as permissões apropriadas definidas. Para obter mais informações, consulte [Proteger a pasta de instantâneos](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
-   Um nome e locais de arquivo para o banco de dados de distribuição. O banco de dados de distribuição não pode ser renomeado depois de criado. Para usar um nome diferente para o banco de dados, deve-se desabilitar a distribuição e reconfigurá-la.  
  
-   Quaisquer Publicadores autorizados a usar o Distribuidor. Se você especificar Publicadores diferentes da instância em que o Distribuidor é executado, também deverá especificar uma senha para as conexões feitas pelo Publicador para o Distribuidor remoto.  
  
 Para replicação transacional, depois que configurar distribuição, recomendamos que você:  
  
-   Dimensione adequadamente o banco de dados de distribuição. Teste a replicação com uma carga típica para seu sistema para determinar a quantidade de espaço necessária para armazenar comandos. Certifique-se de que o banco de dados seja amplo o suficiente para armazenar comandos, sem ter que aumentá-lo frequentemente. Para obter mais informações sobre como alterar o tamanho de um banco de dados, consulte [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
-   Defina a opção **sync with backup** no banco de dados de distribuição. Para obter mais informações, consulte [Estratégias para fazer backup e restaurar o instantâneo e a replicação transacional](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md) e [Habilitar backups coordenados para a replicação transacional &#40;Programação Transact-SQL de replicação&#41;](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md).  
  
## <a name="local-and-remote-distributors"></a>Distribuidores locais e remotos  
 Por padrão, o Distribuidor é o mesmo servidor que o Publicador (um Distribuidor local), mas também pode ser um servidor separado do Publicador (um Distribuidor remoto). Normalmente, escolheria usar um Distribuidor remoto se você quiser:  
  
-   Processamento de offload para outro computador se você quiser impacto mínimo de replicação no Publicador (por exemplo, se o Publicador for um servidor OLTP).  
  
-   Configurar um Distribuidor centralizado para vários Publicadores.  
  
 Distribuidores remotos são mais comuns na replicação transacional do que na replicação de mesclagem por duas razões:  
  
-   O Distribuidor tem um papel maior na replicação transacional por que todas as transações replicadas são gravadas para e lidas de um banco de dados de distribuição.  
  
-   Topologias de replicação de mesclagem normalmente usam assinaturas pull, por isso agentes são executados para cada Assinante, em vez de serem todos executados no Distribuidor. Para obter mais informações, consulte [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md) (Assinar publicações). Na maioria dos casos, deve-se usar um Distribuidor local para replicação de mesclagem.  
  
 Para configurar publicação e distribuição, consulte [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
 Para modificar propriedades de Publicador e Distribuidor, consulte [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Proteger o Distribuidor](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  
