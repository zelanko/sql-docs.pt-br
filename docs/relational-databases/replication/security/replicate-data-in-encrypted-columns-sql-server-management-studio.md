---
title: Replicar dados em colunas criptografadas (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], replicating data
- encryption [SQL Server replication]
- publishing [SQL Server replication], encrypted columns
ms.assetid: d1f8f586-e5a3-4a71-9391-11198d42bfa3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7a692cb2d5862699abb68d5a0814b948a25158fa
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129546"
---
# <a name="replicate-data-in-encrypted-columns-sql-server-management-studio"></a>Replicar dados em colunas criptografadas (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A replicação permite que você publique dados criptografados em coluna. Para descriptografar e usar esses dados no Assinante, a chave usada para criptografar os dados no Publicador também deve estar presente no Assinante. A replicação não fornece um mecanismo seguro para transportar chaves de criptografia. Você deve recriar a chave de criptografia manualmente no Assinante. Este tópico mostra como criptografar uma coluna no Publicador e certificar-se de que a chave de criptografia está disponível no Assinante.  
  
 As etapas básicas são as seguintes:  
  
1.  Crie a chave simétrica no Publicador.  
  
2.  Criptografe os dados da coluna com a chave simétrica.  
  
3.  Publique a tabela com a coluna criptografada.  
  
4.  Assine a publicação.  
  
5.  Inicialize a assinatura.  
  
6.  Recrie a chave simétrica no Assinante usando os mesmos valores para ALGORITMO, KEY_SOURCE e IDENTITY_VALUE como na etapa 1.  
  
7.  Acesse os dados de coluna criptografados.  
  
> [!NOTE]  
>  Você deve usar uma chave simétrica para criptografar dados de coluna. A própria chave simétrica pode ser protegida através de meios diferentes no Publicador e no Assinante.  
  
### <a name="to-create-and-replicate-encrypted-column-data"></a>Para criar e reproduzir dados em coluna criptografada  
  
1.  No Publicador, execute [CREATE SYMMETRIC KEY](../../../t-sql/statements/create-symmetric-key-transact-sql.md).  
  
    > [!IMPORTANT]  
    >  O valor de KEY_SOURCE é um dado valioso que pode ser usado recriar a chave simétrica e descriptografar os dados. KEY_SOURCE sempre deve ser armazenado e transportado de modo seguro.  
  
2.  Execute [OPEN SYMMETRIC KEY](../../../t-sql/statements/open-symmetric-key-transact-sql.md) para abrir a chave nova.  
  
3.  Use a função [EncryptByKey](../../../t-sql/functions/encryptbykey-transact-sql.md) para criptografar dados de coluna no Publicador.  
  
4.  Execute [CLOSE SYMMETRIC KEY](../../../t-sql/statements/close-symmetric-key-transact-sql.md) para fechar a chave.  
  
5.  Publique a tabela que contém a coluna criptografada. Para obter mais informações, consulte [Criar uma assinatura](../../../relational-databases/replication/publish/create-a-publication.md).  
  
6.  Assine a publicação. Para obter mais informações, consulte [Criar uma assinatura pull](../../../relational-databases/replication/create-a-pull-subscription.md) ou [Criar uma assinatura push](../../../relational-databases/replication/create-a-push-subscription.md).  
  
7.  Inicialize a assinatura. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
8.  No Assinante, execute [CREATE SYMMETRIC KEY](../../../t-sql/statements/create-symmetric-key-transact-sql.md) usando os mesmos valores para ALGORITHM, KEY_SOURCE, e IDENTITY_VALUE da etapa 1. Você pode especificar um valor diferente para ENCRYPTION BY.  
  
    > [!IMPORTANT]  
    >  O valor de KEY_SOURCE é um dado valioso que pode ser usado recriar a chave simétrica e descriptografar os dados. KEY_SOURCE sempre deve ser armazenado e transportado de modo seguro.  
  
9. Execute [OPEN SYMMETRIC KEY](../../../t-sql/statements/open-symmetric-key-transact-sql.md) para abrir a chave nova.  
  
10. Use a função [DecryptByKey](../../../t-sql/functions/decryptbykey-transact-sql.md) para descriptografar dados replicados no Assinante.  
  
11. Execute [CLOSE SYMMETRIC KEY](../../../t-sql/statements/close-symmetric-key-transact-sql.md) para fechar a chave.  
  
## <a name="example"></a>Exemplo  
 Este exemplo cria uma chave simétrica, um certificado que é usado para auxiliar a proteger a chave simétrica e uma chave mestra. Essas chaves são criadas no banco de dados de publicação. Depois elas são usadas para criar uma coluna criptografada (EncryptedCreditCardApprovalCode) na tabela `SalesOrderHeader` . Essa coluna é publicada na publicação AdvWorksSalesOrdersMerge em vez da coluna não criptografada CreditCardApprovalCode. Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
 [!code-sql[HowTo#sp_PublishEncryptedColumn](../../../relational-databases/replication/codesnippet/tsql/replicate-data-in-encryp_1.sql)]  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/replicate-data-in-encryp_2.sql)]  
  
## <a name="example"></a>Exemplo  
 Este exemplo recria a mesma chave simétrica no banco de dados de assinatura usando os mesmos valores para ALGORITHM, KEY_SOURCE, e IDENTITY_VALUE do primeiro exemplo. Este exemplo supõe que você já inicializou uma assinatura à publicação AdvWorksSalesOrdersMerge para replicar a coluna criptografada. Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, deve-se proteger o arquivo durante o armazenamento e o transporte para evitar o acesso não autorizado.  
  
 [!code-sql[HowTo#sp_SubscriberEncryptedColumn](../../../relational-databases/replication/codesnippet/tsql/replicate-data-in-encryp_3.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar configurações de segurança de replicação](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Criar chaves simétricas idênticas em dois servidores](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
  
