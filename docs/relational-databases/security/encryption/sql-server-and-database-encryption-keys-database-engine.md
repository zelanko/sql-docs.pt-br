---
title: Chaves de criptografia do SQL Server e banco de dados (Mecanismo de Banco de Dados) | Microsoft Docs
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
- keys [SQL Server], database encryption
ms.assetid: 15c0a5e8-9177-484c-ae75-8c552dc0dac0
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 909656391a0c51345860aece6f41f02de1dc360f
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-and-database-encryption-keys-database-engine"></a>Chaves de criptografia do SQL Server e banco de dados (Mecanismo de Banco de Dados)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa chaves de criptografia para ajudar a proteger dados, credenciais e informações de conexão armazenados em um banco de dados de servidor. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tem dois tipos de chaves: *simétrica* e *asimétrica*. As chaves simétricas usam a mesma senha para criptografar e descriptografar dados. As chaves assimétricas usam uma senha para criptografar dados (chamada chave *pública* ) e outra para descriptografar dados (chamada chave *privada* ).  
  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], as chaves de criptografia incluem uma combinação de chaves públicas, privadas e assimétricas, usadas para proteger dados confidenciais. A chave simétrica é criada durante a inicialização do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando você inicia pela primeira vez a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . A chave é usada pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para criptografar dados confidenciais que são armazenados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. As chaves públicas e privadas são criadas pelo sistema operacional e são usadas para proteger a chave simétrica. Um par de chaves pública e privada é criado para cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que armazena dados confidenciais em um banco de dados.  
  
## <a name="applications-for-sql-server-and-database-keys"></a>Aplicativos para o SQL Server e chaves de banco de dados  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tem dois aplicativos principais para chaves: uma *SMK (chave mestra de serviço)* gerada e para uma instância [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , e uma *DMK (chave mestra de banco de dados)* usada para um banco de dados.  
  
 A SMK é gerada automaticamente na primeira vez que a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é iniciada, e é usada para criptografar a senha, as credenciais e a chave mestra de banco de dados de um servidor vinculado. A SMK é criptografada com a chave do computador local usando a DPAPI (API de proteção de dados do Windows). A DPAPI usa uma chave derivada das credenciais do Windows da conta de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e das credenciais do computador. A chave mestra de serviço só pode ser descriptografada pela conta de serviço sob a qual foi criada ou por um principal que tenha acesso às credenciais da máquina.  
  
 A chave mestra de banco de dados é uma chave simétrica usada para proteger as chaves privadas dos certificados e as chaves assimétricas presentes no banco de dados. Ela também pode ser usada para criptografar dados, mas tem limitações de comprimento que a tornam pouco prática para os dados do que usar uma chave simétrica.  
  
 Quando é criada, a chave mestra é criptografada com o algoritmo DES Triplo e uma senha fornecida pelo usuário. Para habilitar a descriptografia automática da chave mestra, uma cópia da chave é criptografada com o uso da SMK. Ela é armazenada no banco de dados em que é usada e no banco de dados **master** do sistema.  
  
 A cópia da DMK armazenada no banco de dados **master** do sistema é silenciosamente atualizada sempre que a DMK é alterada. No entanto, esse padrão pode ser alterado com o uso da opção **DROP ENCRYPTION BY SERVICE MASTER KEY** da instrução **ALTER MASTER KEY** . Uma DMK não criptografada pela chave mestra de serviço deve ser aberta com a instrução **OPEN MASTER KEY** e uma senha.  
  
## <a name="managing-sql-server-and-database-keys"></a>Gerenciando o SQL Server e chaves de banco de dados  
 O gerenciamento de chaves de criptografia consiste na criação de novas chaves de banco de dados, na criação de um backup das chaves de servidor e de banco de dados, além de saber quando e como restaurar, excluir ou alterar as chaves.  
  
 Para gerenciar chaves simétricas, você pode usar as ferramentas incluídas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para fazer o seguinte:  
  
