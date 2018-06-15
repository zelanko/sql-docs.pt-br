---
title: Administrar uma topologia ponto a ponto (programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- transactional replication, peer-to-peer replication
ms.assetid: 4d0fa941-f9ea-4a14-aed9-34df593fc6f2
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a6555cb74774b3c883580da305f66552a1ca7bf9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32954961"
---
# <a name="administer-a-peer-to-peer-topology-replication-transact-sql-programming"></a>Administrar uma topologia ponto a ponto (Programação Transact-SQL de replicação)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A administração de uma topologia ponto a ponto é semelhante à administração de uma topologia de replicação transacional comum, porém, há algumas áreas com considerações especiais. A diferença principal na administração da topologia ponto a ponto é que algumas alterações exigem que o sistema seja *confirmado*. Fechar um sistema para novas sessões envolve parar as atividades em tabelas publicadas em todos os nós e garantir que todos os nós tenham recebido todas as alterações de todos os demais nós. Para obter mais informações, consulte [Como confirmar uma topologia de replicação &#40;Programação Transact-SQL de replicação&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
> [!NOTE]  
>  Em uma topologia ponto a ponto, o distribuidor não pode estar usando uma versão anterior do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de um assinante de pull.  
  
### <a name="to-add-an-article-to-an-existing-configuration"></a>Para adicionar um artigo a uma configuração existente  
  
1.  Confirme o sistema.  
  
2.  Pare o Distribution Agent em cada nó na topologia. Para obter mais informações, consulte [Conceitos Executáveis do Agente de Replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) ou [Iniciar e Parar um Agente de Replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
3.  Execute a instrução CREATE TABLE para adicionar a nova tabela em cada nó na topologia.  
  
4.  Copie manualmente os dados em massa da nova tabela em todos os nós usando a [utilidade bcp](../../../tools/bcp-utility.md).  
  
5.  Execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) para criar um novo artigo em cada nó na topologia. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Depois que [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) é executado, a replicação adiciona automaticamente o artigo às assinaturas na topologia.  
  
6.  Reinicialize os Distribution Agents em cada nó na topologia.  
  
### <a name="to-make-schema-changes-to-a-publication-database"></a>Para efetuar alterações de esquema em um banco de dados de publicação  
  
1.  Confirme o sistema.  
  
2.  Execute as instruções de linguagem de definição de dados (DDL) para modificar o esquema das tabelas publicadas. Para obter mais informações sobre alterações de esquema com suporte, consulte [Fazer alterações de esquema em bancos de dados de publicação](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
3.  Antes de retomar a atividade nas tabelas publicadas, confirme o sistema novamente. Isto garante que as alterações de esquema foram recebidas por todos os nós antes que novas alterações de dados sejam replicadas.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como adicionar um novo artigo de tabela em uma topologia de replicação ponto a ponto existente que tenha dois nós.  
  
 [!code-sql[HowTo#sp_addp2particle_createtables](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_1.sql)]  
  
 [!code-sql[HowTo#sp_addp2particle_cmdline](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_2.sql)]  
  
 [!code-sql[HowTo#sp_addp2particle_createarticle](../../../relational-databases/replication/codesnippet/tsql/administer-a-peer-to-pee_3.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [Administração &#40;Replicação&#41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [Backup e Restauração de bancos de dados do SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Replicação transacional ponto a ponto](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
