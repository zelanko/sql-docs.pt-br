---
title: TDE (Transparent Data Encryption) | Microsoft Docs
description: Saiba mais sobre Transparent Data Encryption que criptografa dados do SQL Server, do Banco de Dados SQL do Azure e do Azure Synapse Analytics, conhecidos como criptografia de dados em repouso.
ms.custom: ''
ms.date: 05/09/2019
ms.prod: sql
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption
- database encryption key, about
- TDE
- database encryption key
- TDE, about
- Transparent Data Encryption, about
- encryption [SQL Server], transparent data encryption
ms.assetid: c75d0d4b-4008-4e71-9a9d-cee2a566bd3b
author: jaszymas
ms.author: jaszymas
ms.reviewer: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: edb5d6b73305b9acc840c2f34461c3056a3b9cbd
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006473"
---
# <a name="transparent-data-encryption-tde"></a>Criptografia de Dados Transparente (TDE)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

A *Transparent Data Encryption* (TDE) criptografa os arquivos de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] e [!INCLUDE[ssSDWfull](../../../includes/sssdwfull-md.md)]. Essa criptografia é conhecida como criptografia de dados em repouso.

Para ajudar a proteger um banco de dados, você pode tomar precauções como:

* Projetar um sistema seguro.
* Criptografar ativos confidenciais.
* Criar um firewall em todos os servidores de banco de dados.

Mas uma parte mal-intencionada que rouba mídia física, como unidades ou fitas de backup, pode restaurar ou anexar o banco de dados e navegar em seus dados.

Uma solução é criptografar dados confidenciais em um banco de dados e usar um certificado para proteger as chaves que criptografam os dados. Essa solução impede que alguém sem as chaves use os dados. Mas você deve planejar esse tipo de proteção com antecedência.

A TDE realiza a criptografia e a descriptografia de E/S em tempo real dos arquivos de log e de dados. A criptografia usa uma DEK (chave de criptografia de banco de dados). O registro de inicialização do banco de dados armazena a chave para disponibilidade durante a recuperação. O DEK é uma chave simétrica. Ele é protegido por um certificado que o banco de dados mestre do servidor armazena ou por uma chave assimétrica que o módulo EKM protege.

A TDE protege os dados "em repouso", que são os dados e os arquivos de log. Ele permite que você siga muitas leis, regulamentos e diretrizes estabelecidos em vários setores. Isso permite que os desenvolvedores de software criptografem dados usando algoritmos de criptografia AES e 3DES, sem alterar os aplicativos existentes.

> [!IMPORTANT]
> A TDE não fornece criptografia em canais de comunicação. Para obter mais informações sobre como criptografar dados em canais de comunicação, veja [Habilitar conexões criptografadas no Mecanismo de Banco de Dados (SQL Server Configuration Manager)](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).
>
>**Tópicos relacionados:**
>
> - [Transparent Data Encryption com o Banco de Dados SQL do Azure](/azure/azure-sql/database/transparent-data-encryption-tde-overview)
> - [Introdução aos dados TDE (Transparent Data Encryption) no Azure Synapse Analytics](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql)
> - [Mover um banco de dados protegido por TDE para outro SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)
> - [Habilitar TDE no SQL Server usando EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)
> - [Usar o Conector do SQL Server com recursos de criptografia do SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)
> - [O blog de segurança do SQL Server na TDE com Perguntas frequentes](/archive/blogs/sqlsecurity/feature-spotlight-transparent-data-encryption-tde)

## <a name="about-tde"></a>Sobre a TDE

A criptografia de um arquivo de banco de dados é feita no nível da página. As páginas em um banco de dados criptografado são criptografadas antes de serem gravadas no disco e descriptografadas quando lidas na memória. A TDE não aumenta o tamanho do banco de dados criptografado.

### <a name="information-applicable-to-sssds"></a>Informações aplicáveis a [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]

Quando você usa o TDE com o [!INCLUDE[sqldbesa](../../../includes/sqldbesa-md.md)] V12, o [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] cria automaticamente para você o certificado no nível de servidor armazenado no banco de dados mestre. Para mover um banco de dados TDE no [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], não é necessário descriptografar o banco de dados para a operação de movimentação. Para obter mais informações sobre como usar a TDE com [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], confira [Transparent Data Encryption com o Banco de Dados SQL do Azure](/azure/azure-sql/database/transparent-data-encryption-tde-overview).

