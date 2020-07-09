---
title: Gerenciar espaços para tabela Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], managing tablespaces
- tablespaces [SQL Server replication]
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e6f969ef7b006c6ccf3f24668322fe55c00511c4
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893300"
---
# <a name="manage-oracle-tablespaces"></a>Gerenciar espaços de tabela Oracle
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Um espaço de tabela é uma unidade de armazenamento de banco de dados que é aproximadamente equivalente a um grupo de arquivo no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os espaços de tabela permitem armazenamento e gerenciamento de objetos de banco de dados dentro de grupos individuais. Para obter mais informações, consulte a documentação Oracle.  
  
 Ao configurar uma tabela como parte de uma publicação Oracle, você pode especificar opcionalmente um espaço de tabela do Oracle existente para ser usado ao armazenar informações de log de replicação. Se não especificado, o espaço de tabela para os objetos de replicação é o espaço de tabela padrão associado com o esquema de usuário administrativo de replicação que foi configurado ao se configurar o Publicador.  
  
 **Para especificar um espaço de tabela para uma tabela de log de artigo**:  
  
-   Especifique um espaço de tabela na caixa de diálogo **Propriedades de Artigo** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Use [sp_changearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Para usar **sp_changearticle**, especifique o seguinte:  
  
    -   O nome do Publicador Oracle no parâmetro **\@publisher**.  
  
    -   O nome da publicação da Oracle no parâmetro **\@publication**.  
  
    -   O nome do artigo no parâmetro **\@article**.  
  
    -   Um valor igual a 'tablespace' no parâmetro **\@property**.  
  
    -   O nome do espaço de tabela no parâmetro **\@value**.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar um Publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Objetos criados no Publicador Oracle](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)  
  
  
