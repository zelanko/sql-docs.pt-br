---
title: "TDE – BYOK (Bring Your Own Key) – SQL do Azure | Microsoft Docs"
description: "Suporte a BYOK (Bring Your Own Key) na TDE (Transparent Data Encryption) com o Azure Key Vault para o Banco de Dados SQL e Data Warehouse. Visão geral da TDE com BYOK, benefícios, modo de funcionamento, considerações e recomendações."
keywords: 
services: sql-database
documentationcenter: 
author: aliceku
manager: craigg
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: 
ms.component: security
ms.workload: On Demand
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 11/15/2017
ms.author: aliceku
ms.openlocfilehash: 5621bbaf20f30371ffabafddc0520dd15b8e4723
ms.sourcegitcommit: e851f3cab09f8f09a9a4cc0673b513a1c4303d2d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2018
---
# <a name="transparent-data-encryption-with-bring-your-own-key-preview-support-for-azure-sql-database-and-data-warehouse"></a>Transparent Data Encryption com suporte a Bring Your Own Key (VERSÃO PRÉVIA) para o Banco de Dados SQL do Azure e Data Warehouse
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

O suporte a BYOK (Bring Your Own Key) para [TDE (Transparent Data Encryption)](transparent-data-encryption.md) permite que você criptografe o DEK (Chave de Criptografia do Banco de Dados) com uma chave assimétrica chamada protetor de TDE.  O protetor de TDE é armazenado sob seu controle no [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), o sistema de gerenciamento de chaves externas baseado em nuvem do Azure. O Azure Key Vault é o primeiro serviço de gerenciamento de chaves com o qual a TDE tem suporte integrado a BYOK. O DEK de TDE, que é armazenado na página de inicialização de um banco de dados, é criptografado e descriptografado pelo protetor de TDE. O protetor de TDE é armazenado no Azure Key Vault e nunca deixa o cofre de chaves. Se o acesso do servidor ao cofre de chaves for revogado, um banco de dados não poderá ser descriptografado e lido na memória.  O protetor de TDE é definido no nível do servidor lógico e é herdado por todos os bancos de dados associados ao servidor. 

Com suporte a BYOK, os usuários agora podem controlar tarefas de gerenciamento de chaves, incluindo rotações de chave, permissões do cofre de chaves, exclusão de chaves e habilitação de auditoria/relatórios em todos os protetores de TDE usando a funcionalidade do Azure Key Vault. O Key Vault fornece o gerenciamento central de chaves, utiliza os HSMs (módulos de segurança de hardware) monitorados e possibilita a separação de tarefas entre o gerenciamento de chaves e de dados para ajudar a atender à conformidade regulatória.  


A TDE com BYOK fornece os seguintes benefícios:
- Maior controle granular e transparência com a capacidade de autogerenciar o Protetor de TDE   
- Gerenciamento central de protetores de TDE (juntamente com outras chaves e segredos usados em outros serviços do Azure) hospedando-os no Key Vault
- Separação das responsabilidades de gerenciamento de chaves e dados na organização, para dar suporte à separação de tarefas
- Maior confiança de seus próprios clientes, uma vez que o Key Vault é projetado de forma que a Microsoft não veja ou extraia nenhuma chave de criptografia. 
- Suporte para rotação de chaves

> [!IMPORTANT]
> Para aqueles que usam a TDE gerenciada por serviço que gostariam de começar a usar o Key Vault, a TDE permanece habilitada durante o processo de troca para um protetor de TDE no Key Vault. Não há nenhum tempo de inatividade nem nova criptografia dos arquivos do banco de dados. Mudar de uma chave gerenciada por serviço para uma chave do Key Vault requer apenas uma nova criptografia do DEK (chave de criptografia do banco de dados), que é uma operação online e rápida. 
>

## <a name="how-does-tde-with-byok-support-work"></a>Como a TDE com suporte a BYOK funciona?
 
