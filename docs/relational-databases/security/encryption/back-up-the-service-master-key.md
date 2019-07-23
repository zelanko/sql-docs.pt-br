---
title: Fazer backup da chave mestra de serviço | Microsoft Docs
ms.custom: ''
ms.date: 01/02/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server], exporting
ms.assetid: f60b917c-6408-48be-b911-f93b05796904
author: aliceku
ms.author: aliceku
ms.openlocfilehash: 4a5b28fda96be3fce311abc159bbe8e94fc061ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024421"
---
# <a name="back-up-the-service-master-key"></a>Fazer backup da chave mestra de serviço
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este artigo descreve como fazer backup da Chave mestra de serviço no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[tsql](../../../includes/tsql-md.md)]. A chave mestra de serviço é a raiz da hierarquia de criptografia. Ela deve ter seu backup feito e armazenado em um local seguro, fora do site. Criar este backup deveria ser uma das primeiras ações administrativas executadas no servidor.  

## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a>Limitações e Restrições  

- A chave mestra deve estar aberta e, portanto, descriptografada antes de ser feito o back up. Se for criptografada com a chave mestra de serviço, a chave mestra não precisará ser aberta explicitamente; porém, se a chave mestra só for criptografada com uma senha, deverá ser aberta explicitamente.  
  
- Recomendamos que você faça o backup da chave mestra assim que ela for criada e armazene o backup em um local externo seguro.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões
Exige a permissão CONTROL no banco de dados.  
  
## <a name="using-transact-sql"></a>Usando Transact-SQL  
  
### <a name="to-back-up-the-service-master-key"></a>Para fazer backup da Chave mestra de serviço
  
1. No [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que contém a chave mestra de serviço da qual você deseja fazer backup.  
  
2. Escolha uma senha que será usada para criptografar a chave mestra na mídia de backup. Esta senha está sujeita à verificação de complexidade. Para obter mais informações, consulte [Password Policy](../../../relational-databases/security/password-policy.md).  
  
3. Obtenha uma mídia de backup removível para armazenar uma cópia da chave de backup.  
  
4. Identifique um diretório NTFS no qual criar o backup da chave. Este diretório é o local em que você criará o arquivo especificado na próxima etapa. O diretório deve ser protegido com ACLs (listas de controle de acesso) altamente restritivas.  
  
5. No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
6. Na barra Padrão, clique em **Nova Consulta**.  
  
7. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql
    -- Creates a backup of the service master key.
    USE master;
    GO
    BACKUP SERVICE MASTER KEY TO FILE = 'c:\temp_backups\keys\service_master_ key'
        ENCRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';
    GO
    ```  
  
    > [!NOTE]  
    > O caminho do arquivo para a chave e a senha da chave (se existir) serão diferentes do que é indicado acima. Verifique se ambos são específicos da sua configuração de servidor e chave.
  
8. Copie o arquivo na mídia de backup e verifique a cópia.  
  
9. Armazene o backup em um local seguro, fora do site.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 Para obter mais informações, veja [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-master-key-transact-sql.md) e [BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-master-key-transact-sql.md).  
