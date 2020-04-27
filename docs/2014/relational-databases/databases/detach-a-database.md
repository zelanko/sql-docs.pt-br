---
title: Desanexar um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.detachdatabase.f1
helpviewer_keywords:
- database detaching [SQL Server]
- detaching databases [SQL Server]
ms.assetid: f63d4107-13e4-4bfe-922d-5e4f712e472d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 050220781f484b4a9e595551496d7e58c06f954c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62871951"
---
# <a name="detach-a-database"></a>Desanexar um banco de dados
  Este tópico descreve como desanexar um banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Os arquivos desanexados permanecem e podem ser anexados novamente com o uso de CREATE DATABASE com a opção FOR ATTACH ou FOR ATTACH_REBUILD_LOG. Os arquivos podem ser movidos para outro servidor, onde podem ser anexados.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para desanexar banco de dados usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
 Para obter uma lista de limitações e restrições, veja [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer associação na função de banco de dados fixa db_owner.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-detach-a-database"></a>Para desanexar um banco de dados  
  
1.  No Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , conecte-se à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**e selecione o nome do banco de dados de usuário que você quer desanexar.  
  
3.  Clique com o botão direito do mouse no nome do banco de dados, aponte para **Tarefas**e clique em **Desanexar**. A caixa de diálogo **Desanexar Banco de Dados** é exibida.  
  
     **Bancos de dados a serem desanexados**  
     Lista os bancos de dados a serem desanexados  
  
     **Database Name**  
     Exibe o nome do banco de dados a ser desanexado.  
  
     **Cancelar Conexões**  
     Cancelar conexões com o banco de dados especificado.  
  
    > [!NOTE]  
    >  Você não pode desanexar um banco de dados com conexões ativas.  
  
     **Atualização de Estatísticas**  
     Por padrão, a operação desanexar retém qualquer estatística de otimização desatualizada ao desanexar o banco de dados; para atualizar as estatísticas de otimização existentes, clique nesta caixa de seleção.  
  
     **Manter Catálogos de Texto Completo**  
     Por padrão, a operação desanexar mantém qualquer catálogo de texto completo que esteja associado ao banco de dados. Para removê-los, desmarque a caixa de seleção **Manter Catálogos de Texto Completo** . Essa opção é exibida apenas quando você está atualizando um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
     **Status**  
     Exibe um dos seguintes estados: **Pronto** ou **Não pronto**.  
  
     **Mensagem**  
     A coluna **Mensagem** pode exibir informações sobre o banco de dados, da seguinte forma:  
  
    -   Quando um banco de dados estiver envolvido com replicação, o **Status** será **Não pronto** e a coluna **Mensagem** exibirá **Banco de Dados replicado**.  
  
    -   Quando um banco de dados tiver uma ou mais conexões ativas, o **Status** será **Não está pronto** e a coluna **Mensagem** exibirá _<número_de_conexões_ativas>_ **Conexão(ões) ativa(s)** – por exemplo: **1 Conexão ativa**. Antes de desanexar o banco de dados, você deverá cancelar qualquer conexão ativa selecionando **Cancelar Conexões**.  
  
     Para obter mais informações sobre a mensagem, clique o texto com hiperlink para abrir o Monitor de atividades.  
  
4.  Quando você estiver pronto para desanexar o banco de dados, clique em **OK**.  
  
> [!NOTE]  
>  O banco de dados recém-desanexado permanecerá visível no nó **Bancos de Dados** do Pesquisador de Objetos até que a exibição seja atualizada. Você pode atualizar a exibição a qualquer momento: Clique no painel Pesquisador de Objetos e, na barra de menus, selecione **Exibir** e, depois, **Atualizar**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-detach-a-database"></a>Para desanexar um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo desanexa o banco de dados AdventureWorks2012 com skipchecks definido como verdadeiro.  
  
```  
EXEC sp_detach_db 'AdventureWorks2012', 'true';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)  
  
  
