---
title: Questões do Database Evolution (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], multuser database changes
- database evolution [SQL Server]
ms.assetid: 1ed6ae10-d212-4ec2-8569-1b94ab1cba6d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d3a1f10ae77061983a5cf64ddd5a3462bb4be49b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63035585"
---
# <a name="issues-of-database-evolution-visual-database-tools"></a>Questões do Database Evolution (Visual Database Tools)
  Se você alterar a estrutura de um banco de dados implantado, tenha atenção especial para que sua alteração seja compatível com os dados e a estrutura de banco de dados existentes. Você pode precisar executar etapas especiais ao fazer as seguintes modificações:  
  
-   **Adicionar uma Restrição** Se você adicionar uma restrição, o banco de dados poderá já conter dados que não atendem às exigências. Quando você tentar salvar a nova restrição, a [Caixa de diálogo Notificações Pós-salvamento &#40;Visual Database Tools&#41;](visual-database-tools.md) o informará que o servidor de banco de dados não pode criar a restrição. Para forçar o banco de dados a aceitar a nova restrição, você pode desmarcar a caixa de seleção **Verificar dados existentes na criação**.  
  
-   **Adicionar uma Relação** Se você adicionar uma relação, o banco de dados poderá já conter linhas da tabela de chave estrangeira que não têm linhas correspondentes na tabela de chave primária. Isto é, os dados existentes podem não satisfazer a integridade referencial. Quando você tentar salvar a nova relação, a [Caixa de diálogo Notificações Pós-salvamento &#40;Visual Database Tools&#41;](visual-database-tools.md) o informará que o servidor de banco de dados não pode salvar a tabela de chave estrangeira revisada. Para forçar o banco de dados a aceitar a modificação, você pode desmarcar a caixa de seleção **Verificar dados existentes na criação**.  
  
-   **Modificar uma Tabela que Contribui para uma Exibição Indexada** Se você modificar uma tabela que contribui para uma exibição indexada do Microsoft SQL Server, os índices serão perdidos na exibição. Consulte os Manuais Online do SQL Server para obter informações sobre como recriar índices.  
  
-   **Excluir um Objeto** Se você excluir um objeto, como uma coluna, tabela ou exibição, verifique primeiro se o objeto não representa uma referência para outro objeto no banco de dados.  
  
 Você deve manter um histórico das alterações independentemente de como o design do banco de dados é alterado. Uma opção é manter os scripts SQL de todas as modificações que você já fez em seu banco de dados de produção.  
  
## <a name="see-also"></a>Consulte também  
 [As restrições UNIQUE e restrições de verificação](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [Ambientes multiusuários &#40;Visual Database Tools&#41;](multiuser-environments-visual-database-tools.md)  
  
  
