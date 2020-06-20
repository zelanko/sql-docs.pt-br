---
title: Publicar a execução de um procedimento armazenado em uma publicação transacional (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- stored procedures [SQL Server replication], publishing
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a226d7c58b3b72caf415d8e873b58ca38d3c749f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060424"
---
# <a name="publish-the-execution-of-a-stored-procedure-in-a-transactional-publication-sql-server-management-studio"></a>Publicar a execução de um procedimento armazenado em uma publicação transacional (SQL Server Management Studio)
  Especifique que a execução de um procedimento armazenado (em vez de apenas sua definição) deve ser publicada na caixa de diálogo **Propriedades do artigo – \<Article> ** . Essa caixa de diálogo está disponível no Assistente para nova publicação e na caixa de diálogo **Propriedades da publicação – \<Publication> ** . Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](create-a-publication.md) e [Exibir e modificar as propriedades da publicação](view-and-modify-publication-properties.md).  
  
 A definição do procedimento (instrução CREATE PROCEDURE) será replicada para o Assinante quando a inscrição for inicializada. Quando o procedimento armazenado for executado no Publicador, a replicação executará o procedimento correspondente no Assinante.  
  
### <a name="to-publish-the-execution-of-a-stored-procedure"></a>Para publicar a execução de um procedimento armazenado  
  
1.  Na página **artigos** do assistente para nova publicação ou na caixa de diálogo **Propriedades \<Publication> da publicação –** , selecione um procedimento armazenado.  
  
2.  Clique em **Propriedade de Artigo**, depois em **Definir Propriedades de Procedimento Armazenado Realçado**.  
  
3.  Na caixa de diálogo **Propriedades \<Article> do artigo –** , especifique um dos seguintes valores para a opção **replicar** :  
  
    -   **Execução do procedimento armazenado**  
  
    -   **Execução em uma transação serializável do SP**  
  
         Essa é a opção recomendada, uma vez que ela replica a execução do procedimento apenas se o procedimento for executado dentro do contexto de uma transação serializável. Se o procedimento armazenado for executado fora de uma transação serializável, as alterações dos dados nas tabelas publicadas serão replicadas como uma série de instruções DML (Data Manipulation Language).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se você estiver na caixa de diálogo **Propriedades \<Publication> da publicação –** , clique em **OK** para salvar e fechar a caixa de diálogo.  
  
## <a name="see-also"></a>Consulte Também  
 [Publicando a execução de procedimento armazenado na replicação transacional](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  
