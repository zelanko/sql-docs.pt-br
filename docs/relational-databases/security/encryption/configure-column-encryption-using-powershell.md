---
description: Configurar a criptografia de coluna usando o Always Encrypted com o PowerShell
title: Configurar a criptografia de coluna usando o Always Encrypted com o PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 074c012b-cf14-4230-bf0d-55e23d24f9c8
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7014f349998781dcd890e84a77deb4732fe028c9
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91865755"
---
# <a name="configure-column-encryption-using-always-encrypted-with-powershell"></a>Configurar a criptografia de coluna usando o Always Encrypted com o PowerShell
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

Este artigo fornece as etapas para definir a configuração de destino Always Encrypted para colunas de banco de dados que usam o cmdlet [Set-SqlColumnEncryption](/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption) (no módulo do *SqlServer* PowerShell). O cmdlet **Set-SqlColumnEncryption** modifica tanto o esquema de banco de dados de destino quanto os dados armazenados nas colunas selecionadas. Os dados armazenados em uma coluna podem ser criptografados, criptografados novamente ou descriptografados, de acordo com as configurações de criptografia de destino especificadas para as colunas e a configuração de criptografia atual.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> Se estiver usando [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] e sua instância do SQL Server estiver configurada com um enclave seguro, você poderá executar operações criptográficas in-loco, sem mover os dados para fora do banco de dados. Confira [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md). Observe que o PowerShell não dá suporte à criptografia in-loco.

::: moniker-end
Para saber mais sobre o suporte a Always Encrypted no módulo SqlServer PowerShell para Always Encrypted, veja [Configurar o Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md).

## <a name="prerequisites"></a>Pré-requisitos

Para definir a configuração de criptografia de destino, verifique se:
- uma chave de criptografia de coluna está configurada no banco de dados (se você estiver criptografando ou criptografando novamente uma coluna). Para ver mais detalhes, confira [Configurar chaves do Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md).
- Você pode acessar a chave mestra de coluna para cada coluna que deseja criptografar, criptografar novamente ou descriptografar no computador que executa os cmdlets do PowerShell. 

## <a name="performance-and-availability-considerations"></a>Considerações sobre desempenho e disponibilidade

Para aplicar as configurações de criptografia de destino especificadas para o banco de dados, o cmdlet **Set-SqlColumnEncryption** baixa transparentemente todos os dados das colunas que contêm tabelas de destino, carrega os dados de volta para um conjunto de tabelas temporárias (com as configurações de destino criptografadas) e finalmente substitui as tabelas originais pelas novas versões das tabelas. O .NET Framework Data Provider para SQL Server subjacente criptografa ou/e descriptografa os dados no download ou/e upload, dependendo da configuração de criptografia atual da coluna de destino e das definições de criptografia de destino especificadas para as colunas de destino. A operação de movimentação dos dados pode levar algum tempo, dependendo do tamanho dos dados nas tabelas afetadas e da largura de banda da rede.

O cmdlet **Set-SqlColumnEncryption** oferece suporte a duas abordagens para definir a configuração de criptografia de destino: online e offline.

Com a abordagem offline, as tabelas de destino (e as tabelas relacionadas às tabelas de destino, por exemplo, qualquer tabela com a qual uma tabela de destino tem relações de chave estrangeira) estão disponíveis para transações por toda a duração da operação de gravação. A semântica das restrições de chave estrangeira (**CHECK** ou **NOCHECK**) sempre são preservadas ao usar a abordagem offline.

Com a abordagem online (requer o módulo do SqlServer PowerShell versão 21.x ou posterior), a operação de copiar e criptografar, descriptografar ou recriptografar os dados é realizada de forma incremental. Os aplicativos podem ler e gravar dados de/nas tabelas de destino durante a operação de movimentação de dados, exceto pela última iteração, cuja duração é limitada pelo parâmetro **MaxDownTimeInSeconds** (que você pode definir). Para detectar e processar as alterações que os aplicativos podem fazer enquanto os dados estão sendo copiados, o cmdlet habilita o [Controle de Alterações](../../track-changes/enable-and-disable-change-tracking-sql-server.md) no banco de dados de destino. Por causa disso, a abordagem online provavelmente consome mais recursos no lado do servidor que a abordagem online. A operação também pode levar muito mais tempo com a abordagem online, especialmente se uma carga de trabalho de gravação intensa estiver em execução no banco de dados. A abordagem online pode ser usada para criptografar uma tabela por vez e a tabela deve ter uma chave primária. Por padrão, as restrições de chave estrangeira são recriadas com a opção **NOCHECK** para minimizar o impacto nos aplicativos. É possível impor a preservação da semântica de restrições de chave estrangeira, especificando a opção **KeepCheckForeignKeyConstraints**. 

Aqui estão as diretrizes para escolher entre as abordagens online e offline:

Use a abordagem offline:
- Para minimizar a duração da operação. 
- Para criptografar/descriptografar/recriptografar colunas em várias tabelas ao mesmo tempo.
- Se a tabela não tem uma chave primária.

Use a abordagem online:
- Para minimizar o tempo de inatividade/indisponibilidade do banco de dados para seus aplicativos.

## <a name="security-considerations"></a>Considerações sobre segurança

