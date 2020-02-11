---
title: Fazer backup da chave mestra de serviço | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server], exporting
ms.assetid: f60b917c-6408-48be-b911-f93b05796904
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: c6e67b2eacfd428bc296596699ff65939789d1e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74957270"
---
# <a name="back-up-the-service-master-key"></a>Fazer backup da chave mestra de serviço
  Este tópico descreve como fazer backup da Chave mestra de serviço no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. A chave mestra de serviço é a raiz da hierarquia de criptografia. Ela deve ter seu backup feito e armazenado em um local seguro, fora do site. Criar este backup deveria ser uma das primeiras ações administrativas executadas no servidor.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   [Para fazer backup da chave mestra de serviço](#Procedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   A chave mestra deve estar aberta e, portanto, descriptografada antes de ser feito o back up. Se for criptografada com a chave mestra de serviço, a chave mestra não precisará ser aberta explicitamente; porém, se a chave mestra só for criptografada com uma senha, deverá ser aberta explicitamente.  
  
-   Recomendamos que você faça o backup da chave mestra assim que ela for criada e armazene o backup em um local externo seguro.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão CONTROL no banco de dados.  
  
##  <a name="Procedure"></a> Usando o Transact-SQL  
  
#### <a name="to-back-up-the-service-master-key"></a>Para fazer backup da Chave mestra de serviço  
  
1.  No [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que contém a chave mestra de serviço da qual você deseja fazer backup.  
  
2.  Escolha uma senha que será usada para criptografar a chave mestra na mídia de backup. Esta senha está sujeita à verificação de complexidade. Para obter mais informações, consulte [Password Policy](../password-policy.md).  
  
3.  Obtenha uma mídia de backup removível para armazenar uma cópia da chave de backup.  
  
4.  Identifique um diretório NTFS no qual criar o backup da chave. É aí que você criará o arquivo especificado na próxima etapa. O diretório deve ser protegido com ACLs (listas de controle de acesso) altamente restritivas.  
  
5.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
6.  Na barra Padrão, clique em **Nova Consulta**.  
  
7.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Creates a backup of the "AdventureWorks2012" master key.  
    -- Because this master key is not encrypted by the service master key, a password must be specified when it is opened.  
    USE AdventureWorks2012;  
    GO  
    BACKUP SERVICE MASTER KEY TO FILE = 'c:\temp_backups\keys\service_master_ key'   
        ENCRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
    GO  
    ```  
  
    > [!NOTE]  
    >  O caminho do arquivo para a chave e a senha da chave (se existir) serão diferentes do que é indicado acima. Verifique se ambos são específicos da sua configuração de servidor e chave.  
  
8.  Copie o arquivo na mídia de backup e verifique a cópia.  
  
9. Armazene o backup em um local seguro, fora do site.  
  
 Para obter mais informações, veja [OPEN MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/open-master-key-transact-sql) e [BACKUP MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-master-key-transact-sql).  
  
  
