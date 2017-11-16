---
title: "TDE – Bring Your Own Key – SQL do Azure | Microsoft Docs"
description: "Uma visão geral do suporte a Bring Your Own Key para Transparent Data Encryption com o Azure Key Vault para Data Warehouse e Banco de Dados SQL. O documento aborda os benefícios do recurso, como ele funciona, considerações e recomendações."
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: cguyer
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: Inactive
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.openlocfilehash: 35e51899bda60ccb5b176de0a3d7fabcc86faad7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehouse"></a>Transparent Data Encryption com suporte a Bring Your Own Key para Data Warehouse e Banco de Dados SQL do Azure

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

O suporte a BYOK (Bring Your Own Key) para [TDE (Transparent Data Encryption)](transparent-data-encryption.md) permite que o você tenha controle sobre suas chaves de criptografia de TDE e controle quem pode acessá-las e quando. O [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), o sistema de gerenciamento de chaves externas baseado em nuvem do Azure, é o primeiro serviço de gerenciamento de chaves com o qual a TDE tem suporte integrado a BYOK. Com o BYOK, a chave de criptografia do banco de dados é protegida por uma chave assimétrica armazenada no Key Vault. A chave assimétrica é definida no nível do servidor e herdada por todos os bancos de dados no servidor. 

Com suporte a BYOK, os usuários agora podem controlar tarefas de gerenciamento de chaves, incluindo rotações de chave, permissões do cofre de chaves, exclusão de chaves e habilitação de auditoria/relatórios em todas as chaves de criptografia. O Key Vault fornece o gerenciamento de chaves central, aproveita os HSMs (módulos de segurança de hardware) monitorados e promove a separação do gerenciamento de chaves e de dados para ajudar a atender à conformidade regulatória. 

A TDE com BYOK fornece os seguintes benefícios:
- Maior controle granular e transparência com a capacidade de autogerenciar o Protetor de TDE   
- Gerenciamento central das chaves de criptografia de TDE (juntamente com outras chaves e segredos usados em outros serviços do Azure) hospedando-as no Key Vault
- Separação do gerenciamento de dados e de chaves dentro da organização, para dar suporte à separação de funções
- Maior confiança de seus próprios clientes, uma vez que o Key Vault é projetado de forma que a Microsoft não veja ou extraia nenhuma chave de criptografia. 
- Suporte para rotação de chaves

> [!IMPORTANT]
> Para aqueles que usam a TDE gerenciada por serviço que gostariam de começar a usar o Key Vault, a TDE permanece ativada durante o processo de troca para uma chave no Key Vault. Não há nenhum tempo de inatividade nem nova criptografia dos próprios arquivos do banco de dados. Mudar de uma chave gerenciada por serviço para uma chave do Key Vault requer uma nova criptografia da chave de criptografia do banco de dados, que é uma operação online e rápida.
>

## <a name="how-does-tde-with-byok-support-work"></a>Como a TDE com suporte a BYOK funciona?
 
![Autenticação do servidor para o Key Vault](./media/transparent-data-encryption-byok-azure-sql/tde-byok-server-authentication-flow.PNG)

Quando a TDE está configurada para usar uma chave do Key Vault, o servidor envia a chave de criptografia de banco de dados de cada banco de dados habilitado para TDE para o Key Vault para uma solicitação *wrap key*. O Key Vault retorna a chave de criptografia do banco de dados criptografado, que é armazenada no banco de dados do usuário. 

É importante observar que **quando uma chave é armazenada no Key Vault, ela nunca deixa o Key Vault**. Uma chave com backup no HSM (módulo de segurança de hardware) no Key Vault nunca deixa o limite de segurança do HSM. O servidor pode apenas enviar solicitações de operação de chave para o material da chave do Protetor de TDE no Key Vault. O administrador do Key Vault tem o direito de revogar permissões do Key Vault para o servidor a qualquer momento, caso em que todas as conexões com o servidor são cortadas. 

## <a name="considerations"></a>Considerações

Usar a TDE com BYOK traz tarefas de gerenciamento de chave e custos relacionados adicionais para o uso do cofre de chaves em si. Essas considerações são discutidas nas próximas duas seções.

### <a name="key-management-responsibilities"></a>Responsabilidades de gerenciamento de chaves

