---
title: Restaurar uma chave mestra de banco de dados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database master key [SQL Server], importing
ms.assetid: 16897cc5-db8f-43bb-a38e-6855c82647cf
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c2833a4b91d4465e126c0a393e756ab09106d1c8
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="restore-a-database-master-key"></a>Restaurar uma chave mestra de banco de dados
  Este tópico descreve como restaurar a chave mestra de banco de dados no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   [Para restaurar a chave mestra de banco de dados usando o Transact-SQL](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Quando a chave mestra é restaurada, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] descriptografa todas as chaves atualmente criptografadas com a chave mestra ativa e criptografa essas chaves com a chave mestra restaurada. Essa operação de uso intensivo de recursos deve ser agendada em um período de baixa demanda. Se a chave mestra de banco de dados atual não for aberta ou não puder ser aberta, ou se qualquer chave criptografada com ela não puder ser descriptografada, a operação de restauração falhará.  
  
-   Se qualquer uma dessas descriptografias falhar, a restauração falhará. É possível usar a opção FORCE para ignorar erros, mas essa opção causará a perda dos dados que não puderem ser descriptografados.  
  
-   Se a chave mestra foi criptografada pela chave mestra de serviço, a chave mestra restaurada também será criptografada pela chave mestra de serviço.  
  
-   Se não houver nenhuma chave mestra no banco de dados atual, RESTORE MASTER KEY criará uma chave mestra. A nova chave mestra não será criptografada automaticamente com a chave mestra de serviço.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão CONTROL no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio com o Transact-SQL  
  
#### <a name="to-restore-the-database-master-key"></a>Para restaurar a chave mestra de banco de dados  
  
1.  Recupere uma cópia do backup da chave mestra de banco de dados de uma mídia de backup física ou de um diretório no sistema de arquivos local.  
  
2.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
3.  Na barra Padrão, clique em **Nova Consulta**.  
  
4.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Restores the database master key of the AdventureWorks2012 database.  
    USE AdventureWorks2012;  
    GO  
    RESTORE MASTER KEY   
        FROM FILE = 'c:\backups\keys\AdventureWorks2012_master_key'   
        DECRYPTION BY PASSWORD = '3dH85Hhk003#GHkf02597gheij04'   
        ENCRYPTION BY PASSWORD = '259087M#MyjkFkjhywiyedfgGDFD';  
    GO  
    ```  
  
    > [!NOTE]  
    >  O caminho do arquivo para a chave e a senha da chave (se existir) serão diferentes do que é indicado acima. Certifique-se de que ambos sejam específicos da sua configuração de servidor e chave.  
  
 Para obter mais informações, consulte [RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/restore-master-key-transact-sql.md)  
  
  
