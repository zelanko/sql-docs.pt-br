---
title: "Gerenciar espaços para tabela Oracle | Microsoft Docs"
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
- Oracle publishing [SQL Server replication], managing tablespaces
- tablespaces [SQL Server replication]
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6eaa6d1c6836cee6d8367e0c0893b3f8a73184f3
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="manage-oracle-tablespaces"></a>Gerenciar espaços de tabela Oracle
  Um espaço para tabela é uma unidade de armazenamento de banco de dados que é aproximadamente equivalente a um grupo de arquivo no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os espaços de tabela permitem armazenamento e gerenciamento de objetos de banco de dados dentro de grupos individuais. Para obter mais informações, consulte a documentação Oracle.  
  
 Ao configurar uma tabela como parte de uma publicação Oracle, você pode especificar opcionalmente um espaço de tabela do Oracle existente para ser usado ao armazenar informações de log de replicação. Se não especificado, o espaço de tabela para os objetos de replicação é o espaço de tabela padrão associado com o esquema de usuário administrativo de replicação que foi configurado ao se configurar o Publicador.  
  
 **Para especificar um espaço de tabela para uma tabela de log de artigo**:  
  
-   Especifique um espaço de tabela na caixa de diálogo **Propriedades de Artigo** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Use [sp_changearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Para usar **sp_changearticle**, especifique o seguinte:  
  
    -   O nome do Editor Oracle para o parâmetro **@publisher**.  
  
    -   O nome da publicação Oracle para o parâmetro **@publication**.  
  
    -   O nome do artigo para o parâmetro **@article**.  
  
    -   Um valor de 'espaço de tabela' para o parâmetro **@property**.  
  
    -   O nome do espaço de tabela para o parâmetro **@value**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar um Publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Objects Created on the Oracle Publisher](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)  
  
  
