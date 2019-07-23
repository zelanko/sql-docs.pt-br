---
title: Restaurar a chave mestra de serviço | Microsoft Docs
ms.custom: ''
ms.date: 01/02/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server], importing
- service master key [SQL Server], restoring
ms.assetid: 14bdbbbe-d384-4692-b670-4243d2466fe1
author: aliceku
ms.author: aliceku
ms.openlocfilehash: c16742fe161f947e6256537ce04f36f9a07a89a6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111617"
---
# <a name="restore-the-service-master-key"></a>Restaurar a chave mestra de serviço
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como restaurar a chave mestra de serviço no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
> [!WARNING]  
> É improvável que você alguma vez precise restaurar essa chave. Se precisar, você deverá continuar com precaução extrema. Para obter mais informações, consulte [Back Up the Service Master Key](../../../relational-databases/security/encryption/back-up-the-service-master-key.md).  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a>Limitações e Restrições  
  
- Quando a chave mestra de serviço é restaurada, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] descriptografa todas as chaves e segredos que foram criptografados com a chave mestra de serviço atual e, em seguida, criptografa a chave mestra de serviço carregada do arquivo de backup.  
  
- Se qualquer uma dessas descriptografias falhar, a restauração falhará. É possível usar a opção FORCE para ignorar erros, mas essa opção causará a perda dos dados que não puderem ser descriptografados.  
  
- A nova geração da hierarquia de criptografia é uma operação que utiliza muitos recursos. É recomendável agendá-la em um período de baixa demanda.  
  
> [!CAUTION]  
> A chave mestra de serviço é a raiz da hierarquia de criptografia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . A chave mestra de serviço protege todas as outras chaves diretamente ou indiretamente na árvore. Se uma chave dependente não puder ser descriptografada durante uma restauração forçada, os dados protegidos por ela serão perdidos.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
Exige a permissão CONTROL SERVER no servidor.  
  
## <a name="using-transact-sql"></a>Usando Transact-SQL  
  
### <a name="to-restore-the-service-master-key"></a>Para restaurar a chave mestra de serviço  
  
1. Recupere uma cópia do backup da chave mestra de serviço de uma mídia de backup física ou de um diretório no sistema de arquivos local.  
  
2. No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
3. Na barra Padrão, clique em **Nova Consulta**.  
  
4. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql
    -- Restores the service master key from a backup file.  
    RESTORE SERVICE MASTER KEY   
        FROM FILE = 'c:\temp_backups\keys\service_master_key'   
        DECRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
    GO  
    ```  
  
    > [!NOTE]  
    > O caminho do arquivo para a chave e a senha da chave (se existir) serão diferentes do que é indicado acima. Certifique-se de que ambos sejam específicos da sua configuração de servidor e chave.
