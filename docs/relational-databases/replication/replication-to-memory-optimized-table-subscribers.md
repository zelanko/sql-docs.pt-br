---
title: "Replicação para assinantes de tabela com otimização de memória | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1a8e6bc7-433e-471d-b646-092dc80a2d1a
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 38b426bdc8e0485bdbada8c9dbd7371b63612465
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="replication-to-memory-optimized-table-subscribers"></a>Replicação para assinantes de tabela com otimização de memória
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  As tabelas que atuam como assinantes de replicação transacional e de instantâneo, com exceção da replicação transacional Ponto a Ponto, podem ser configuradas como tabelas com otimização de memória. Outras configurações de replicação não são compatíveis com tabelas com otimização de memória. Este recurso está disponível a partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
## <a name="two-configurations-are-required"></a>São necessárias duas configurações  
  
-   **Configurar o banco de dados do assinante para oferecer suporte à replicação de tabelas com otimização de memória**  
  
     Defina a propriedade **@memory_optimized** para **true** usando [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) ou [sp_changesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md).  
  
-   **Configurar o artigo para oferecer suporte à replicação de tabelas com otimização de memória**  
  
     Defina a opção `@schema_option = 0x40000000000` para o artigo usando [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) ou [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md).  
  
#### <a name="to-configure-a-memory-optimized-table-as-a-subscriber"></a>Para configurar uma tabela com otimização de memória como um assinante  
  
1.  Crie uma publicação transacional. Para obter mais informações, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Adicione artigos à publicação. Para obter mais informações, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
     Se a configuração que usa o [!INCLUDE[tsql](../../includes/tsql-md.md)] set the **@schema_option** do **sp_addarticle** procedimento armazenado como   
    **0x40000000000**.  
  
3.  Na janela de propriedades do artigo, defina **Habilitar Otimização de memória** como **true**.  
  
4.  Inicie o trabalho do Agente de Instantâneo para gerar o instantâneo inicial para essa publicação. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
5.  Agora, crie uma nova assinatura. No **Assistente para Nova Assinatura** , defina a **Assinatura de Otimização de Memória** como **true**.  
  
 As tabelas com otimização de memória agora devem começar a receber atualizações do publicador.  
  
#### <a name="reconfigure-an-existing-transaction-replication"></a>Reconfigurar uma replicação de transação existente  
  
1.  Vá para propriedades de assinatura no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e defina **Assinatura de Otimização de Memória** como **true**. As alterações não são aplicadas até a assinatura ser reiniciada.  
  
     Se a configuração que usa o [!INCLUDE[tsql](../../includes/tsql-md.md)] definir o novo parâmetro **@memory_optimized** do **sp_addsubscription** como true.  
  
2.  Vá até as propriedades do artigo para uma publicação em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e defina a otimização **Habilitar memória** como true.  
  
     Se a configuração que usa o [!INCLUDE[tsql](../../includes/tsql-md.md)] set the **@schema_option** do **sp_addarticle** procedimento armazenado como   
    **0x40000000000**.  
  
3.  Tabelas com otimização de memória não dão suporte a índices clusterizados. Para que a replicação trate disto, convertendo-o para um índice não clusterizado no destino, defina **Converter índice clusterizado em não clusterizado para artigo com otimização de memória** como true.  
  
     Se a configuração que usa o [!INCLUDE[tsql](../../includes/tsql-md.md)] set the **@schema_option** do **sp_addarticle** procedimento armazenado como  **0x0000080000000000**.  
  
4.  Regenere o instantâneo.  
  
5.  Reinicialize a assinatura.  
  
## <a name="remarks-and-restrictions"></a>Limitações e restrições  
 Somente há suporte para a replicação transacional unidirecional. Não há suporte para a replicação transacional ponto a ponto.  
  
 Não é possível publicar as tabelas com otimização de memória.  
  
 As tabelas de replicação no distribuidor não podem ser configuradas como tabelas com otimização de memória.  
  
 A replicação de mesclagem não pode incluir tabelas com otimização de memória.  
  
 No assinante, as tabelas envolvidas na replicação transacional podem ser configuradas como tabelas com otimização de memória, mas as tabelas do assinante devem atender aos requisitos de tabelas com otimização de memória. Isso requer as restrições a seguir.  
 
-   As tabelas replicadas nas tabelas com otimização de memória em um assinante estão limitadas a tipos de dados permitidos em tabelas com otimização de memória. Para obter mais informações, veja [Tipos de dados com suporte no OLTP in-memory](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md).  
  
-   Nem todos os recursos de Transact-SQL têm suporte com tabelas com otimização de memória. Consulte [Construtos Transact-SQL sem suporte no OLTP in-memory](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md) para ver mais detalhes.  
  
##  <a name="Schema"></a> Modificando um arquivo de esquema  
  
-   Se você estiver usando a opção de tabela com otimização de memória `DURABILITY = SCHEMA_AND_DATA` , a tabela deverá ter um índice de chave primária não clusterizado.  
  
-   ANSI_PADDING deve ser ON.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos e tarefas de replicação](../../relational-databases/replication/replication-features-and-tasks.md)  
  
  