![Autenticação do servidor para o Key Vault](./media/transparent-data-encryption-byok-azure-sql/tde-byok-server-authentication-flow.PNG)

Quando a primeira TDE está configurada para usar um protetor de TDE do Key Vault, o servidor envia o DEK de cada banco de dados habilitado para TDE para o Key Vault para uma solicitação wrap key. O Key Vault retorna a chave de criptografia do banco de dados criptografado, que é armazenada no banco de dados do usuário.  

>[!IMPORTANT]
>É importante observar que **quando um protetor de TDE é armazenado no Azure Key Vault, ele nunca deixa o Azure Key Vault**. O servidor lógico pode apenas enviar solicitações de operação de chave para o material da chave do protetor de TDE no Key Vault e **nunca acessa ou armazena em cache o protetor de TDE**. O administrador do Key Vault tem o direito de revogar permissões do Key Vault do servidor a qualquer momento, caso em que todas as conexões com o servidor são cortadas. 
>


## <a name="guidelines-for-configuring-tde-with-byok"></a>Diretrizes para a configuração da TDE com BYOK

### <a name="general-guidelines"></a>Instruções gerais
- Certifique-se de que o Azure Key Vault e o Banco de Dados SQL do Azure estarão no mesmo locatário.  **Não há suporte** para interações de servidor e cofre de chaves entre locatários.

- Decida quais assinaturas serão usadas para os recursos necessários, mover o servidor entre assinaturas posteriormente requer uma nova configuração de TDE com BYOKs.
- Configure o Azure Key Vault em uma única assinatura exclusivamente para os protetores de TDE do Banco de Dados SQL.  Todos os bancos de dados associados a um servidor lógico usam mesmo protetor de TDE, portanto, o agrupamento de bancos de dados para um servidor lógico deve ser considerado. 
- Recomendado: manter uma cópia local do protetor de TDE.  Isso exige um dispositivo HSM para criar um protetor de TDE localmente e um sistema de caução de chave para armazenar uma cópia local do protetor de TDE.


### <a name="guidelines-for-configuring-azure-key-vault"></a>Diretrizes para a configuração do Azure Key Vault

- Use um cofre de chaves com [exclusão reversível](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete) habilitada para proteger contra a perda de dados no caso da exclusão acidental da chave ou do cofre de chaves:  
  - Os recursos excluídos com a exclusão reversível são retidos por um determinado período, 90 dias a menos que eles sejam recuperados ou limpos.
  - As ações de **recuperação** e **limpeza** têm suas próprias permissões associadas em uma política de acesso do cofre de chaves. 
- Conceda ao servidor lógico o acesso ao cofre de chaves usando sua identidade do AAD (Azure Active Directory).  Ao usar a interface do usuário do Portal, a identidade do AAD é criada automaticamente e as permissões de acesso do cofre de chaves são concedidas ao servidor.  Usando o PowerShell para configurar a TDE com BYOK, a identidade do AAD deve ser criada e a conclusão deve ser verificada. Consulte [Configurar a TDE com BYOK](transparent-data-encryption-byok-azure-sql-configure.md) para obter instruções passo a passo detalhadas ao usar o PowerShell.

  >[!NOTE]
  >Se a identidade do AAD **for acidentalmente excluída ou as permissões do servidor forem revogadas** usando a política de acesso do cofre de chaves, o servidor perderá o acesso ao cofre de chaves.
  >
  
- Habilite a auditoria e os relatórios em todas as chaves de criptografia: o Key Vault fornece logs que são fáceis de injetar em outras ferramentas de SIEM (gerenciamento de eventos e informações de segurança). O [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-key-vault) do OMS (Operations Management Suite) é um exemplo de serviço que já está integrado.
- Para garantir a alta disponibilidade dos bancos de dados criptografados, configure cada servidor lógico com dois Azure Key Vaults que residem em regiões diferentes.


### <a name="guidelines-for-configuring-the-tde-protector-asymmetric-key-stored-in-azure-key-vault"></a>Diretrizes para configurar o protetor de TDE (chave assimétrica) armazenado no Azure Key Vault

