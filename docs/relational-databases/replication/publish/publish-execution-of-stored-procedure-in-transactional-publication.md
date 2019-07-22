---
title: Publicar a execução do procedimento armazenado na publicação transacional | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- stored procedures [SQL Server replication], publishing
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8a0f0333989b44ffcfad86233313d7f4b3e8768e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934310"
---
# <a name="publish-execution-of-stored-procedure-in-transactional-publication"></a>Publicar a execução do procedimento armazenado na publicação transacional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifique que a execução de um procedimento armazenado (em vez de apenas sua definição) deve ser publicada na caixa de diálogo **Propriedades do Artigo – \<Artigo>** . Essa caixa de diálogo está disponível no Assistente para Nova Publicação e na caixa de diálogo **Propriedades da Publicação – \<Publicação>** . Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
 A definição do procedimento (instrução CREATE PROCEDURE) será replicada para o Assinante quando a inscrição for inicializada. Quando o procedimento armazenado for executado no Publicador, a replicação executará o procedimento correspondente no Assinante.  
  
### <a name="to-publish-the-execution-of-a-stored-procedure"></a>Para publicar a execução de um procedimento armazenado  
  
1.  Na página **Artigos** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , selecione um procedimento armazenado.  
  
2.  Clique em **Propriedade de Artigo**, depois em **Definir Propriedades de Procedimento Armazenado Realçado**.  
  
3.  Na caixa de diálogo **Propriedades do Artigo – \<Artigo>** , especifique um dos seguintes valores para a opção **Replicar**:  
  
    -   **Execução do procedimento armazenado**  
  
    -   **Execução em uma transação serializável do SP**  
  
         Essa é a opção recomendada, uma vez que ela replica a execução do procedimento apenas se o procedimento for executado dentro do contexto de uma transação serializável. Se o procedimento armazenado for executado fora de uma transação serializável, as alterações dos dados nas tabelas publicadas serão replicadas como uma série de instruções DML (Data Manipulation Language).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , clique em **OK** para salvar e fechar a caixa de diálogo.  
  
## <a name="see-also"></a>Consulte Também  
 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  
