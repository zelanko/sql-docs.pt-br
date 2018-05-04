---
title: TDE – BYOK (Bring Your Own Key) – SQL do Azure | Microsoft Docs
description: Suporte a BYOK (Bring Your Own Key) na TDE (Transparent Data Encryption) com o Azure Key Vault para o Banco de Dados SQL e Data Warehouse. Visão geral da TDE com BYOK, benefícios, modo de funcionamento, considerações e recomendações.
keywords: ''
services: sql-database
documentationcenter: ''
author: aliceku
manager: craigg
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: ''
ms.component: security
ms.workload: On Demand
ms.tgt_pltfrm: ''
ms.topic: article
ms.date: 04/19/2018
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 1ca79d0f6c4bc501e7b03cd0c5b710eba2b50adf
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehouse"></a>Transparent Data Encryption com suporte a Bring Your Own Key para Data Warehouse e Banco de Dados SQL do Azure
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
- Ao configurar a TDE com BYOK, é importante considerar a carga colocada no cofre de chaves por operações repetidas de encapsulamento/desencapsulamento. Por exemplo, já que todos os bancos de dados associados a um servidor lógico usam o mesmo protetor de TDE, um failover desse servidor disparará um número de operações de chave destinadas ao cofre que será equivalente ao número de bancos de dados no servidor. Com base em nossa experiência e nos [limites de serviço do cofre de chaves](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-service-limits) documentados, recomendamos associar no máximo 500 bancos de dados Standard/Uso Geral ou 200 bancos de dados Premium/Comercialmente Críticos a um Azure Key Vault em uma assinatura única para garantir alta disponibilidade de forma consistente ao acessar o protetor de TDE no cofre. 
- Recomendado: manter uma cópia local do protetor de TDE.  Isso exige um dispositivo HSM para criar um protetor de TDE localmente e um sistema de caução de chave para armazenar uma cópia local do protetor de TDE.


### <a name="guidelines-for-configuring-azure-key-vault"></a>Diretrizes para a configuração do Azure Key Vault

- Crie um cofre de chaves com [exclusão reversível](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete) habilitada para proteger contra a perda de dados no caso da exclusão acidental da chave ou do cofre de chaves.  É necessário usar o [PowerShell para habilitar a propriedade de "exclusão reversível"](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-soft-delete-powershell) no cofre de chaves (essa opção ainda não está disponível no Portal do AKV – mas é obrigatória no SQL):  
  - Os recursos excluídos com a exclusão reversível são retidos por um determinado período, 90 dias a menos que eles sejam recuperados ou limpos.
  - As ações de **recuperação** e **limpeza** têm suas próprias permissões associadas em uma política de acesso do cofre de chaves. 

- Conceda ao servidor lógico o acesso ao cofre de chaves usando sua identidade do Microsoft Azure AD (Azure Active Directory).  Ao usar a interface do usuário do Portal, a identidade do Microsoft Azure AD é criada automaticamente e as permissões de acesso do cofre de chaves são concedidas ao servidor.  Usando o PowerShell para configurar a TDE com BYOK, é necessário criar a identidade do Microsoft Azure AD e verificar a conclusão. Consulte [Configurar a TDE com BYOK](transparent-data-encryption-byok-azure-sql-configure.md) para obter instruções passo a passo detalhadas ao usar o PowerShell.

  >[!NOTE]
  >Se a identidade do Microsoft Azure AD **for acidentalmente excluída ou as permissões do servidor forem revogadas** usando a política de acesso do cofre de chaves, o servidor perderá o acesso ao cofre de chaves.
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

## <a name="how-to-configure-geo-dr-with-azure-key-vault"></a>Como configurar a recuperação de desastres geográfica com o Azure Key Vault

Para manter a alta disponibilidade de Protetores TDE para bancos de dados criptografados, é necessário configurar Azure Key Vaults redundantes com base nos grupos de failover ou instâncias de replicação geográfica ativas do Banco de Dados SQL desejado ou existente.  Cada servidor com replicação geográfica requer um cofre de chaves separado, que deve estar colocalizado com o servidor na mesma região do Azure. Caso um banco de dados primário se torne inacessível devido a uma interrupção em uma região e um failover seja acionado, o banco de dados secundário é capaz de assumir usando o cofre de chaves secundário. 
 
Para bancos de dados SQL do Azure com replicação geográfica, é necessária a seguinte configuração do Azure Key Vault:
- Um banco de dados primário com um cofre de chaves na região e um banco de dados secundário com um cofre de chaves na região. 
- Pelo menos um secundário é necessário; há suporte para até quatro secundários. 
- Não há suporte para secundários de secundários (encadeamento).

A seção a seguir apresentará as etapas de instalação e de configuração em mais detalhes. 

### <a name="azure-key-vault-configuration-steps"></a>Etapas de configuração do Azure Key Vault

- Instalar o [PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps?view=azurermps-5.6.0) 
- Crie dois Azure Key Vaults em duas regiões diferentes usando o [PowerShell para habilitar a propriedade de "exclusão reversível"](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-soft-delete-powershell) nos cofres de chaves (essa opção ainda não está disponível no Portal do AKV – mas é obrigatória no SQL).
- Ambos os Azure Key Vaults devem estar localizados nas duas regiões disponíveis na mesma Área Geográfica do Azure para que o backup e a restauração de chaves funcione.  Se precisar que os dois cofres de chaves estejam localizados em áreas geográficas diferentes para atender aos requisitos de Geo-DR do SQL, siga o [Processo BYOK](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-hsm-protected-keys) que permite a importação das chaves de um HSM local.
- Crie uma nova chave no primeiro cofre de chaves:  
  - Chave RSA/RSA-HSA 2048 
  - Nenhuma data de expiração 
  - A chave está habilitada e tem permissões para executar as operações get, wrap key e unwrap key 