- Crie sua chave de criptografia localmente em um dispositivo HSM local. Certifique-se de que seja uma chave RSA 2048 assimétrica para que ela possa ser armazenada no Azure Key Vault.
- Efetue a caução da chave em um sistema de caução de chave.  
- Importe o arquivo de chave de criptografia (.pfx, .byok ou .backup) para o Azure Key Vault. 
    
    >[!NOTE] 
    >Para fins de teste, é possível criar uma chave com o Azure Key Vault, no entanto, não é possível efetuar a caução dessa chave, pois a chave privada nunca pode deixar o cofre de chaves.  Sempre faça backup e efetue a caução de chaves usadas para criptografar dados de produção, uma vez que a perda da chave (exclusão acidental no cofre de chaves, expiração etc.) resulta em perda de dados permanente.
    >
    
- Use uma chave sem uma data de expiração e nunca defina uma data de expiração em uma chave que já está em uso: **depois que a chave expira, os bancos de dados criptografados perdem o acesso ao seu protetor de TDE e são descartados dentro de 24 horas**.
- Certifique-se de que a chave está habilitada e tem permissões para executar as operações *get*, *wrap key* e *unwrap key*.
- Crie um backup da chave do Azure Key Vault antes de usar a chave no Azure Key Vault pela primeira vez. Saiba mais sobre o comando [Backup-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) .
- Crie um novo backup sempre que quaisquer alterações forem feitas na chave (por exemplo, adicionar ACLs, adicionar marcas, adicionar atributos de chave).
- **Mantenha as versões anteriores** da chave no cofre de chaves ao realizar a rotação de chaves para que os backups do banco de dados mais antigos possam ser restaurados. Quando o protetor de TDE é alterado para um banco de dados, os backups antigos do banco de dados **não são** atualizados para usar o protetor de TDE mais recente.  Cada backup precisa do protetor de TDE no qual foi criado no momento da restauração. As rotações de chave podem ser executadas seguindo as instruções em [Girar o protetor de Transparent Data Encryption usando o PowerShell](transparent-data-encryption-byok-azure-sql-key-rotation.md).
- Mantenha todas as chaves usadas anteriormente no Azure Key Vault depois de trocar de volta para chaves gerenciadas por serviço.  Isso garante que os backups de banco de dados podem ser restaurados com os protetores de TDE armazenados no Azure Key Vault.  Os protetores de TDE criados com o Azure Key Vault devem ser mantidos até que todos os backups armazenados tenham sido criados com chaves gerenciadas por serviço.  
- Faça cópias de backup recuperáveis dessas chaves usando [Backup-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1).
- Para remover uma chave potencialmente comprometida durante um incidente de segurança sem o risco de perda de dados, siga as etapas em [Remover uma chave potencialmente comprometida](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md).


## <a name="high-availability-geo-replication-and-backup--restore"></a>Alta disponibilidade, replicação geográfica e backup/restauração

### <a name="high-availability-and-disaster-recovery"></a>Alta disponibilidade e recuperação de desastre

A forma como configurar a alta disponibilidade com o Azure Key Vault depende da configuração do banco de dados e do servidor lógico e aqui estão as configurações recomendadas para dois casos distintos.  O primeiro caso é um servidor lógico ou um banco de dados autônomo sem nenhuma redundância geográfica configurada.  O segundo caso é um banco de dados ou um servidor lógico configurado com grupos de failover ou redundância geográfica, em que se deve garantir que cada cópia com redundância geográfica tenha um Azure Key Vault local dentro do grupo de failover para garantir que os failovers geográficos funcionam. No primeiro caso, se você precisa de alta disponibilidade de um banco de dados e do servidor lógico sem nenhuma redundância geográfica configurada, é altamente recomendável configurar o servidor para usar dois cofres de chaves diferentes em duas regiões diferentes com o mesmo material de chave.  Isso pode ser feito criando um protetor de TDE usando o cofre de chaves primário colocalizado na mesma região que o servidor lógico e clonando a chave em um cofre de chaves em uma região do Azure diferente, para que o servidor tenha acesso a um segundo cofre de chaves caso o cofre de chaves primário sofra uma interrupção enquanto o banco de dados está em funcionamento. Use o cmdlet Backup-AzureKeyVaultKey para recuperar a chave no formato criptografado do cofre de chaves primário e, em seguida, use o cmdlet Restore-AzureKeyVaultKey e especifique um cofre de chaves na segunda região.