### <a name="information-applicable-to-ssnoversion"></a>Informações aplicáveis a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]

Depois de proteger um banco de dados, você pode restaurá-lo usando o certificado correto. Para obter mais informações sobre certificados, consulte [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).

Depois de habilitar o TDE, faça backup imediatamente do certificado e de sua chave privada associada. Se o certificado ficar não disponível ou se você restaurar ou anexar o banco de dados em outro servidor, precisará de backups do certificado e da chave privada. Caso contrário, você não poderá abrir o banco de dados.

Mantenha o certificado de criptografia mesmo se você tiver desabilitado o TDE no banco de dados. Embora o banco de dados não esteja criptografado, partes do log de transações podem permanecer protegidas. Você também pode precisar do certificado para algumas operações até fazer um backup completo do banco de dados.

Você ainda pode usar um certificado que exceda sua data de validade para criptografar e descriptografar dados com o TDE.

### <a name="encryption-hierarchy"></a>Hierarquia de criptografia

A ilustração a seguir mostra a arquitetura de criptografia da TDE. Somente os itens de nível de banco de dados (a chave de criptografia do banco de dados e partes de ALTER DATABASE) são configuráveis pelo usuário quando você usa o TDE em [!INCLUDE[ssSDS](../../../includes/sssds-md.md)].

![A arquitetura Transparent Database Encryption](../../../relational-databases/security/encryption/media/tde-architecture.png)

## <a name="enable-tde"></a>Habilitar a TDE

Para usar a TDE, execute estes procedimentos.

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

1. Crie uma chave mestra.

1. Crie ou obtenha um certificado protegido pela chave mestra.

1. Crie uma chave de criptografia de banco de dados e proteja-a usando o certificado.

1. Defina o banco de dados para usar criptografia.

O exemplo a seguir mostra a criptografia e a descriptografia do banco de dados `AdventureWorks2012` usando um certificado chamado `MyServerCert` que está instalado no servidor.

```sql
USE master;
GO
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';
go
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';
go
USE AdventureWorks2012;
GO
CREATE DATABASE ENCRYPTION KEY
WITH ALGORITHM = AES_128
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;
GO
ALTER DATABASE AdventureWorks2012
SET ENCRYPTION ON;
GO
```

As operações de criptografia e descriptografia são agendadas em threads em segundo plano pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para ver o status dessas operações, use as exibições do catálogo e de gerenciamento dinâmico na tabela mostrada posteriormente neste artigo.

> [!CAUTION]
> Arquivos de backup para banco de dados que têm a TDE habilitada também são criptografados com a chave de criptografia do banco de dados. Como resultado, quando você restaura esses backups, o certificado que protege a chave de criptografia do banco de dados deve estar disponível. Portanto, além de fazer backup do banco de dados, mantenha os backups dos certificados do servidor. Ocorre perda de dados se os certificados não estão mais disponíveis.
>
> Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).

## <a name="commands-and-functions"></a>Comandos e funções

Para as instruções a seguir aceitarem certificados TDE, use uma chave mestra de banco de dados para criptografá-los. Se você criptografá-los apenas por senha, as instruções os rejeitarão como criptografadores.

> [!IMPORTANT]
> Se você tornar os certificados protegidos por senha depois que a TDE os usar, o banco de dados ficará inacessível após uma reinicialização.

A seguinte tabela fornece links e explicações de comandos e funções da TDE:

|Comando ou função|Finalidade|
|-------------------------|-------------|
|[CREATE DATABASE ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)|Cria uma chave que criptografa um banco de dados| 
|[ALTER DATABASE ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-database-encryption-key-transact-sql.md)|Altera a chave que criptografa um banco de dados|
|[DROP DATABASE ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-database-encryption-key-transact-sql.md)|Remove a chave que criptografa um banco de dados|
|[Opções ALTER DATABASE SET (Transact-SQL)](../../../t-sql/statements/alter-database-transact-sql-set-options.md)|Explica a opção **ALTER DATABASE** usada para habilitar a TDE|

