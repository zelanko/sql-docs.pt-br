---
title: Definir um banco de dados como modo de usuário único | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- single-user mode [SQL Server], database option
ms.assetid: fb5254eb-b635-4b39-8361-136fd36f2b1f
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f4ad215f53d3100ada7d0cb66a69aeb11075bad0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287272"
---
# <a name="set-a-database-to-single-user-mode"></a>Definir um banco de dados como modo de usuário único
  Este tópico descreve como configurar um banco de dados definido pelo usuário no modo de usuário único no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. O modo de usuário único especifica que apenas um usuário pode acessar o banco de dados por vez e, normalmente é usado para ações de manutenção.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para definir um banco de dados como modo de usuário único, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Se outros usuários estiverem conectados ao banco de dados no momento em que você configurar o banco de dados como modo de usuário único, as conexões deles ao banco de dados serão fechadas sem aviso.  
  
-   O banco de dados permanece em modo de usuário único mesmo se o usuário que definiu a opção fizer logoff. Nesse momento, um usuário diferente, mas somente um, poderá se conectar ao banco de dados.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Antes de definir o banco de dados como SINGLE_USER, verifique se a opção AUTO_UPDATE_STATISTICS_ASYNC está definida como OFF. Quando esta opção está definida como ON, o thread em segundo plano usado para a atualização de estatísticas estabelece uma conexão com o banco de dados e não será possível acessar o banco de dados em modo de usuário único. Para obter mais informações, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-set-a-database-to-single-user-mode"></a>Para definir um banco de dados como modo de usuário único  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e expanda-a.  
  
2.  Clique com o botão direito do mouse no banco de dados a ser alterado e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Banco de Dados** , clique na página **Opções** .  
  
4.  Da opção **Restringir o Acesso** , selecione **Simples**.  
  
5.  Se outros usuários estiverem conectados ao banco de dados, uma mensagem **Conexões Abertas** será exibida. Para alterar a propriedade e fechar todas as outras conexões, clique em **Sim**.  
  
 Também é possível definir o banco de dados como acesso múltiplo ou restrito usando esse procedimento. Para obter mais informações sobre as opções de Restringir o Acesso, veja [Propriedades de banco de dados &#40;Página Opções&#41;](database-properties-options-page.md).  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-set-a-database-to-single-user-mode"></a>Para definir um banco de dados como modo de usuário único  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo define o banco de dados como o modo `SINGLE_USER` para obter acesso exclusivo. Em seguida, o exemplo define o estado do banco de dados [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] como `READ_ONLY` e retorna o acesso ao banco de dados para todos os usuários. A opção de término `WITH ROLLBACK IMMEDIATE` é especificada na primeira instrução `ALTER DATABASE` . Isso levará todas as transações incompletas a serem revertidas e qualquer outra conexão com o banco de dados [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] a ser desconectada imediatamente.  
  
 [!code-sql[DatabaseDDL#AlterDatabase8](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase8)]  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