![Alta disponibilidade de servidor único e nenhuma recuperação de desastres geográfica](./media/transparent-data-encryption-byok-azure-sql/SingleServer_HA_Config.PNG)

No segundo caso, é necessário configurar Azure Key Vaults redundantes com base nas cópias de replicação geográfica ativa ou grupos de failover do Banco de Dados SQL existentes para manter a alta disponibilidade dos protetores de TDE no Azure Key Vault.  Cada servidor com replicação geográfica requer um cofre de chaves separado, idealmente colocalizado na mesma região do Azure que seu servidor. Caso um banco de dados primário se torne inacessível devido a uma interrupção em uma região e um failover seja acionado, o banco de dados secundário é capaz de assumir usando o cofre de chaves secundário.  

![Grupos de failover e recuperação de desastres geográfica](./media/transparent-data-encryption-byok-azure-sql/Geo_DR_Config.PNG)

Para assegurar que o acesso contínuo ao protetor de TDE no Azure Key Vault seja garantido durante um failover, ele deve ser configurado antes de um banco de dados ser replicado ou fazer o failover para um servidor secundário. Os servidores primário e secundário precisam armazenar cópias de protetores de TDE em todos os outros Azure Key Vaults, o que significa que nesse exemplo as mesmas chaves são armazenadas nos dois cofres de chaves.

Para adicionar uma chave existente de um cofre de chaves a outro Cofre de chaves, use o cmdlet [Add-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey).

 ```powershell
   <# Include the version guid in the KeyId #>
   Add-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```

>[!NOTE]
>O tamanho em caracteres combinado do nome do cofre de chaves e o nome da chave não pode exceder 94 caracteres.
>
 
Siga as etapas em [Visão geral de replicação geográfica ativa](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) para configurar a replicação geográfica ativa com esses servidores e para disparar um failover. 


### <a name="backup-and-restore"></a>Backup e restauração

Depois que um banco de dados é criptografado com a TDE usando uma chave do Key Vault, todos os backups gerados também são criptografados com o mesmo Protetor de TDE.

Para restaurar um backup criptografado com um Protetor de TDE do Key Vault, certifique-se de que o material da chave ainda está no cofre original com o nome de chave original. Quando o Protetor de TDE é alterado para um banco de dados, os backups antigos do banco de dados **não são** atualizado para usar o Protetor de TDE mais recente. Portanto, recomendamos que você mantenha todas as versões antigas do Protetor de TDE no Key Vault para que os backups de banco de dados possam ser restaurados. 

Se uma chave que pode ser necessária para restaurar um backup não estiver mais em seu cofre de chaves original, a seguinte mensagem de erro será retornada: “O servidor de destino <Servername> não tem acesso a todos os URIs do AKV criados entre <Timestamp #1> e <Timestamp #2>. Repita a operação depois de restaurar todos os Uris do AKV."

Para atenuar isso, execute o cmdlet [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) para retornar a lista de chaves do Key Vault que foram adicionadas ao servidor (a menos que tenham sido excluídas por um usuário). Para garantir que todos os backups podem ser restaurados, verifique se o servidor de destino para o backup tem acesso a todas essas chaves.

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
Para saber mais sobre a recuperação de backup do Banco de Dados SQL, consulte [Recuperar um Banco de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups). Para saber mais sobre a recuperação de backup do SQL Data Warehouse, consulte [Recuperar um SQL Data Warehouse do Azure](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview).
