---
title: "Gerenciar espa&#231;os de tabela Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "publicação Oracle [replicação do SQL Server], mapeamento de espaços de tabela"
  - "espaços de tabela [Replicação do SQL Server]"
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Gerenciar espa&#231;os de tabela Oracle
  Um espaço de tabela é uma unidade de armazenamento de banco de dados que é aproximadamente equivalente a um grupo de arquivos em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os espaços de tabela permitem armazenamento e gerenciamento de objetos de banco de dados dentro de grupos individuais. Para obter mais informações, consulte a documentação Oracle.  
  
 Ao configurar uma tabela como parte de uma publicação Oracle, você pode especificar opcionalmente um espaço de tabela do Oracle existente para ser usado ao armazenar informações de log de replicação. Se não especificado, o espaço de tabela para os objetos de replicação é o espaço de tabela padrão associado com o esquema de usuário administrativo de replicação que foi configurado ao se configurar o Publicador.  
  
 **Para especificar um espaço de tabela para uma tabela de log de artigo**:  
  
-   Especificar um espaço de tabela no **Propriedades do artigo** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Use [sp_changearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Usar **sp_changearticle**, especifique o seguinte:  
  
    -   O nome do editor Oracle para o parâmetro **@publisher**.  
  
    -   O nome da publicação Oracle para o parâmetro **@publication**.  
  
    -   O nome do artigo para o parâmetro **@article**.  
  
    -   Um valor de 'espaço de tabela' para o parâmetro **@property**.  
  
    -   O nome do espaço de tabela para o parâmetro **@value**.  
  
## Consulte também  
 [Configurar um publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Objetos criados no Editor Oracle](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)  
  
  