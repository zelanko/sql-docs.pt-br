---
title: Configurar o Always Encrypted usando o PowerShell | Microsoft Docs
description: Saiba como importar e usar o módulo SqlServer do PowerShell, que fornece cmdlets para configurar o Always Encrypted no Banco de Dados SQL do Azure e no SQL Server.
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 12f2bde5-e100-41fa-b474-2d2332fc7650
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cbfed6a62aa912eff42564a06ebc9574f8cab064
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97405377"
---
# <a name="configure-always-encrypted-using-powershell"></a>Configurar Always Encrypted usando o PowerShell
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

O módulo do SqlServer PowerShell fornece cmdlets para configurar o [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) no [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] ou no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

## <a name="security-considerations-when-using-powershell-to-configure-always-encrypted"></a>Considerações de segurança ao usar o PowerShell para configurar o Always Encrypted

Como a meta principal do Always Encrypted é garantir que os dados confidenciais criptografados estejam seguros mesmo se o sistema do banco de dados for comprometido, executar um script do PowerShell que processa chaves ou dados confidenciais no computador do SQL Server pode reduzir ou anular os benefícios do recurso. Para obter recomendações adicionais relacionadas à segurança, consulte [Security Considerations for Key Management](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)(Considerações de segurança para o Gerenciamento de Chaves).

Você pode usar o PowerShell para gerenciar chaves Always Encrypted com e sem separação de funções, oferecendo controle sobre quem tem acesso à criptografia de chaves real no repositório de chaves e quem tem acesso ao banco de dados.

 Para obter recomendações adicionais, consulte [Security Considerations for Key Management](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)(Considerações de segurança para o Gerenciamento de Chaves).

## <a name="prerequisites"></a>Pré-requisitos

Instalar o [módulo do SqlServer](/powershell/sqlserver/sqlserver/vlatest/sqlserver) em um computador seguro que NÃO seja um computador que hospeda a instância do SQL Server. O módulo pode ser instalado diretamente da Galeria do PowerShell.  Consulte as instruções de [download](../../../powershell/download-sql-server-ps-module.md) para ver mais detalhes.


## <a name="importing-the-sqlserver-module"></a><a name="importsqlservermodule"></a> Importando o módulo SqlServer 

Para carregar o módulo SqlServer:

1.  Use o cmdlet **Set-ExecutionPolicy** para definir a política de execução de script adequada.
2.  Use o cmdlet **Import-Module** para importar o módulo SqlServer.

Este exemplo carrega o módulo SqlServer.

```
# Import the SQL Server Module.  
Import-Module "SqlServer" 
```

## <a name="connecting-to-a-database"></a><a name="connectingtodatabase"></a> Conectando a um banco de dados

Alguns dos cmdlets do Always Encrypted trabalham com dados ou metadados no banco de dados e requerem que você se conecte ao banco de dados primeiro. Há dois métodos recomendados para se conectar a um banco de dados ao configurar o Always Encrypted usando o módulo SqlServer: 
1. Conectar-se usando o cmdlet **Get-SqlDatabase**.
2. Conectar-se usando o Provedor do SQL Server PowerShell.

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

### <a name="using-get-sqldatabase"></a>Usando Get-SqlDatabase
O cmdlet **Get-SqlDatabase** permite que você se conecte a um banco de dados no SQL Server ou no Banco de Dados SQL do Azure. Ele retorna um objeto de banco de dados, que você pode transmitir usando o parâmetro **InputObject** de um cmdlet que se conecta ao banco de dados. 

### <a name="using-sql-server-powershell"></a>Usando o SQL Server PowerShell

```
# Import the SqlServer module
Import-Module "SqlServer"  

# Connect to your database
# Set the valid server name, database name and authentication keywords in the connection string
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$database = Get-SqlDatabase -ConnectionString $connStr

# List column master keys for the specified database.
Get-SqlColumnMasterKey -InputObject $database
```

Como alternativa, você pode usar a barra vertical:


```
$database | Get-SqlColumnMasterKey
```

### <a name="using-sql-server-powershell-provider"></a>Usando o Provedor do SQL Server PowerShell
O [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md) expõe a hierarquia de objetos do SQL Server em caminhos semelhantes aos caminhos do sistema de arquivos. Com o SQL Server PowerShell, você pode navegar nos caminhos usando aliases do Windows PowerShell semelhantes aos comandos normalmente usados para navegar em caminhos do sistema de arquivos. Depois de navegar para a instância de destino e para o banco de dados, os cmdlets seguintes terão como destino esse banco de dados, como mostrado no exemplo a seguir. 

> [!NOTE]
> Esse método de conexão com o banco de dados funciona apenas para o SQL Server (não há suporte no Banco de Dados SQL do Azure).

