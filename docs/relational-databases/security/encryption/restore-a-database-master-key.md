---
title: Restaurar uma chave mestra de banco de dados | Microsoft Docs
description: Saiba como restaurar a chave mestra do banco de dados no SQL Server usando o SQL Server Management Studio com o Transact-SQL.
ms.custom: ''
ms.date: 01/02/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], importing
ms.assetid: 16897cc5-db8f-43bb-a38e-6855c82647cf
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 9860b952751937b18ca5e95e92ac959bb86abd23
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892239"
---
# <a name="restore-a-database-master-key"></a>Restaurar uma chave mestra de banco de dados
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como restaurar a chave mestra de banco de dados no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a>Limitações e Restrições  
  
- Quando a chave mestra é restaurada, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] descriptografa todas as chaves atualmente criptografadas com a chave mestra ativa e criptografa essas chaves com a chave mestra restaurada. Essa operação de uso intensivo de recursos deve ser agendada em um período de baixa demanda. Se a chave mestra de banco de dados atual não for aberta ou não puder ser aberta, ou se qualquer chave criptografada com ela não puder ser descriptografada, a operação de restauração falhará.  
  
- Se qualquer uma dessas descriptografias falhar, a restauração falhará. É possível usar a opção FORCE para ignorar erros, mas essa opção causará a perda dos dados que não puderem ser descriptografados.  
  
- Se a chave mestra foi criptografada pela chave mestra de serviço, a chave mestra restaurada também será criptografada pela chave mestra de serviço.  
  
- Se não houver nenhuma chave mestra no banco de dados atual, RESTORE MASTER KEY criará uma chave mestra. A nova chave mestra não será criptografada automaticamente com a chave mestra de serviço.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões
Exige a permissão CONTROL no banco de dados.  
  
## <a name="using-sql-server-management-studio-with-transact-sql"></a>Usando o SQL Server Management Studio com o Transact-SQL  
  
### <a name="to-restore-the-database-master-key"></a>Para restaurar a chave mestra de banco de dados  
  
1. Recupere uma cópia do backup da chave mestra de banco de dados de uma mídia de backup física ou de um diretório no sistema de arquivos local.  
  
2. No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
3. Na barra Padrão, clique em **Nova Consulta**.  
  
4. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  

    ```sql
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
    > O caminho do arquivo para a chave e a senha da chave (se existir) serão diferentes do que é indicado acima. Certifique-se de que ambos sejam específicos da sua configuração de servidor e chave.  
  
 Para obter mais informações, consulte [RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/restore-master-key-transact-sql.md)  