-   Fazer backup de uma cópia das chaves de servidor e de banco de dados para poder usá-las para recuperar uma instalação de servidor, ou como parte de uma migração planejada.  
  
-   Restaurar uma chave salva anteriormente em um banco de dados. Isso permite que uma nova instância de servidor acesse dados existentes que ela não criptografou originalmente.  
  
-   Excluir os dados criptografados em um banco de dados no evento improvável que você não possa mais acessar dados criptografados.  
  
-   Recriar chaves e criptografar novamente os dados no evento improvável que a chave seja comprometida. Como prática recomendável de segurança, você deve recriar as chaves periodicamente (por exemplo, a cada poucos meses) para proteger o servidor contra ataques que tentem decifrar as chaves.  
  
-   Adicionar ou remover uma instância do servidor de uma implantação em expansão do servidor em que vários servidores compartilham um único banco de dados e a chave que fornece criptografia reversível para esse banco de dados.  
  
## <a name="important-security-information"></a>Informações importantes sobre segurança  
 O acesso a objetos protegidos pela chave mestra de serviço requer ou a conta de Serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que foi usada para criar a chave, ou a conta do computador (máquina). Ou seja, o computador está ligado ao sistema em que a chave foi criada. Você pode alterar a conta de Serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] *ou* a conta do computador, sem perder o acesso à chave. Porém, se alterar ambos, você perderá o acesso à chave mestra de serviço. Se perder o acesso a essa chave sem um desses dois elementos, você não poderá descriptografar dados e objetos criptografados com o uso da chave original.  
  
 As conexões protegidas com a chave mestra de serviço não podem ser restauradas sem essa chave.  
  
 O acesso aos objetos e dados protegidos com a chave mestra de banco de dados requer apenas a senha usada para ajudar a proteger a chave.  
  
> [!CAUTION]  
>  Se você perder todo o acesso às chaves descritas anteriormente, perderá o acesso a objetos, conexões e dados protegidos por essas chaves. É possível restaurar a chave mestra de serviço, conforme descrito nos links aqui mostrados, ou você pode voltar ao sistema de criptografia original para recuperar o acesso. Não há nenhuma "porta dos fundos" para recuperar o acesso.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Service Master Key](../../../relational-databases/security/encryption/service-master-key.md)  
 Fornece uma breve explicação da chave mestra de serviço e suas práticas recomendadas.  
  
 [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
 Explica como usar sistemas de gerenciamento de chaves de terceiros com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 [Fazer backup da chave mestra de serviço](../../../relational-databases/security/encryption/back-up-the-service-master-key.md)  
  
 [Restaurar a chave mestra de serviço](../../../relational-databases/security/encryption/restore-the-service-master-key.md)  
  
 [Criar uma chave mestra de banco de dados](../../../relational-databases/security/encryption/create-a-database-master-key.md)  
  
 [Fazer backup da chave mestra de um banco de dados](../../../relational-databases/security/encryption/back-up-a-database-master-key.md)  
  
 [Restaurar uma chave mestra de banco de dados](../../../relational-databases/security/encryption/restore-a-database-master-key.md)  
  
 [Criar chaves simétricas idênticas em dois servidores](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
 [Habilitar TDE no SQL Server usando EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
 [Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 [Criptografar uma coluna de dados](../../../relational-databases/security/encryption/encrypt-a-column-of-data.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-service-master-key-transact-sql.md)  
  
 [Restaurar uma chave mestra de banco de dados](../../../relational-databases/security/encryption/restore-a-database-master-key.md)  
  
## <a name="see-also"></a>Consulte também  
 [Fazer backup e restaurar as chave de criptografia do Reporting Services](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Excluir e recriar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Adicionar e remover chaves de criptografia para implantação escalável &#40;Gerenciador de Configurações do SSRS&#41;](../../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [TDE &#40;Transparent Data Encryption&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md)  
  
  
