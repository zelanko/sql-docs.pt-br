---
title: Criptografia do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- encryption [SQL Server], about encryption
- security [SQL Server], encryption
- cryptography [SQL Server], about cryptography
ms.assetid: ead0150e-4943-4ad5-84c8-36f85c7278f4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3f975f11bf5a3c71b1f62109db1c68b5b25739b7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sql-server-encryption"></a>Criptografia do SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Criptografia é o processo de ocultar dados pelo uso de uma chave ou senha. Isso pode tornar os dados inúteis sem a chave de descriptrografia correspondente ou senha. A criptografia não resolve problemas de controle de acesso. Porém, aumenta a segurança, limitando perda de dados mesmo se os controles de acesso forem ignorados. Por exemplo, se o computador host do banco de dados for malconfigurado e um hacker obtiver dados confidenciais, as informações roubadas poderão ser inúteis se estiverem criptografadas.  
  

> [!IMPORTANT]  
>  Embora a criptografia seja uma ferramenta valiosa para ajudar a garantir a segurança, não deve ser considerada em todos os dados ou conexões. Quando você estiver decidindo se a criptografia deve ser implementada, considere como os usuários acessarão os dados. Se os usuários acessarem dados por uma rede pública, a criptografia de dados poderá ser necessária para aumentar a segurança. No entanto, se todos os acessos envolverem uma configuração de intranet segura, a criptografia poderá não ser necessária. Qualquer uso de criptografia deve também incluir uma estratégia de manutenção de senhas, chaves e certificados.  
  
> [!NOTE]  
>  As informações mais recentes sobre o protocolo TSL1.2 estão disponíveis em [Suporte a TLS 1.2 para o Microsoft SQL Server](https://support.microsoft.com/kb/3135244).  

Você pode usar criptografia no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para conexões, dados e procedimentos armazenados. A tabela a seguir contém mais informações sobre criptografia no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

 [Hierarquia de criptografia](../../../relational-databases/security/encryption/encryption-hierarchy.md)  
 Informações sobre a hierarquia de criptografia no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Escolher um algoritmo de criptografia](../../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
 Informações sobre como selecionar um algoritmo de criptografia eficaz.  
  
 [TDE &#40;Transparent Data Encryption&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
 Informações gerais sobre como criptografar dados de forma transparente.  
  
 [Chaves de criptografia do SQL Server e banco de dados &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], as chaves de criptografia incluem uma combinação de chaves públicas, privadas e assimétricas, usadas para proteger dados confidenciais. Esta seção explica como implementar e gerenciar chaves de criptografia.  
  
 [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
 Garantir que administradores de banco de dados locais, operadores de banco de dados de nuvem e outros com altos privilégios, mas não autorizados, não possam acessar os dados criptografados.  
  
 [Mascaramento de dados dinâmicos](../../../relational-databases/security/dynamic-data-masking.md)  
 Limitar a exposição de dados confidenciais mascarando-os para usuários sem privilégios.  
  
 [Certificados e chaves assimétricas do SQL Server](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)  
 Informações sobre o uso de Criptografia por Chave Pública.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Protegendo o SQL Server](../../../relational-databases/security/securing-sql-server.md)  
 Visão geral de como ajudar a proteger a plataforma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e como trabalhar com usuários e objetos protegíveis.  
  
 [Funções criptográficas &#40;Transact-SQL&#41;](../../../t-sql/functions/cryptographic-functions-transact-sql.md)  
 Informações sobre como implementar funções de criptografia.  
  
 [ENCRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
 Informações sobre como usar uma senha para criptografar dados.  
  
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)  
 Informações sobre como usar uma chave simétrica para criptografar dados.  
  
 [ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbyasymkey-transact-sql.md)  
 Informações sobre como usar uma chave assimétrica para criptografar dados.  
  
 [ENCRYPTBYCERT &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbycert-transact-sql.md)  
 Informações sobre como usar um certificado para criptografar dados.  
  
## <a name="external-resources"></a>Recursos externos  
 [Microsoft TechNet: TechCenter do SQL Server: Segurança e proteção do SQL Server 2012](http://download.microsoft.com/download/8/F/A/8FABACD7-803E-40FC-ADF8-355E7D218F4C/SQL_Server_2012_Security_Best_Practice_Whitepaper_Apr2012.docx)  
 Informações atuais sobre segurança do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [sys.key_encryptions &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)   
 [Chaves de criptografia do SQL Server e banco de dados &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Fazer backup e restaurar as chave de criptografia do Reporting Services](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
  
  