```
# Import the SqlServer module.
Import-Module "SqlServer"
# Navigate to the database in the remote instance.
cd SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
# List column master keys in the above database.
Get-SqlColumnMasterKey
```

 
Como alternativa, você pode especificar um caminho de banco de dados usando o parâmetro **Path** genérico, em vez de navegar até o banco de dados.


```
# Import the SqlServer module.
Import-Module "SqlServer" 
# List column master keys for the specified database.
Get-SqlColumnMasterKey -Path SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
```
 
## <a name="always-encrypted-tasks-using-powershell"></a>Tarefas do Always Encrypted usando o PowerShell

- [Provisionar chaves do Always Encrypted usando o PowerShell](configure-always-encrypted-keys-using-powershell.md)
- [Girar chaves Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [Criptografar, criptografar novamente ou descriptografar colunas com Always Encrypted usando o PowerShell](configure-column-encryption-using-powershell.md)


##  <a name="always-encrypted-cmdlet-reference"></a><a name="aecmdletreference"></a> Referência de cmdlet do Always Encrypted

Os cmdlets do PowerShell a seguir estão disponíveis para o Always Encrypted:

|CMDLET |Descrição
|:---|:---
|**[Add-SqlAzureAuthenticationContext](/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)** |Executa a autenticação no Azure e adquire um token de autenticação.
|**[Add-SqlColumnEncryptionKeyValue](/powershell/sqlserver/sqlserver/vlatest/add-sqlcolumnencryptionkeyvalue)** |Adiciona um novo valor criptografado para um objeto de chave de criptografia da coluna existente no banco de dados.
|**[Complete-SqlColumnMasterKeyRotation](/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)** |Conclui a rotação de uma chave mestra de coluna
|**[Get-SqlColumnEncryptionKey](/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey)**   |Retorna todos os objetos de chave de criptografia de coluna no banco de dados ou retorna um objeto de chave de criptografia da coluna com o nome especificado.
|**[Get-SqlColumnMasterKey](/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnmasterkey)**   |Retorna os objetos de chave mestra da coluna definidos no banco de dados ou retorna um objeto de chave mestra da coluna com o nome especificado.
|**[Invoke-SqlColumnMasterKeyRotation](/powershell/sqlserver/sqlserver/vlatest/invoke-sqlcolumnmasterkeyrotation)** |Inicia a rotação de uma chave mestra de coluna.
|**[New-SqlAzureKeyVaultColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)** |Cria um objeto SqlColumnMasterKeySettings descrevendo uma chave assimétrica armazenada no Cofre de Chaves do Azure.
|**[New-SqlCngColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)** |Cria um objeto SqlColumnMasterKeySettings descrevendo uma chave assimétrica armazenada em um repositório de chaves com suporte à API de CNG (Cryptography Next Generation).
|**[New-SqlColumnEncryptionKey](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)**   |Cria um objeto de chave de criptografia de coluna no banco de dados.
|**[New-SqlColumnEncryptionKeyEncryptedValue](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)**   |Produz um valor criptografado de uma chave de criptografia da coluna.
|**[New-SqlColumnEncryptionSettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings)** |Cria um objeto SqlColumnEncryptionSettings que encapsula informações sobre a criptografia de uma única coluna, incluindo o tipo de criptografia e CEK.
|**[New-SqlColumnMasterKey](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)**   |Cria um objeto de chave mestra de coluna no banco de dados.
|**[New-SqlColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkeysettings)**|Cria um objeto SqlColumnMasterKeySettings para uma chave mestra de coluna com o provedor especificado e o caminho principal.
|**[New-SqlCspColumnMasterKeySettings](/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)** |Cria um objeto SqlColumnMasterKeySettings descrevendo uma chave assimétrica armazenada em um repositório de chaves com um CSP (Provedor de Serviços de Criptografia) dando suporte à CAPI (Cryptography API).
|**[Remove-SqlColumnEncryptionKey](/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkey)** |Remove o objeto de chave de criptografia da coluna do banco de dados.
|**[Remove-SqlColumnEncryptionKeyValue](/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkeyvalue)**   |Remove um valor criptografado de um objeto de chave de criptografia da coluna no banco de dados.
|**[Remove-SqlColumnMasterKey](/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)** |Remove o objeto de chave mestra da coluna do banco de dados.
|**[Set-SqlColumnEncryption](/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)** |Criptografa, descriptografa ou criptografa novamente as colunas especificadas no banco de dados.



## <a name="see-also"></a>Consulte Também

- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Visão geral do gerenciamento de chaves do Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Configurar o Always Encrypted usando o SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)
- [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md)