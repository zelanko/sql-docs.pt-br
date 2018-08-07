---
title: Opções de Conexão | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6d1ea295-8e34-438e-8468-4bbc0f76192c
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81dc9e66bee9411841a3ee421adb73840bb2b783
ms.sourcegitcommit: f9d4f9c1815cff1689a68debdccff5e7ff97ccaf
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39367638"
---
# <a name="connection-options"></a>Opções de conexão
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico lista as opções que são permitidas na matriz associativa (ao usar [sqlsrv_connect](../../connect/php/sqlsrv-connect.md) no driver SQLSRV) ou as palavras-chave que são permitidas no dsn (nome da fonte de dados) (ao usar [PDO::__construct](../../connect/php/pdo-construct.md) no driver PDO_SQLSRV).  

## <a name="table-of-connection-options"></a>Opções de Conexão
|Chave|Valor|Descrição|Padrão|  
|-------|---------|---------------|-----------|  
|APP|Cadeia de caracteres|Especifica o nome do aplicativo usado no rastreamento.|Nenhum valor definido.|  
|ApplicationIntent|Cadeia de caracteres|Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. Os valores possíveis são ReadOnly e ReadWrite.<br /><br />Para obter mais informações sobre [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] suporte para [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], consulte [dão suporte para alta disponibilidade, recuperação de desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|ReadWrite|  
|AttachDBFileName|Cadeia de caracteres|Especifica qual arquivo de banco de dados o servidor deve anexar.|Nenhum valor definido.|  
|Autenticação|Uma das seguintes cadeias de caracteres:<br /><br />'SqlPassword'<br /><br />'ActiveDirectoryPassword'|Especifica o modo de autenticação.|Não definido.|  
|CharacterSet<br /><br />(sem suporte no driver PDO_SQLSRV)|Cadeia de caracteres|Especifica o conjunto de caracteres usado para enviar dados ao servidor.<br /><br />Os valores possíveis são SQLSRV_ENC_CHAR e UTF-8. Para obter mais informações, consulte [How to: Send and Retrieve UTF-8 Data Using Built-In UTF-8 Support](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md).|SQLSRV_ENC_CHAR|  
|ColumnEncryption|**Habilitado** ou **Desabilitado**|Especifica se o recurso Always Encrypted está habilitado ou não. |Desabilitado|  
|ConnectionPooling|1 ou **true** para pool de conexões ativado.<br /><br />0 ou **false** para pool de conexões desativado.|Especifica se a conexão é atribuída de um pool de conexões (1 ou **true**) ou não (0 ou **false**).<sup>1</sup>|**true** (1)|  
|ConnectRetryCount|Número inteiro entre 0 e 255 (inclusive)|O número máximo de tentativas para reestabelecer uma conexão interrompida antes de desistir. Por padrão, uma única tentativa é feita para restabelecer uma conexão quando quebrado. Um valor de 0 significa que nenhum reconexão será tentada.|1|  
|ConnectRetryInterval|Número inteiro entre 1 e 60 (inclusive)|O tempo, em segundos entre tentativas para reestabelecer uma conexão. O aplicativo tentará reconectar-se imediatamente ao detectar uma conexão interrompida e, em seguida, aguardará ConnectRetryInterval segundos antes de tentar novamente. Essa palavra-chave será ignorado se ConnectRetryCount for igual a 0.|1|  
|banco de dados|Cadeia de caracteres|Especifica o nome do banco de dados em uso para a conexão que está sendo estabelecida<sup>2</sup>.|O banco de dados padrão para o logon que está sendo usado.|  
|Driver|Cadeia de caracteres|Especifica o driver ODBC da Microsoft usado para se comunicar com o SQL Server.<br /><br />Os valores possíveis são:<br />ODBC Driver 17 for SQL Server<br />ODBC Driver 13 for SQL Server<br />ODBC Driver 11 para SQL Server (somente Windows).|Quando a palavra-chave Driver não for especificada, o Microsoft Drivers for PHP para SQL Server tenta encontrar drivers de ODBC da Microsoft com suporte no sistema, começando com a versão mais recente do ODBC e assim por diante.|  
|Encrypt|1 ou **true** para criptografia ativada.<br /><br />0 ou **false** para criptografia desativada.|Especifica se a comunicação com o SQL Server é criptografada (1 ou **true**) ou não criptografada (0 ou **false**)<sup>3</sup>.|**false** (0)|  
|Failover_Partner|Cadeia de caracteres|Especifica o servidor e a instância do espelho do banco de dados (se habilitado e configurado) a serem usados quando o servidor primário não está disponível.<br /><br />Há restrições ao uso de Failover_Partner com MultiSubnetFailover. Para obter mais informações, consulte [suporte para alta disponibilidade, recuperação de desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|Nenhum valor definido.|  
|keyStoreAuthentication|**KeyVaultPassword**<br /><br />**KeyVaultClientSecret**|Método de autenticação para acessar o Cofre de chaves do Azure. Controla quais tipos de credenciais são usadas com KeyStorePrincipalId e KeyStoreSecret. Para obter mais informações, consulte [usando o Azure Key Vault](../../connect/php/using-always-encrypted-php-drivers.md###using-azure-key-vault).|Não definido.|
|KeyStorePrincipalId|Cadeia de caracteres|Identificador para a conta de busca acessar o Cofre de chaves do Azure. <br /><br />Se for KeyStoreAuthentication **KeyVaultPassword**, isso deve ser um nome de usuário do Active Directory do Azure. <br /><br />Se for KeyStoreAuthentication **KeyVaultClientSecret**, isso deve ser uma ID de cliente do aplicativo.|Não definido.|
|keyStoreSecret|Cadeia de caracteres|Segredo da credencial para a conta de busca acessar o Cofre de chaves do Azure. <br /><br />Se for KeyStoreAuthentication **KeyVaultPassword**, isso deve ser uma senha do Active Directory do Azure. <br /><br />Se for KeyStoreAuthentication **KeyVaultClientSecret**, isso deve ser um segredo de cliente do aplicativo.|Não definido.|
|LoginTimeout|Inteiro (driver SQLSRV)<br /><br />Cadeia de caracteres (driver PDO_SQLSRV)|Especifica o número de segundos a aguardar antes de a tentativa de conexão falhar.|Sem tempo limite.|  
|MultipleActiveResultSets|1 ou **true** para usar vários conjuntos de resultados ativos.<br /><br />0 ou **false** para desabilitar vários conjuntos de resultados ativos.|Desabilita ou habilita explicitamente o suporte para vários conjuntos de resultados ativos (MARS).<br /><br />Para obter mais informações, confira [Como desabilitar o MARS &#40;conjunto de resultados ativos múltiplos &#41;](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md).|true (1)|  
|MultiSubnetFailover|Cadeia de caracteres|Sempre especifique **multiSubnetFailover=yes** ao se conectar ao ouvinte do grupo de disponibilidade do [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] ou a uma Instância do Cluster de Failover do [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]. **multiSubnetFailover=yes** configura o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] para fornecer mais rapidez na detecção do servidor ativo (atualmente) e na conexão a ele. Os valores possíveis são Sim e Não.<br /><br />Para obter mais informações sobre [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] suporte para [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], consulte [dão suporte para alta disponibilidade, recuperação de desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|não|  
|PWD<br /><br />(sem suporte no driver PDO_SQLSRV)|Cadeia de caracteres|Especifica a senha associada à ID de Usuário a ser usada ao se conectar com a Autenticação do SQL Server<sup>4</sup>.|Nenhum valor definido.|  
|QuotedId|1 ou **true** para usar as regras do SQL-92.<br /><br />0 ou **false** para usar regras herdadas.|Especifica se devem ser usadas as regras do SQL-92 para identificadores entre aspas (1 ou **true**) ou as regras herdadas do Transact-SQL (0 ou **false**).|**true** (1)|  
|ReturnDatesAsStrings<br /><br />(sem suporte no driver PDO_SQLSRV)|1 ou **true** para retornar tipos de data e hora como cadeias de caracteres.<br /><br />0 ou **false** para retornar tipos de data e hora como tipos **DateTime** do PHP.|Recupera os tipos de data e hora (datetime, date, time, datetime2 e datetimeoffset) como cadeias de caracteres ou como tipos do PHP. Ao usar o driver PDO_SQLSRV, as datas são retornadas como cadeias de caracteres. O driver PDO_SQLSRV não tem nenhum tipo **datetime**.<br /><br />Para obter mais informações, consulte [Como recuperar um tipo de data e hora como cadeias de caracteres usando o driver SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md).|**false**|  
|Rolável|Cadeia de caracteres|"Em buffer" indica que você quer um cursor do lado do cliente (em buffer), que permite armazenar em cache um conjunto de resultados inteiro na memória. Para obter mais informações, confira [Tipos de cursor &#40;Driver SQLSRV&#41;](../../connect/php/cursor-types-sqlsrv-driver.md).|Cursor somente de avanço|  
|Servidor<br /><br />(sem suporte no driver SQLSRV)|Cadeia de caracteres|A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] à qual se conectar.<br /><br />Você também pode especificar um nome de rede virtual, para se conectar a um grupo de disponibilidade AlwaysOn. Para obter mais informações sobre [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] suporte para [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], consulte [dão suporte para alta disponibilidade, recuperação de desastres](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|Servidor é uma palavra-chave necessária (embora não precise ser a primeira palavra-chave na cadeia de conexão). Se o nome do servidor não for passado para a palavra-chave, será feita uma tentativa para se conectar à instância local.<br /><br />O valor passado para o servidor pode ser o nome de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou o endereço IP da instância. Opcionalmente, você pode especificar um número da porta (por exemplo, `sqlsrv:server=(local),1033`).<br /><br />A partir da versão 3.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] , você também pode especificar uma instância LocalDB com `server=(localdb)\instancename`. Para obter mais informações, consulte [suporte para o LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).|  
|TraceFile|Cadeia de caracteres|Especifica o caminho do arquivo usado para dados de rastreamento.|Nenhum valor definido.|  
|TraceOn|1 ou **true** para habilitar o rastreamento.<br /><br />0 ou **false** para desabilitar o rastreamento.|Especifica se o rastreamento ODBC está habilitado (1 ou **true**) ou desabilitado (0 ou **false**) para a conexão que está sendo estabelecida.|**false** (0)|  
|TransactionIsolation|O driver SQLSRV usa os seguintes valores:<br /><br />SQLSRV_TXN_READ_UNCOMMITTED<br /><br />SQLSRV_TXN_READ_COMMITTED<br /><br />SQLSRV_TXN_REPEATABLE_READ<br /><br />SQLSRV_TXN_SNAPSHOT<br /><br />SQLSRV_TXN_SERIALIZABLE<br /><br />O driver PDO_SQLSRV usa os seguintes valores:<br /><br />PDO::SQLSRV_TXN_READ_UNCOMMITTED<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED<br /><br />PDO::SQLSRV_TXN_REPEATABLE_READ<br /><br />PDO::SQLSRV_TXN_SNAPSHOT<br /><br />PDO::SQLSRV_TXN_SERIALIZABLE|Especifica o nível de isolamento da transação.<br /><br />Para obter mais informações sobre o isolamento da transação, confira [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md) na documentação do SQL Server.|SQLSRV_TXN_READ_COMMITTED<br /><br />ou em<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED|  
|transparentNetworkIPResolution|**Habilitado** ou **Desabilitado**|Afeta a sequência de conexão quando a primeira resolvida IP do nome do host não responde e há vários IPs associados com o nome do host.<br /><br />Ele interage com MultiSubnetFailover para fornecer sequências de conexão diferentes. Para obter mais informações, consulte [resolução de IP de rede transparente](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) ou [usando resolução de IP de rede transparente](https://docs.microsoft.com/sql/connect/odbc/using-transparent-network-ip-resolution).|Habilitado|
|TrustServerCertificate|1 ou **true** para confiar no certificado.<br /><br />0 ou **false** para não confiar no certificado.|Especifica se o cliente deve confiar em um certificado do servidor autoassinado (1 ou **true**) ou rejeitá-lo (0 ou **false**).|**false** (0)|  
|UID<br /><br />(sem suporte no driver PDO_SQLSRV)|Cadeia de caracteres|Especifica a ID de Usuário a ser usada ao se conectar com a Autenticação do SQL Server<sup>4</sup>.|Nenhum valor definido.|  
|WSID|Cadeia de caracteres|Especifica o nome do computador para rastreamento.|Nenhum valor definido.|  

1. O `ConnectionPooling` atributo não pode ser usado para habilitar/desabilitar o pooling de conexão no Linux e Mac. Confira [Pooling de conexões (Microsoft Drivers for PHP for SQL Server)](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md).

2. Todas as consultas executadas na conexão estabelecida são feitas no banco de dados especificado pelo atributo *Database*. No entanto, caso o usuário tenha as permissões apropriadas, os dados em outros bancos de dados poderão ser acessados usando um nome totalmente qualificado. Por exemplo, se o banco de dados *mestre* for definido com o atributo de conexão *Database*, ainda será possível executar uma consulta Transact-SQL que acessa a tabela *AdventureWorks.HumanResources.Employee* usando o nome totalmente qualificado.  

3. A habilitação de *Encryption* pode afetar o desempenho de alguns aplicativos devido à sobrecarga de computação necessária para criptografar os dados.  

4. A instância do *UID* e *PWD* devem ser definidos ao se conectar com a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  

Muitas das chaves com suporte são atributos de cadeias de conexão do ODBC. Para obter informações sobre cadeias de conexão do ODBC, confira [Usando palavras-chave da cadeia de conexão com o SQL Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).

## <a name="see-also"></a>Consulte Também  
[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)  