O cmdlet **Set-SqlColumnEncryption** , usado para configurar a criptografia para colunas de banco de dados, gerencia chaves Always Encrypted e os dados armazenados em colunas de banco de dados. Portanto, é importante que você execute o cmdlet em um computador seguro. Se seu banco de dados estive no SQL Server, execute os cmdlets de um computador diferente daquele que hospeda a instância do SQL Server. Como o objetivo principal do Always Encrypted é garantir que os dados confidenciais criptografados estejam seguros mesmo se o sistema do banco de dados for comprometido, a execução de um script do PowerShell que processa chaves e/ou dados confidenciais no computador do SQL Server pode reduzir ou anular os benefícios do recurso.

Tarefa  |Artigo  |Acessa chaves de texto não criptografado/repositório de chaves  |Acessar banco de dados   
---|---|---|---
Etapa 1. Inicie um ambiente do PowerShell e importe o módulo do SqlServer. | [Importar o módulo do SqlServer](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | Não | Não
Etapa 2. Conecte-se ao servidor e banco de dados | [Conectando-se a um banco de dados](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | Não | Sim
Etapa 3. Autentique no Azure se a chave mestra de coluna (que protege a chave de criptografia de coluna a ser girada) estiver armazenada no Cofre de Chaves do Azure | [Add-SqlAzureAuthenticationContext](/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | Sim | Não
Etapa 4. Construir uma matriz de objetos SqlColumnEncryptionSettings - uma para cada coluna de banco de dados que você deseja criptografar, criptografar novamente ou descriptografar. SqlColumnMasterKeySettings é um objeto que existe na memória (no PowerShell). Especifica o esquema de criptografia de destino para uma coluna. | [New-SqlColumnEncryptionSettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings) | Não | Não
Etapa 5. Defina a configuração de criptografia desejada, especificada na matriz de objetos SqlColumnMasterKeySettings que você criou na etapa anterior. A coluna será criptografada, criptografada novamente ou descriptografada, dependendo das configurações de destino especificadas e a configuração de criptografia atual da coluna.| [Set-SqlColumnEncryption](/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)<br><br>**Observação:** esta etapa pode levar muito tempo. Seus aplicativos não poderão acessar as tabelas durante a operação inteira ou de parte dela, dependendo da abordagem (online versus offline) selecionada. | Sim | Sim

## <a name="encrypt-columns-using-offline-approach---example"></a>Criptografar colunas usando a abordagem offline - exemplo

O exemplo abaixo demonstra a definição da configuração da criptografia de destino para duas colunas. Se a coluna ainda não estiver criptografada, ela o será. Se qualquer coluna já estiver criptografada usando uma chave diferente e/ou um tipo de criptografia diferente, ela será descriptografada e criptografada novamente com o tipo da chave de destino especificado.


```PowerShell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Encrypt the selected columns (or re-encrypt, if they are already encrypted using keys/encrypt types, different than the specified keys/types.
$ces = @()
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.SSN" -EncryptionType "Deterministic" -EncryptionKey "CEK1"
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.BirthDate" -EncryptionType "Randomized" -EncryptionKey "CEK1"
Set-SqlColumnEncryption -InputObject $database -ColumnEncryptionSettings $ces -LogFileDirectory .
```
 
## <a name="encrypt-columns-using-online-approach---example"></a>Criptografar colunas usando a abordagem online - exemplo

O exemplo abaixo demonstra a definição da configuração da criptografia de destino para duas colunas usando a abordagem online. Se a coluna ainda não estiver criptografada, ela o será. Se qualquer coluna já estiver criptografada usando uma chave diferente e/ou um tipo de criptografia diferente, ela será descriptografada e criptografada novamente com o tipo da chave de destino especificado.

```PowerShell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Encrypt the selected columns (or re-encrypt, if they are already encrypted using keys/encrypt types, different than the specified keys/types.
$ces = @()
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.SSN" -EncryptionType "Deterministic" -EncryptionKey "CEK1"
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.BirthDate" -EncryptionType "Randomized" -EncryptionKey "CEK1"
Set-SqlColumnEncryption -InputObject $database -ColumnEncryptionSettings $ces -UseOnlineApproach -MaxDowntimeInSeconds 180 -LogFileDirectory .
```
## <a name="decrypt-columns---example"></a>Descriptografar colunas - exemplo

O exemplo a seguir mostra como descriptografar todas as colunas que estão criptografadas no momento em um banco de dados.


```PowerShell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Find all encrypted columns, and create a SqlColumnEncryptionSetting object for each column.
$ces = @()
$tables = $database.Tables
for($i=0; $i -lt $tables.Count; $i++){
    $columns = $tables[$i].Columns
    for($j=0; $j -lt $columns.Count; $j++) {
        if($columns[$j].isEncrypted) {
            $threeColPartName = $tables[$i].Schema + "." + $tables[$i].Name + "." + $columns[$j].Name 
            $ces += New-SqlColumnEncryptionSettings -ColumnName $threeColPartName -EncryptionType "Plaintext" 
        }
    }
}

# Decrypt all columns.
Set-SqlColumnEncryption -ColumnEncryptionSettings $ces -InputObject $database -LogFileDirectory .
```
 
## <a name="next-steps"></a>Próximas etapas
- [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md)

## <a name="see-also"></a>Consulte Também  
 - [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
 - [Visão geral do gerenciamento de chaves do Always Encrypted](overview-of-key-management-for-always-encrypted.md) 
 - [Configurar Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
 - [Configurar a criptografia de coluna usando o Assistente do Always Encrypted](always-encrypted-wizard.md)
 - [Configurar a criptografia de coluna usando o Always Encrypted com um pacote de DAC](configure-always-encrypted-using-dacpac.md)