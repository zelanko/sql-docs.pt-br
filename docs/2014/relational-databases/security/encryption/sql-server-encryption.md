---
title: Criptografia do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], about encryption
- security [SQL Server], encryption
- cryptography [SQL Server], about cryptography
ms.assetid: ead0150e-4943-4ad5-84c8-36f85c7278f4
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 1484a32eb808e6778896a498d5a6dee525b18aed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63011311"
---
# <a name="sql-server-encryption"></a>Criptografia do SQL Server
  Criptografia é o processo de confundir dados pelo uso de uma chave ou senha. Isso pode tornar os dados inúteis sem a chave de descriptrografia correspondente ou senha. A criptografia não resolve problemas de controle de acesso. Porém, aumenta a segurança, limitando perda de dados mesmo se os controles de acesso forem ignorados. Por exemplo, se o computador host do banco de dados for malconfigurado e um hacker obtiver dados confidenciais, as informações roubadas poderão ser inúteis se estiverem criptografadas.  
  
 Você pode usar criptografia no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para conexões, dados e procedimentos armazenados. A tabela seguinte contém mais informações sobre criptografia no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Embora a criptografia seja uma ferramenta valiosa para ajudar a garantir a segurança, não deve ser considerada em todos os dados ou conexões. Quando você estiver decidindo se a criptografia deve ser implementada, considere como os usuários acessarão os dados. Se os usuários acessarem dados por uma rede pública, a criptografia de dados poderá ser necessária para aumentar a segurança. No entanto, se todos os acessos envolverem uma configuração de intranet segura, a criptografia poderá não ser necessária. Qualquer uso de criptografia deve também incluir uma estratégia de manutenção de senhas, chaves e certificados.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Hierarquia de criptografia](encryption-hierarchy.md)  
 Informações sobre a hierarquia de criptografia no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Escolher um algoritmo de criptografia](choose-an-encryption-algorithm.md)  
 Informações sobre como selecionar um algoritmo de criptografia eficaz.  
  
 [TDE &#40;Transparent Data Encryption&#41;](transparent-data-encryption.md)  
 Informações gerais sobre como criptografar dados de forma transparente.  
  
 [Chaves de criptografia do SQL Server e banco de dados &#40;Mecanismo de Banco de Dados&#41;](sql-server-and-database-encryption-keys-database-engine.md)  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], as chaves de criptografia incluem uma combinação de chaves públicas, privadas e assimétricas, usadas para proteger dados confidenciais. Esta seção explica como implementar e gerenciar chaves de criptografia.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Protegendo o SQL Server](../securing-sql-server.md)  
 Visão geral de como ajudar a proteger a plataforma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e como trabalhar com usuários e objetos protegíveis.  
  
 [Funções criptográficas &#40;Transact-SQL&#41;](/sql/t-sql/functions/cryptographic-functions-transact-sql)  
 Informações sobre como implementar funções de criptografia.  
  
 [ENCRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
 Informações sobre como usar uma senha para criptografar dados.  
  
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](/sql/t-sql/functions/encryptbykey-transact-sql)  
 Informações sobre como usar uma chave simétrica para criptografar dados.  
  
 [ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
 Informações sobre como usar uma chave assimétrica para criptografar dados.  
  
 [ENCRYPTBYCERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/encryptbycert-transact-sql)  
 Informações sobre como usar um certificado para criptografar dados.  
  
## <a name="external-resources"></a>Recursos externos  
 [10 etapas a segurança do SQL Server 2005](https://www.itprotoday.com/sql-server/10-steps-sql-server-2005-security)  
 Informações atuais sobre segurança do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [sys.key_encryptions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-key-encryptions-transact-sql)   
 [Chaves de criptografia do SQL Server e banco de dados &#40;Mecanismo de Banco de Dados&#41;](sql-server-and-database-encryption-keys-database-engine.md)   
 [Fazer backup e restaurar as chave de criptografia do Reporting Services](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
  
  