- Faça backup da chave primária e restaure a chave para o segundo cofre de chaves.  Consulte [BackupAzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) e [Restore-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey?view=azurermps-5.5.0). 

### <a name="azure-sql-database-configuration-steps"></a>Etapas de configuração do Banco de Dados SQL do Azure

As seguintes etapas de configuração serão diferentes se iniciarem com uma nova implantação do SQL ou se trabalharem com uma implantação de recuperação de desastres geográfica do SQL.  Descrevemos as etapas de configuração para uma nova implantação primeiro e, em seguida, explicamos como atribuir Protetores de TDE armazenados no Azure Key Vault a uma implantação existente que já tem um link de recuperação de desastres geográfica estabelecido. 

Etapas para uma nova implantação:
- Crie os dois servidores SQL lógicos nas mesmas duas regiões que os cofres de chaves criados anteriormente. 
- Selecione o painel TDE do servidor lógico e, para cada SQL Server lógico:  
   - Selecione o AKV na mesma região 
   - Selecione a chave a ser usada como o Protetor de TDE – cada servidor usará a cópia local do Protetor de TDE. 
   - Fazer isso no Portal criará uma [AppID](https://docs.microsoft.com/en-us/azure/active-directory/managed-service-identity/overview) para o SQL Server lógico, que será usada para atribuir as permissões do SQL Server lógico para acessar o cofre de chaves. Não exclua essa identidade.  O acesso pode ser revogado com a remoção das permissões no Azure Key Vault. para o SQL Server lógico, que é usado para atribuir as permissões do SQL Server lógico para acessar o cofre de chaves.
- Crie o banco de dados primário. 
- Siga a [diretriz para replicação geográfica ativa](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview) para completar o cenário. Essa etapa criará o banco de dados secundário.

![Grupos de failover e recuperação de desastres geográfica](./media/transparent-data-encryption-byok-azure-sql/Geo_DR_Config.PNG)

>[!NOTE]
>É importante garantir que os mesmos Protetores de TDE estão presentes em ambos os cofres de chaves antes de passar para o estabelecimento do link de replicação geográfica entre os bancos de dados.
>

Etapas de um banco de dados SQL existente com implantação de recuperação de desastres geográfica:

Como os servidores SQL lógicos já existem, e os bancos de dados primários e secundários já estão atribuídos, as etapas para configurar o Azure Key Vault deverão ser executadas na seguinte ordem: 
- Comece com o SQL Server lógico que hospeda o banco de dados secundário: 
   - Atribua o cofre de chaves localizado na mesma região 
   - Atribua o Protetor de TDE 
- Agora acesse o SQL Server lógico que hospeda o banco de dados primário: 
   - Selecione o mesmo Protetor de TDE que o usado para o BD secundário
   
![Grupos de failover e recuperação de desastres geográfica](./media/transparent-data-encryption-byok-azure-sql/geo_DR_ex_config.PNG)

>[!NOTE]
>Ao atribuir o cofre de chaves ao servidor, é importante começar com o servidor secundário.  Na segunda etapa, atribua o cofre de chaves ao servidor primário e atualize o Protetor de TDE. O link de recuperação de desastres geográfica continuará funcionando, porque, nesse momento, o Protetor de TDE usado pelo banco de dados replicado estará disponível para ambos os servidores.
>

Antes de habilitar o TDE com as chaves gerenciadas pelo cliente no Azure Key Vault para um cenário de recuperação de desastres geográfica do Banco de Dados SQL, é importante criar e manter dois Azure Key Vaults com conteúdos idênticos nas mesmas regiões que serão usadas para a replicação geográfica do Banco de Dados SQL.  "Conteúdos idênticos" significa especificamente que ambos os cofres de chaves devem conter cópias dos mesmos Protetores de TDE para que ambos os servidores tenham acesso ao uso de Protetores de TDE por todos os bancos de dados.  Avançando, é necessário manter os dois cofres de chaves em sincronia, o que significa que eles devem conter as mesmas cópias de Protetores de TDE após a rotação de chaves, manter versões antigas de chaves usadas para arquivos de log ou backups, os Protetores de TDE devem manter as mesmas propriedades de chave e os cofres de chaves devem manter as mesmas permissões de acesso para SQL.  
 
Siga as etapas em [Visão geral de replicação geográfica ativa](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) para testar e disparar um failover, que deve ser feito regularmente para confirmar que as permissões de acesso para o SQL para ambos os cofres de chaves tenham sido mantidas. 


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


Consideração adicional para backup de arquivos de log: o resultado do backup de arquivos de log permanece criptografado com o Criptografador TDE original, mesmo se houve rodízio do protetor de TDE e o banco de dados agora usa um novo protetor de TDE.  No momento da restauração, as duas chaves serão necessárias para restaurar o banco de dados.  Se o arquivo de log estiver usando um protetor de TDE armazenado no Azure Key Vault, essa chave será necessária no momento da restauração mesmo se, durante esse intervalo de tempo, o banco de dados tiver sido alterado para usar o TDE gerenciado por serviços.