## <a name="catalog-views-and-dynamic-management-views"></a>Exibições do catálogo e exibições de gerenciamento dinâmico

 A tabela a seguir mostra exibições do catálogo de TDE e exibições de gerenciamento dinâmico.

|Exibição do catálogo ou exibição de gerenciamento dinâmico|Finalidade|
|---------------------------------------------|-------------|
|[sys.databases (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|Exibição do catálogo que mostra informações do banco de dados|
|[sys.certificates (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|Exibição do catálogo que mostra os certificados em um banco de dados|
|[sys.dm_database_encryption_keys (Transact-SQL)](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)|Exibição de gerenciamento dinâmico que fornece informações sobre chaves de criptografia e estado de criptografia de um banco de dados|

## <a name="permissions"></a>Permissões

Cada recurso e comando da TDE têm requisitos individuais de permissões, conforme descrito nas tabelas anteriores.

A exibição de metadados envolvidos com TDE requer a permissão VIEW DEFINITION em um certificado.

## <a name="considerations"></a>Considerações

Quando um exame de recriptografia para uma operação de criptografia de banco de dados está em andamento, as operações de manutenção no banco de dados são desabilitadas. Você pode usar a configuração de modo de usuário único para o banco de dados executar as operações de manutenção. Para obter mais informações, veja [Definir um banco de dados como modo de usuário único](../../../relational-databases/databases/set-a-database-to-single-user-mode.md).

Use o modo de exibição de gerenciamento dinâmico sys.dm_database_encryption_keys para descobrir o estado da criptografia de banco de dados. Para obter mais informações, veja a seção "Exibições de catálogo e exibições de gerenciamento dinâmico" no início deste artigo.

Na TDE, todos os arquivos e os grupos de arquivos em um banco de dados são criptografados. Se qualquer grupo de arquivos em um banco de dados estiver marcado como somente leitura, a operação de criptografia de banco de dados falhará.

Se você usar um banco de dados no espelhamento de banco de dados ou no envio de logs, ambos os bancos serão criptografados. As transações de logs são criptografadas quando enviadas entre eles.

> [!IMPORTANT]
> Índices de texto completo novos são criptografados quando um banco de dados for definido para criptografia. Esses índices criados em uma versão SQL Server anterior ao SQL Server 2008 são importados para o banco de dados do SQL Server 2008 ou posterior e são criptografados pelo TDE.

> [!TIP]
> Para monitorar alterações no status de TDE do banco de dados, use a Auditoria do SQL Server ou a auditoria de Banco de Dados SQL. Para o SQL Server, o TDE é controlado no grupo de ações de auditoria DATABASE_CHANGE_GROUP, que você pode encontrar em [Ações e grupos de ações de auditoria do SQL Server](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).

## <a name="restrictions"></a>Restrições

As seguintes operações são proibidas durante criptografia de banco de dados inicial, alteração de chave ou descriptografia de banco de dados:

- Descartar um arquivo de um grupo de arquivos em um banco de dados

- Cancelar um banco de dados

- Colocar um banco de dados offline

- Desanexando um banco de dados

- Fazendo a transição de um banco de dados ou grupo de arquivos para um estado READ ONLY

As seguintes operações são proibidas durante a execução das instruções CREATE DATABASE ENCRYPTION KEY, ALTER DATABASE ENCRYPTION KEY, DROP DATABASE ENCRYPTION KEY e ALTER DATABASE...SET ENCRYPTION:

- Descartar um arquivo de um grupo de arquivos em um banco de dados

- Cancelar um banco de dados

- Colocar um banco de dados offline

- Desanexando um banco de dados

- Fazendo a transição de um banco de dados ou grupo de arquivos para um estado READ ONLY

- Usar um comando ALTER DATABASE

- Iniciar um banco de dados ou backup de arquivo de banco de dados

- Iniciar um banco de dados ou restauração de arquivo de banco de dados

- Criar um instantâneo

As seguintes operações ou condições impedem a execução das instruções CREATE DATABASE ENCRYPTION KEY, ALTER DATABASE ENCRYPTION KEY, DROP DATABASE ENCRYPTION KEY e ALTER DATABASE...SET ENCRYPTION:

- Um banco de dados é somente leitura ou tem grupos de arquivos somente leitura.

- Um comando ALTER DATABASE está em execução.

- Um backup de dados está sendo executado.

- Um banco de dados está em condição de restauração ou offline.

- Um instantâneo está em andamento.

- As tarefas de manutenção do banco de dados estão em execução.

Quando os arquivos de banco de dados são criados, a inicialização instantânea de arquivo fica não disponível quando o TDE está habilitado.

Para criptografar a chave de criptografia do banco de dados com uma chave assimétrica, a chave assimétrica deve estar em um provedor de gerenciamento extensível de chaves.

## <a name="tde-scan"></a>Verificação da TDE

Para habilitar o TDE em um banco de dados, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve fazer uma verificação de criptografia. A verificação lê cada página dos arquivos de dados no pool de buffers e, em seguida, grava as páginas criptografadas de volta no disco.

Para fornecer a você mais controle sobre a verificação de criptografia, [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] apresenta a verificação de TDE, que tem uma sintaxe de suspensão e de retomada. Você pode pausar a verificação, enquanto a carga de trabalho no sistema é pesada ou durante horários críticos para os negócios e então retomar a verificação mais tarde.

Use a sintaxe a seguir para pausar a verificação de criptografia de TDE:

```sql
ALTER DATABASE <db_name> SET ENCRYPTION SUSPEND;
```

Da mesma forma, use a seguinte sintaxe para retomar a verificação de criptografia TDE:

```sql
ALTER DATABASE <db_name> SET ENCRYPTION RESUME;
```

A coluna encryption_scan_state foi adicionada à exibição de gerenciamento dinâmico sys.dm_database_encryption_keys. Ela mostra o estado atual da verificação de criptografia. Há também uma nova coluna chamada encryption_scan_modify_date, que contém a data e a hora da última alteração de estado de verificação de criptografia.

Se a instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] for reiniciada enquanto sua verificação de criptografia estiver suspensa, uma mensagem será registrada no log de erros na inicialização. A mensagem indica que uma verificação existente foi colocada em pausa.

## <a name="tde-and-transaction-logs"></a>TDE e logs de transações

Deixar um banco de dados usar TDE remove a parte restante do log de transações virtual atual. A remoção força a criação do próximo log de transações. Esse comportamento garante que nenhum texto não criptografado seja deixado nos logs depois que o banco de dados for definido para criptografia.

Para localizar o status da criptografia do arquivo de log, confira a coluna `encryption_state` na exibição `sys.dm_database_encryption_keys`, como neste exemplo:

```sql
USE AdventureWorks2012;
GO
/* The value 3 represents an encrypted state
   on the database and transaction logs. */
SELECT *
FROM sys.dm_database_encryption_keys
WHERE encryption_state = 3;
GO
```

Para obter mais informações sobre a arquitetura de arquivos de log do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], veja [O log de transações (SQL Server)](../../../relational-databases/logs/the-transaction-log-sql-server.md).

Antes de uma chave de criptografia de banco de dados ser alterada, a chave de criptografia de banco de dados anterior criptografa todos os registros gravados no log de transações.

Se você alterar uma chave de criptografia de banco de dados duas vezes, deverá fazer um backup de log antes de poder alterar a chave de criptografia de banco de dados novamente.

## <a name="tde-and-the-tempdb-system-database"></a>TDE e o banco de dados de sistema tempdb

O banco de dados do sistema **tempdb** será criptografado se qualquer outro banco de dados da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] for criptografado usando TDE. Essa criptografia poderá ter um efeito de desempenho em bancos de dados não criptografados na mesma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações sobre o banco de dados do sistema **tempdb**, confira [Banco de dados tempdb](../../../relational-databases/databases/tempdb-database.md).

## <a name="tde-and-replication"></a>TDE e replicação

A replicação não replica automaticamente os dados de um banco de dados habilitado para TDE em um formulário criptografado. Habilite separadamente a TDE se quiser proteger a distribuição e os bancos de dados dos assinantes.

A replicação de instantâneo pode armazenar dados em arquivos intermediários não criptografados, como arquivos BCP. A distribuição de dados inicial para replicação transacional e de mesclagem também pode. Durante essa replicação, você pode habilitar a criptografia para proteger o canal de comunicação.

Para obter mais informações, confira [Habilitar conexões criptografadas para o mecanismo de banco de dados (SQL Server Configuration Manager)](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).

## <a name="tde-and-always-on"></a>TDE e Always On    
Você pode [adicionar um banco de dados criptografado a um grupo de disponibilidade Always On](../../../database-engine/availability-groups/windows/encrypted-databases-with-always-on-availability-groups-sql-server.md).  

Para criptografar bancos de dados que fazem parte de um grupo de disponibilidade, crie a chave mestra e os certificados ou a chave assimétrica (EKM) em todas as réplicas secundárias antes de criar a [chave de criptografia de banco de dados](../../../t-sql/statements/create-database-encryption-key-transact-sql.md) na réplica primária.  

Se um certificado for usado para proteger a DEK (chave de criptografia de banco de dados), [faça backup do certificado](../../../t-sql/statements/backup-certificate-transact-sql.md) criado na réplica primária e, em seguida, [crie o certificado de um arquivo](../../../t-sql/statements/create-certificate-transact-sql.md) em todas as réplicas secundárias antes de criar a chave de criptografia de banco de dados na réplica primária. 

## <a name="tde-and-filestream-data"></a>TDE e os dados FILESTREAM

Os dados **FILESTREAM** não são criptografados mesmo quando você habilita TDE.

<a name="scan-suspend-resume"></a>

## <a name="remove-tde"></a>Remover a TDE

Remova a criptografia do banco de dados usando a instrução `ALTER DATABASE`.

```sql
ALTER DATABASE <db_name> SET ENCRYPTION OFF;
```

Para exibir o estado do banco de dados, use a exibição de gerenciamento dinâmico [sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md).

Aguarde a conclusão da descriptografia antes de remover a chave de criptografia de banco de dados usando [DROP DATABASE ENCRYPTION KEY](../../../t-sql/statements/drop-database-encryption-key-transact-sql.md).

> [!IMPORTANT]
> Faça backup da chave mestra e do certificado que são usados para a TDE em uma localização segura. A chave mestra e o certificado são necessários para restaurar backups que foram feitos quando o banco de dados foi criptografado com a TDE. Depois de remover a chave de criptografia de banco de dados, faça um backup de log seguido de um novo backup completo do banco de dados descriptografado. 

## <a name="tde-and-buffer-pool-extension"></a>TDE e extensão do pool de buffers

Quando você criptografa um banco de dados usando TDE, os arquivos relacionados à BPE (extensão do pool de buffers) não são criptografados. Para esses arquivos, use ferramentas de criptografia como BitLocker ou EFS no nível do sistema de arquivos.

## <a name="tde-and-in-memory-oltp"></a>TDE e OLTP in-memory

Você pode habilitar a TDE em um banco de dados que tem objetos OLTP in-memory. No [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] e no [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)], os dados e os registros de log do OLTP in-memory serão criptografados se a TDE estiver habilitada. No [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], os registros de log do OLTP in-memory serão criptografados se você habilitar a TDE, mas os arquivos no grupo de arquivos MEMORY_OPTIMIZED_DATA ficarão descriptografados.

## <a name="related-tasks"></a>Tarefas relacionadas

[Mover um banco de dados protegido por TDE para outro SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)  
[Habilitar TDE no SQL Server usando EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
[Gerenciamento extensível de chaves Usando o Azure Key Vault (SQL Server)](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  

## <a name="related-content"></a>Conteúdo relacionado

[Transparent Data Encryption com o Banco de Dados SQL do Azure](/azure/azure-sql/database/transparent-data-encryption-tde-overview)  
[Introdução aos dados TDE (Transparent Data Encryption) no Azure Synapse Analytics](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql)  
[Criptografia do SQL Server](../../../relational-databases/security/encryption/sql-server-encryption.md)  
[Chaves de criptografia do SQL Server e banco de dados (Mecanismo de Banco de Dados)](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

## <a name="see-also"></a>Confira também

[Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[FILESTREAM (SQL Server)](../../../relational-databases/blob/filestream-sql-server.md)