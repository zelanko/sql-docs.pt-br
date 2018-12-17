---
title: Gerenciamento extensível de chaves usando o Azure Key Vault (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2016
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Extensible Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
- EKM, with key vault
- TDE, EKM and key vault
- Key Management with key vault
- SQL Server Connector, about
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 9bb567ea41c87b895314abb8c3f7cedc4bbfbc7d
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52391020"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>Gerenciamento extensível de chaves usando o Azure Key Vault (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para Cofre de Chaves do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure permite que a criptografia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] use o serviço de Cofre de Chaves do Azure como um provedor de [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md) para proteger suas chaves de criptografia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Este tópico descreve o conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Informações adicionais estão disponíveis em [Etapas de instalação para o gerenciamento extensível de chaves usando o Cofre de Chaves do Azure](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md), [Use o Conector do SQL Server com recursos de criptografia do SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)e [Manutenção e solução de problemas do Conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md).  
  
##  <a name="Uses"></a> O que é o EKM (Gerenciamento Extensível de Chaves) e por que o usamos?  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece vários tipos de criptografia que ajudam a proteger dados confidenciais, incluindo [Transparent Data Encryption&#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md), [CLE](../../../t-sql/functions/cryptographic-functions-transact-sql.md) (Criptografia de Nível de Coluna) e [Criptografia de Backup](../../../relational-databases/backup-restore/backup-encryption.md). Em todos esses casos, nessa hierarquia de chave tradicional, os dados são criptografados usando uma chave de criptografia simétrica de dados (DEK). A chave de criptografia simétrica de dados é ainda mais protegida ao criptografar com uma hierarquia de chaves armazenadas em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Em vez de nesse modelo, a alternativa é o Modelo de Provedor EKM. Usar a arquitetura de provedor EKM permite que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proteja as chaves de criptografia de dados usando uma chave assimétrica armazenada fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um provedor de criptografia externo. Esse modelo acrescenta uma camada adicional de segurança e separa o gerenciamento de chaves e dados.  
   
 A imagem a seguir compara o serviço tradicional de gerenciamento de hierarquia de chave com o sistema de Cofre de Chaves do Azure.  
  
 ![ekm-key-hierarchy-traditional](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-traditional.png "ekm-key-hierarchy-traditional")  
  
   
 O Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] atua como uma ponte entre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o Cofre de Chaves do Azure, portanto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode aproveitar a escalabilidade, alto desempenho e alta disponibilidade do serviço de Cofre de Chaves do Azure. A imagem a seguir representa como a hierarquia de chave funciona na arquitetura do provedor EKM com o Cofre de Chaves do Azure e o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
  O Cofre de Chaves do Azure pode ser usado com instalações do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em Máquinas Virtuais do Azure do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] e para servidores locais. O serviço de chave de cofre também fornece a opção de usar rigidamente módulos de segurança de hardware (HSM) monitorados e controlados para um nível mais alto de proteção para as chaves de criptografia assimétrica. Para obter mais informações sobre o cofre de chaves, consulte [Cofre de Chaves do Azure](https://go.microsoft.com/fwlink/?LinkId=521401).  
  
 A imagem a seguir resume o fluxo do processo de EKM usando o cofre da chave. (Os números de etapa do processo na imagem não devem corresponder aos números de etapa de instalação que seguem a imagem.)  
  
 ![EKM do SQL Server usando o Azure Key Vault](../../../relational-databases/security/encryption/media/ekm-using-azure-key-vault.png "EKM do SQL Server usando o Azure Key Vault")  

> [!NOTE]  
>  Versões 1.0.0.440 e anteriores foram substituídas e não têm mais suporte em ambientes de produção. Atualize para a versão 1.0.1.0 ou posterior visitando o [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=45344) e usando as instruções da página [Manutenção e solução de problemas do Conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) em "Atualização do Conector do SQL Server".
  
 Para a próxima etapa, consulte [Etapas de instalação para o gerenciamento extensível de chaves usando o Cofre de Chaves do Azure](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md).  
  
 Para cenários de uso, consulte [Use SQL Server Connector with SQL Encryption Features](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)(Usar o Conector do SQL Server com recursos de criptografia do SQL).  
  
## <a name="see-also"></a>Consulte Também  
 [Manutenção e solução de problemas do conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  