Assumir o gerenciamento de chave de criptografia dos recursos de um aplicativo é uma responsabilidade importante. Ao usar a TDE com BYOK por meio do Key Vault, as tarefas a seguir são as tarefas de gerenciamento de chaves que você está assumindo:
- **Rotações de chave:** os Protetores de TDE devem ser girados de acordo com as regulamentações internas ou com os requisitos de conformidade. As rotações de chave podem ser feitas por meio do cofre de chaves do Protetor de TDE.  
- **Permissões do Key Vault**: as permissões no Key Vault são provisionadas em um nível de servidor e de cofre de chaves. As permissões do servidor para um cofre de chaves podem ser revogadas a qualquer momento usando a política de acesso do cofre de chaves.
- **Exclusão de chaves**: as chaves podem ser removidas do Key Vault e do SQL Server para fornecer segurança adicional ou para fins de conformidade.
- **Auditoria/relatórios em todas as chaves de criptografia**: o Key Vault fornece logs que são fáceis de injetar em outras ferramentas de SIEM (gerenciamento de evento e informações de segurança). O [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-key-vault) do OMS (Operations Management Suite) é um serviço de exemplo que já está integrado.

### <a name="pricing-considerations"></a>Considerações sobre preços 

A TDE com suporte a BYOK é uma funcionalidade de segurança integrado ao Data Warehouse e no Banco de Dados SQL do Azure sem taxas adicionais. No entanto, há custos relacionados para o uso do Key Vault em si. As operações do Key Vault realizadas pelo servidor são cobradas como operações normais para seu cofre e seguem o [preço](https://azure.microsoft.com/pricing/details/key-vault/) do Key Vault. O servidor envia solicitações ao Key Vault para os seguintes eventos:
- Reinicializações de instância do SQL
- Sobreposições de chave
- A cada seis horas para verificar se foram feitas alterações nas permissões do servidor para o cofre de chaves

## <a name="important-warnings"></a>Avisos importantes

### <a name="loss-of-access-to-keys"></a>Perda de acesso às chaves

Depois que um servidor não tem mais acesso ao Protetor de TDE (seja pela remoção das permissões do Key Vault ou pela exclusão de uma chave), **todas as conexões com os bancos de dados criptografados no servidor são bloqueadas e esses bancos de dados ficam offline e são descartados dentro de 24 horas**. Backups antigos criptografados com a chave indisponível não são mais acessíveis. Se houver um caso extremo em que há suspeita de uma chave estar comprometida (como um serviço ou usuário ter tido acesso não autorizado à chave), é melhor exclui-la seguindo as diretrizes em [Remover uma chave potencialmente comprometida](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md). Os bancos de dados devem ser descartados antes da exclusão de um Protetor de TDE ativo para evitar até 10 minutos de perda de dados.  

### <a name="expired-keys"></a>Chaves expiradas

Como a disponibilidade do Protetor de TDE afeta diretamente a disponibilidade do banco de dados, uma chave com uma data de expiração não pode ser adicionada a um SQL Server. Se uma chave já for usada como um Protetor de TDE para um servidor e posteriormente for adicionada uma data de expiração no Azure Key Vault, **após a chave expirar, os bancos de dados criptografados não terão mais acesso ao seu Protetor de TDE e serão descartados dentro de 24 horas.**

### <a name="deleted-server-identities"></a>Identidades de servidor excluídas 

O acesso do servidor ao Key Vault é gerenciado por meio da identidade do AAD (Azure Active Directory) exclusiva do servidor. Portanto, se a identidade do servidor for excluída do AAD, o servidor perderá o acesso aos seus cofres de chaves. Como resultado, **todas as conexões com os bancos de dados criptografados no servidor são bloqueadas e esses bancos de dados ficam offline e são descartados dentro de 24 horas.**

## <a name="limitations"></a>Limitações

Os cofres de chave sendo usados para a TDE devem estar no mesmo locatário do AAD que o servidor do Data Warehouse ou do Banco de Dados SQL. Não há suporte para interações de servidor e cofre de chaves entre locatários. Um recurso que está sendo criptografado com uma chave do Key Vault não pode ser movido entre assinaturas do Azure. Mover o recurso em assinaturas interrompe os controles de acesso do Key Vault necessários que tornam a TDE com BYOK possível. Se algum recurso precisar ser movido para outra assinatura, altere o modo da TDE de BYOK para [TDE gerenciada por serviço](transparent-data-encryption-azure-sql.md). 

Não há suporte para os Protetores de TDE exclusivos para um banco de dados ou data warehouse. O Protetor de TDE é definido no nível do servidor e herdado por todos os recursos no servidor. 

## <a name="guidelines-for-managing-encrypted-databases"></a>Diretrizes para gerenciar bancos de dados criptografados

### <a name="high-availability-and-disaster-recovery"></a>Alta disponibilidade e recuperação de desastre
  
Há duas maneiras em que a replicação geográfica pode ser configurada para servidores usando o Key Vault: 

- **Cofre de chaves separado**: cada servidor tem acesso a um cofre de chaves separado (o ideal é cada um dentro de sua própria região do Azure). Essa é a configuração recomendada, já que cada servidor tem sua própria cópia do Protetor de TDE para os bancos de dados criptografados replicados geograficamente. Se uma das regiões do Azure do servidor ficar offline, os outros servidores poderão continuar a acessar os bancos de dados replicados geograficamente.   

- **Key vault compartilhado**: todos os servidores compartilham o mesmo cofre de chaves. Essa configuração é mais fácil de definir, mas se a região do Azure em que o cofre de chaves estiver localizado ficar offline, todos os servidores não poderão ler os bancos de dados replicados geograficamente criptografados ou seus próprios bancos de dados criptografados. 
 
Para começar, use o cmdlet [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) para adicionar cada chave do Key Vault do servidor aos outros servidores em um link de replicação geográfica.  
(Exemplo de um KeyId do Key Vault: *https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h*)

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

Para atenuar isso, execute o cmdlet [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) para retornar a lista de chaves do Key Vault que foram adicionadas ao servidor. Para garantir que todos os backups podem ser restaurados, verifique se o servidor de destino para o backup tem acesso a todas essas chaves.

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
Para saber mais sobre a recuperação de backup do Banco de Dados SQL, consulte [Recuperar um Banco de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups). Para saber mais sobre a recuperação de backup do SQL Data Warehouse, consulte [Recuperar um SQL Data Warehouse do Azure](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview).

## <a name="best-practices"></a>Práticas recomendadas

### <a name="key-management"></a>Gerenciamento de chaves 

Para garantir a rápida recuperação da chave e o acesso aos seus dados fora do Azure, recomendamos o seguinte:
- Crie sua chave de criptografia localmente em um dispositivo HSM local. (Certifique-se de que é uma chave RSA 2048 assimétrica para ela poder ser armazenada no Azure Key Vault.)
- Importe o arquivo de chave de criptografia (.pfx, .byok ou .backup) para o Azure Key Vault. Considere a possibilidade de usar um Key Vault com [exclusão reversível](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete) habilitada para proteção de recuperação contra exclusão acidental de chaves.
- Antes de usar a chave no Cofre de Chaves do Azure pela primeira vez, faça um backup da chave do Cofre de Chaves do Azure. Saiba mais sobre o comando [Backup-AzureKeyVaultKey](https://msdn.microsoft.com/library/mt126292.aspx) .
- Sempre que qualquer alteração for feita na chave (por exemplo, adicionar ACLs, adicionar marcas, adicionar atributos da chave), certifique-se de fazer outro backup da chave do Azure Key Vault.
- Durante a substituição de chave, **mantenha as versões anteriores da chave** no cofre de chaves para que os backups do banco de dados mais antigos possam ser restaurados. 

Criar a chave de criptografia da TDE localmente primeiro e importar a chave assimétrica é altamente recomendável para cenários de produção, pois ela permite que o administrador garanta a chave em um sistema de caução de chaves. Se a chave assimétrica for criada no Azure Key Vault, ela não poderá ser mantida em garantia porque a chave privada nunca pode deixar o cofre. As chaves usadas para proteger dados críticos devem ser mantidas em garantia. A perda de uma chave assimétrica resulta em dados irrecuperáveis permanentemente.

### <a name="pre-configuration-for-replicated-databases"></a>Configuração prévia de bancos de dados replicados

Se um banco de dados criptografado for ser replicado para outro servidor, certifique-se de que o servidor tenha acesso a uma cópia do material da chave do Key Vault usado em outro servidor **antes** de mover ou replicar o banco de dados.  

É recomendável que cada servidor tenha acesso a uma cópia do material da chave do Key Vault usado em outro servidor, que é armazenado em um cofre de chaves separado (idealmente cada um dentro da mesma região do Azure que o servidor). Com essa configuração, cada servidor tem sua própria cópia do Protetor de TDE para bancos de dados replicados criptografados. Se uma das regiões do Azure do servidor ficar offline, os outros servidores poderão continuar a acessar os bancos de dados replicados.

## <a name="next-steps"></a>Próximas etapas

- Introdução ao suporte para Bring Your Own Key para a TDE: [Ativar a TDE usando sua própria chave do Key Vault usando o PowerShell](transparent-data-encryption-byok-azure-sql-configure.md)
- Saiba como girar o Protetor de TDE de um servidor para atender aos requisitos de segurança: [Girar o Protetor de Transparent Data Encryption usando o PowerShell](transparent-data-encryption-byok-azure-sql-key-rotation.md)
- No caso de um risco de segurança, saiba como remover um Protetor de TDE potencialmente comprometido: [Remover uma chave potencialmente comprometida](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) 
