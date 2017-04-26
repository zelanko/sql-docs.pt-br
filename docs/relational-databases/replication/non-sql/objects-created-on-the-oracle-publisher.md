---
title: Objetos criados no Publicador Oracle | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], objects created
ms.assetid: c58a124b-4da7-46e2-9292-af8ce9e6664b
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 97a45c8f524f81d01dceda7a616932b18e799d82
ms.lasthandoff: 04/11/2017

---
# <a name="objects-created-on-the-oracle-publisher"></a>Objetos criados no Editor Oracle
  A replicação do[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala objetos de banco de dados no Editor Oracle para habilitar controle e encaminhamento de alterações (o[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não instala nenhum arquivo binário no Editor Oracle). A tabela seguinte lista os objetos que são criados no Editor Oracle quando este é identificado como um Publicador no Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . As descrições de objeto são fornecidas apenas para fins informativos. Esses objetos não devem ser modificados.  
  
|Nome do Objeto|Tipo de objeto|Descrição|  
|-----------------|-----------------|-----------------|  
|HREPL_ArticleNlog_V|Table|Tabela de controle de alterações usada para armazenar informações à medida que são feitas alterações à tabela publicada. É criada uma tabela de controle de alterações para cada tabela publicada.|  
|HREPL_Changes|Table|Tabela usada internamente pelo trabalho Xactset para determinar o número de alterações que aguardam ser atribuídas a um conjunto de transações. Para obter mais informações sobre esse trabalho, consulte [Ajuste de desempenho para Publicadores Oracle](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md).|  
|HREPL_Distributor|Table|Tabela de status de Distribuidor usada para manter informações sobre o Distribuidor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] associado ao Editor Oracle.|  
|HREPL_Event|Table|Tabela de eventos usada para sincronizar instantâneos e solicitações de número de linhas.|  
|HREPL_Mutex|Table|Tabela usada para assegurar que o procedimento PopulatePollTable de pacote Oracle não seja executado ao mesmo tempo pelo Log Reader Agent e pelo trabalho do banco de dados.|  
|HREPL_Poll|Table|Tabela usada para identificar entradas de tabela de log associadas com conjuntos de alterações a tabelas publicadas.|  
|HREPL_PublishedTables|Table|Tabela que contém uma entrada para cada artigo em uma publicação transacional.|  
|HREPL_Publisher|Table|Tabela de status do Publicador usada para manter informações específicas do Publicador.|  
|HREPL_SchemaFilter|Table|Tabela que contém esquemas que não são exibidos ao publicar por meio do Assistente de Nova Publicação.|  
|HREPL_XactsetCreateTimes|Table|Tabela que identifica o momento de criação associado a cada conjunto de transações.|  
|HREPL_XactsetJob|Table|Tabela com configurações de parâmetro atuais para o trabalho Xactset.|  
|HREPL_Pollid|Sequência|Sequência usada para gerar identificações de sondagem.|  
|HREPL_Seq|Sequência|Sequência usada para ordenar comandos de alteração.|  
|HREPL_Stmt|Sequência|Sequência usada para gerar identificações de instrução.|  
|HREPL|Pacote e corpo de pacote|Código de suporte a pacote de Publicador criado no Publicador.|  
|MSSQLSERVERDISTRIBUTOR|Sinônimo público|Sinônimo público para a tabela HREPL_Distributor. Se você configura um Distribuidor para usar com um Editor Oracle e esse sinônimo já existe no banco de dados, ele é descartado e recriado.<br /><br /> Descartar o sinônimo público e o usuário de replicação Oracle configurado usando a opção CASCADE remove todos os objetos de replicação do Editor Oracle.|  
|HREPL_Len_I_J_K|Função|Função definida fora do código de pacote de publicação Oracle, usada para consultar o comprimento de uma coluna LONG (usada ao gerar comandos com parâmetros para tabelas com colunas LONG publicadas). Uma função é criada para cada tabela publicada com uma coluna LONG.|  
|HREPL_DropPublisher|Procedimento|Procedimento definido fora do código de pacote de publicação Oracle, usado para descartar o Editor Oracle.|  
|HREPL_ExecuteCommand|Procedimento|Procedimento definido fora do código de pacote de publicação Oracle, usado para executar um comando no Publicador.|  
|HREPL_ArticleN_Trigger_Row|Gatilho|Gatilho gerado para cada tabela publicada, usado para controlar alterações de linha.|  
|HREPL_ArticleN_Trigger_Stmt|Gatilho|Gatilho gerado para cada tabela publicado, usado para controlar alterações de nível de instrução.|  
|HREPL_Article_I_J|Exibição|Exibição criada para cada tabela publicada, usada para consultar a tabela publicada.|  
|HREPL_Log_I_J_K|Exibição|Exibição criada para cada tabela publicada, usada para consultar a tabela de controle de alterações.|  
  
## <a name="see-also"></a>Consulte também  
 [Configurar um Publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Glossário de termos para publicações Oracle](../../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
