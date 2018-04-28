---
title: Usando palavras-chave de cadeia de caracteres de Conexão com o Driver do OLE DB para SQL Server | Microsoft Docs
description: Usando palavras-chave de cadeia de caracteres de conexão com o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], connection string keywords
- MSOLEDBSQL, connection string keywords
- connection strings [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, connection string keywords
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Active
ms.openlocfilehash: f4ac4a2231ea983e93c9c418bdd309cf45ed6cc2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="using-connection-string-keywords-with-ole-db-driver-for-sql-server"></a>Usando palavras-chave de cadeia de caracteres de Conexão com o Driver do OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Alguns Driver OLE DB para SQL Server APIs usam cadeias de caracteres de conexão para especificar atributos de conexão. Cadeias de conexão são listas de palavras-chave e valores associados; cada palavra-chave identifica um atributo de conexão específico.  
  
> **Observação:** OLE DB Driver para SQL Server permite ambiguidade em cadeias de caracteres de conexão para manter a compatibilidade com versões anteriores (por exemplo, algumas palavras-chave pode ser especificado mais de uma vez e conflitantes, permitidas tendo a resolução baseada na posição ou precedência). Versões futuras do OLE DB Driver for SQL Server talvez não permitam ambiguidade em cadeias de caracteres de conexão. É uma boa prática ao modificar aplicativos para usar o OLE DB Driver para SQL Server para eliminar qualquer dependência em ambiguidade da cadeia de caracteres de conexão.  
  
 As seções a seguir descrevem as palavras-chave que podem ser usadas com o Driver OLE DB para SQL Server e ActiveX Data Objects (ADO) ao usar o Driver do OLE DB para SQL Server como o provedor de dados.  

  
## <a name="ole-db-driver-connection-string-keywords"></a>Palavras-chave do OLE DB Driver Conexão cadeia de caracteres  
 Os aplicativos OLE DB podem inicializar objetos de fonte de dados de duas formas:  
  
-   **IDBInitialize:: Initialize**  
  
-   **IDataInitialize:: Getdatasource**  
  
 No primeiro caso, uma cadeia de caracteres do provedor pode ser usada para inicializar as propriedades da conexão, definindo a propriedade DBPROP_INIT_PROVIDERSTRING no conjunto de propriedades DBPROPSET_DBINIT. No segundo caso, uma cadeia de caracteres de inicialização pode ser passada para **IDataInitialize:: Getdatasource** método para inicializar as propriedades da conexão. Ambos os métodos inicializam as mesmas propriedades de conexão OLE DB, embora sejam usados conjuntos diferentes de palavras-chave. O conjunto de palavras-chave usadas por **IDataInitialize:: Getdatasource** é, no mínimo, a descrição das propriedades do grupo de propriedade de inicialização.  
  
 Qualquer configuração da cadeia de caracteres do provedor tem uma propriedade OLE DB correspondente definida com um valor padrão ou explicitamente definida com um valor; o valor de propriedade OLE DB substituirá a configuração na cadeia de caracteres do provedor.  
  
 As propriedades boolianas definidas nas cadeias de caracteres do provedor por meio dos valores DBPROP_INIT_PROVIDERSTRING são definidas usando os valores "sim" e "não". Propriedades Boolianas definidas nas cadeias de caracteres de inicialização usando **IDataInitialize:: Getdatasource** são definidas usando os valores "true" e "false".  
  
 Aplicativos que usam **IDataInitialize:: Getdatasource** também pode usar as palavras-chave usadas por **IDBInitialize:: Initialize** , mas apenas para propriedades que não têm um valor padrão. Se um aplicativo usa o **IDataInitialize:: Getdatasource** palavra-chave e o **IDBInitialize:: Initialize** palavra-chave na cadeia de inicialização, o **IDataInitialize:: Getdatasource** configuração de palavra-chave é usada. É altamente recomendável que os aplicativos não usam **IDBInitialize:: Initialize** palavras-chave em **IDataInitialize: Getdatasource** cadeias de conexão, como esse comportamento pode não ser mantido em versões futuras.  
  
> [!NOTE]  
>  Uma cadeia de caracteres de conexão passado **IDataInitialize:: Getdatasource** é convertida em propriedades e aplicada por meio de **idbproperties:: SetProperties**. Se os serviços de componente encontraram a descrição de propriedade **idbproperties:: Getpropertyinfo**, essa propriedade será aplicada como uma propriedade autônoma. Caso contrário, ela será aplicada por meio da propriedade DBPROP_PROVIDERSTRING. Por exemplo, se você especificar a cadeia de caracteres de conexão **Data Source = server1; Server = server2**, **fonte de dados** será definida como uma propriedade, mas **Server** entrará em uma cadeia de caracteres do provedor.  
  
 Se você especificar várias instâncias da mesma propriedade específica de provedor, o primeiro valor da primeira propriedade será usado.  
  
 Cadeias de caracteres de Conexão usadas por aplicativos OLE DB usando DBPROP_INIT_PROVIDERSTRING com **IDBInitialize:: Initialize** têm a seguinte sintaxe:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Os valores de atributo podem ser colocados entre chaves, sendo uma boa prática fazer isso. Isso evita problemas quando os valores de atributo contêm caracteres não alfanuméricos. Como a primeira chave de fechamento é usada para encerrar o valor, os valores não podem conter caracteres de chave de fechamento.  
  
 Um caractere de espaço após o sinal de igual (=) de uma palavra-chave de cadeia de conexão será interpretado como um literal, mesmo que o valor seja colocado entre aspas.  
  
 A tabela a seguir descreve as palavras-chave que podem ser usadas com DBPROP_INIT_PROVIDERSTRING.  
  
|Palavra-chave|Propriedade de inicialização|Description|  
|-------------|-----------------------------|-----------------|  
|**Endereço**|SSPROP_INIT_NETWORKADDRESS|Sinônimo de "Endereço".|  
|**Endereço**|SSPROP_INIT_NETWORKADDRESS|O endereço de rede do servidor executando uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **Endereço** geralmente é o nome de rede do servidor, mas pode ter outros nomes como um pipe, um endereço IP ou um endereço de porta e para o soquete de TCP/IP.<br /><br /> Se você especificar um endereço IP, verifique se os protocolos de pipes nomeados ou TCP/IP estão habilitados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> O valor de **endereço** tem precedência sobre o valor passado para **Server** em cadeias de caracteres de conexão ao usar o Driver do OLE DB para SQL Server. Observe também que `Address=;` se conectará ao servidor especificado no **servidor** palavra-chave, enquanto `Address= ;, Address=.;`, `Address=localhost;`, e `Address=(local);` all fazer com que uma conexão ao servidor local.<br /><br /> A sintaxe completa para o **endereço** palavra-chave é o seguinte:<br /><br /> [*protocolo ***:**]* endereço *[* *, * * * porta &#124;\pipe\pipename*]<br /><br /> O*protocolo* pode ser **tcp** (TCP/IP), **lpc** (memória compartilhada) ou **np** (pipes nomeados). Para obter mais informações sobre protocolos, consulte [configurar protocolos de cliente](../../../database-engine/configure-windows/configure-client-protocols.md).<br /><br /> Se nem *protocolo* nem o **rede** palavra-chave for especificado, o OLE DB Driver para SQL Server usará a ordem de protocolo especificada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do Configuration Manager.<br /><br /> *porta* é a porta para se conectar ao servidor especificado. Por padrão, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa a porta 1433.|   
|**APP**|SSPROP_INIT_APPNAME|A cadeia de caracteres que identifica o aplicativo.|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. Os valores possíveis são **ReadOnly** e **ReadWrite**.<br /><br /> O padrão é **ReadWrite**. Para obter mais informações sobre o Driver do OLE DB para o suporte do SQL Server para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [OLE DB Driver para SQL Server oferecem suporte para alta disponibilidade, recuperação de desastres](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|O nome do arquivo primário (com o nome do caminho completo incluído) de um banco de dados anexável. Para usar **AttachDBFileName**, você também deve especificar o nome do banco de dados com a palavra-chave do provedor cadeia banco de dados. Caso o banco de dados já tenha sido anexado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não o anexa novamente (ele usa o banco de dados anexado como sendo o padrão da conexão).|  
|**Tradução automática**|SSPROP_INIT_AUTOTRANSLATE|Sinônimo de "Tradução automática".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura a conversão de caracteres OEM/ANSI. Os valores reconhecidos são "sim" e "não".|  
|**Banco de dados**|DBPROP_INIT_CATALOG|Nome do banco de dados.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica o modo de manipulação do tipo de dados a ser usado. Os valores reconhecidos são "0" para tipos de dados do provedor e "80" para tipos de dados do SQL Server 2000.|  
|**Encrypt**|SSPROP_INIT_ENCRYPT|Especifica se os dados devem ser criptografados antes de serem enviados pela rede. Os valores possíveis são "sim" e "não". O valor padrão é "não".|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|O nome do servidor de failover usado no espelhamento de banco de dados.|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|O SPN do parceiro de failover. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o OLE DB Driver para SQL Server usar o padrão, o SPN gerado pelo provedor.|  
|**Idioma**|SSPROPT_INIT_CURRENTLANGUAGE|O idioma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|Habilita ou desabilita MARS na conexão caso o servidor seja [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior. Os valores possíveis são "sim" e "não". O valor padrão é "não".|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|Sempre especifique **MultiSubnetFailover = Yes** ao se conectar ao ouvinte do grupo de disponibilidade de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o grupo de disponibilidade ou uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância de Cluster de Failover. **MultiSubnetFailover = Yes** configura OLE DB Driver para SQL Server fornecer detecção mais rápida e conexão ao servidor ativo (atualmente). Os valores possíveis são **Sim** e **Não**. O padrão é **não**. Por exemplo:<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> Para obter mais informações sobre o Driver do OLE DB para o suporte do SQL Server para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [OLE DB Driver para SQL Server oferecem suporte para alta disponibilidade, recuperação de desastres](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**NET**|SSPROP_INIT_NETWORKLIBRARY|Sinônimo de "Rede".|  
|**Rede**|SSPROP_INIT_NETWORKLIBRARY|A biblioteca de rede usada para estabelecer uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.|  
|**Biblioteca de rede**|SSPROP_INIT_NETWORKLIBRARY|Sinônimo de "Rede".|  
|**Tamanho do pacote**|SSPROP_INIT_PACKETSIZE|Tamanho do pacote de rede. O padrão é 4096.|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Aceita as cadeias de caracteres "sim" e "não" como valores. Em caso de "não", o objeto de fonte de dados não tem permissão para manter informações confidenciais de autenticação|  
|**PWD**|DBPROP_AUTH_PASSWORD|A senha de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Servidor**|DBPROP_INIT_DATASOURCE|O nome de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O valor deve ser o nome de um servidor na rede, um endereço IP ou o nome de um alias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> Quando não especificado, uma conexão é estabelecida com a instância padrão no computador local.<br /><br /> O **endereço** palavra-chave substitui o **Server** palavra-chave.<br /><br /> Você pode se conectar à instância padrão no servidor local, especificando um destes procedimentos:<br /><br /> **Server=;**<br /><br /> **Server=.;**<br /><br /> **Server=(local);**<br /><br /> **Server=(local);**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(localdb)\\** *instancename* **;**<br /><br /> Para obter mais informações sobre o suporte de LocalDB, consulte [OLE DB Driver para SQL Server oferecem suporte para o LocalDB](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md).<br /><br /> Para especificar uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], acrescente  **\\ ***InstanceName *.<br /><br /> Quando nenhum servidor for especificado, uma conexão é estabelecida com a instância padrão no computador local.<br /><br /> Se você especificar um endereço IP, certifique-se de que o TCP/IP ou pipes nomeados estão habilitados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do Configuration Manager.<br /><br /> A sintaxe completa para o **servidor** palavra-chave é o seguinte:<br /> <br /> **Server =**[* protocolo***:**] *Servidor*[**, * * * porta*]<br /><br /> O*protocolo* pode ser **tcp** (TCP/IP), **lpc** (memória compartilhada) ou **np** (pipes nomeados).<br /><br /> O seguinte é um exemplo de como especificar um pipe nomeado:<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> Esta linha especifica o protocolo de pipe nomeado, um pipe nomeado na máquina local (`\\.\pipe`), o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (`MSSQL$MYINST01`) e o nome padrão do pipe nomeado (`sql/query`).<br /><br /> Se nem um *protocolo* nem o **rede** palavra-chave for especificado, o OLE DB Driver para SQL Server usará a ordem de protocolo especificada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do Configuration Manager.<br /><br /> *porta* é a porta para se conectar ao servidor especificado. Por padrão, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa a porta 1433.<br /><br /> Os espaços são ignorados no início do valor passado para **Server** em cadeias de caracteres de conexão ao usar o Driver do OLE DB para SQL Server.|   
|**ServerSPN**|SSPROP_INIT_SERVERSPN|O SPN do servidor. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o OLE DB Driver para SQL Server usar o padrão, o SPN gerado pelo provedor.|  
|**Tempo Limite**|DBPROP_INIT_TIMEOUT|O tempo (em segundos) para aguardar a conclusão da inicialização da fonte de dados.|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|Quando "Sim", instrui o Driver OLE DB para SQL Server para usar o modo de autenticação do Windows para validação do logon. Caso contrário, instrui o Driver OLE DB para SQL Server para usar um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nome de usuário e senha para validação de logon e as palavras-chave UID e PWD devem ser especificados.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Aceita as cadeias de caracteres "sim" e "não" como valores. O valor padrão é "não", o que significa que o certificado do servidor será validado.|  
|**UID**|DBPROP_AUTH_USERID|O nome de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|Esta palavra-chave é preterida e sua configuração é ignorada pelo Driver OLE DB para SQL Server.|  
|**WSID**|SSPROP_INIT_WSID|O identificador da estação de trabalho.|  
  
 Cadeias de caracteres de Conexão usadas por aplicativos OLE DB usam **IDataInitialize:: Getdatasource** têm a seguinte sintaxe:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 O uso de propriedades deve estar em conformidade com a sintaxe permitida em seu escopo.  Por exemplo, **WSID** usa chaves (**{}**) caracteres de aspas simples e **nome do aplicativo** usa (**'**) ou duplas (**"**) caracteres de aspas simples. Apenas propriedades de cadeia de caracteres podem ser colocadas entre aspas. A tentativa de colocar um número inteiro ou propriedade enumerada entre aspas resultará no erro: "A Cadeia de Conexão não está de acordo com a especificação OLE DB".  
  
 Opcionalmente, os valores de atributos podem ser colocados entre aspas simples ou duplas, o que é uma boa prática. Isso evita problemas quando os valores contêm caracteres não alfanuméricos. O caractere de aspas usado também pode ser exibido em valores, desde que seja dobrado.  
  
 Um caractere de espaço após o sinal de igual (=) de uma palavra-chave de cadeia de conexão será interpretado como um literal, mesmo que o valor seja colocado entre aspas.  
  
 Se uma cadeia de conexão tiver mais de uma das propriedades listadas na tabela a seguir, o valor da última propriedade será usado.  
  
 A tabela a seguir descreve as palavras-chave que podem ser usadas com **IDataInitialize:: Getdatasource**:  
  
|Palavra-chave|Propriedade de inicialização|Description|  
|-------------|-----------------------------|-----------------|  
|**Nome do Aplicativo**|SSPROP_INIT_APPNAME|A cadeia de caracteres que identifica o aplicativo.|  
|**Tentativa de aplicativo**|SSPROP_INIT_APPLICATIONINTENT|Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. Os valores possíveis são **ReadOnly** e **ReadWrite**.<br /><br /> O padrão é **ReadWrite**. Para obter mais informações sobre o Driver do OLE DB para o suporte do SQL Server para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [OLE DB Driver para SQL Server oferecem suporte para alta disponibilidade, recuperação de desastres](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Tradução automática**|SSPROP_INIT_AUTOTRANSLATE|Sinônimo de "Tradução automática".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura a conversão de caracteres OEM/ANSI. Os valores reconhecidos são "verdadeiro" e "falso".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|O tempo (em segundos) para aguardar a conclusão da inicialização da fonte de dados.|  
|**Idioma atual**|SSPROPT_INIT_CURRENTLANGUAGE|O nome do idioma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Fonte de dados**|DBPROP_INIT_DATASOURCE|O nome de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.<br /><br /> Quando não especificado, uma conexão é estabelecida com a instância padrão no computador local.<br /><br /> Para obter mais informações sobre sintaxe de endereço válida, consulte a descrição do **Server** palavra-chave, neste tópico.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica o modo de manipulação do tipo de dados a ser usado. Os valores reconhecidos são "0" para tipos de dados de provedor e "80" para tipos de dados do [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)].|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|O nome do servidor de failover usado no espelhamento de banco de dados.|  
|**SPN do parceiro de failover**|SSPROP_INIT_FAILOVERPARTNERSPN|O SPN do parceiro de failover. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o OLE DB Driver para SQL Server usar o padrão, o SPN gerado pelo provedor.|  
|**Catálogo Inicial**|DBPROP_INIT_CATALOG|Nome do banco de dados.|  
|**Nome do arquivo**|SSPROP_INIT_FILENAME|O nome do arquivo primário (com o nome do caminho completo incluído) de um banco de dados anexável. Para usar **AttachDBFileName**, você também deve especificar o nome do banco de dados com a palavra-chave do provedor cadeia banco de dados. Caso o banco de dados já tenha sido anexado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não o anexa novamente (ele usa o banco de dados anexado como sendo o padrão da conexão).|  
|**Segurança Integrada**|DBPROP_AUTH_INTEGRATED|Aceita o valor o "SSPI" para a Autenticação do Windows.|  
|**Conexão do MARS**|SSPROP_INIT_MARSCONNECTION|Habilita ou desabilita MARS (Multiple Active Result Sets) na conexão. Os valores reconhecidos são "verdadeiro" e "falso". O padrão é "falso".|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|Sempre especifique **MultiSubnetFailover = True** ao se conectar ao ouvinte do grupo de disponibilidade de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o grupo de disponibilidade ou uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância de Cluster de Failover. **MultiSubnetFailover = True** configura OLE DB Driver para SQL Server fornecer detecção mais rápida e conexão ao servidor ativo (atualmente). Os valores possíveis são **True** e **False**. O padrão é **False**. Por exemplo:<br /><br /> `MultiSubnetFailover=True`<br /><br /> Para obter mais informações sobre o Driver do OLE DB para o suporte do SQL Server para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [OLE DB Driver para SQL Server oferecem suporte para alta disponibilidade, recuperação de desastres](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Endereço de rede**|SSPROP_INIT_NETWORKADDRESS|O endereço de rede de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.<br /><br /> Para obter mais informações sobre sintaxe de endereço válida, consulte a descrição do **endereço** palavra-chave, neste tópico.|  
|**Biblioteca de rede**|SSPROP_INIT_NETWORKLIBRARY|A biblioteca de rede usada para estabelecer uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Tamanho do pacote de rede. O padrão é 4096.|  
|**Senha**|DBPROP_AUTH_PASSWORD|A senha de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Informações de Persistência de Segurança**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Aceita as cadeias de caracteres "verdadeiro" e "falso" como valores. Em caso de "falso", o objeto de fonte de dados não tem permissão para manter informações confidenciais de autenticação|  
|**Provedor**||Para OLE DB Driver para SQL Server, isso deve ser "MSOLEDBSQL".|  
|**SPN do servidor**|SSPROP_INIT_SERVERSPN|O SPN do servidor. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o OLE DB Driver para SQL Server usar o padrão, o SPN gerado pelo provedor.|  
|**Confiar em Certificado do Servidor**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Aceita as cadeias de caracteres "verdadeiro" e "falso" como valores. O valor padrão é "falso", o que significa que o certificado do servidor será validado.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|Especifica se os dados devem ser criptografados antes de serem enviados pela rede. Os valores possíveis são "verdadeiro" e "falso". O valor padrão é "falso".|  
|**ID de usuário**|DBPROP_AUTH_USERID|O nome de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**ID de estação de trabalho**|SSPROP_INIT_WSID|O identificador da estação de trabalho.|  
  
 **Observação** na cadeia de conexão, a propriedade "Old Password" define SSPROP_AUTH_OLD_PASSWORD, que é a senha atual (provavelmente expirada) que não está disponível por meio de uma propriedade de cadeia de caracteres do provedor.  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>Palavras-chave da cadeia de conexão do ADO (ActiveX Data Objects)  
 Aplicativos ADO definem a **ConnectionString** propriedade de **ADODBConnection** objetos ou fornecer uma cadeia de caracteres de conexão como um parâmetro para o **abrir** método **ADODBConnection** objetos.  
  
 Aplicativos ADO também podem usar as palavras-chave usadas pelo OLE DB **IDBInitialize:: Initialize** método, mas apenas para propriedades que não têm um valor padrão. Se um aplicativo usa ambos as ADO palavras-chave e o **IDBInitialize:: Initialize** palavras-chave na cadeia de inicialização, a palavra-chave do ADO configuração serão usadas. É altamente recomendável que os aplicativos só usem palavras-chave da cadeia de conexão do ADO.  
  
 As cadeias de conexão usadas pelo ADO têm a seguinte sintaxe:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=["]attribute-value["]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Os valores de atributo podem ser colocados entre aspas duplas, sendo uma boa prática fazer isso. Isso evita problemas quando os valores contêm caracteres não alfanuméricos. Os valores de atributo não podem conter aspas duplas.  
  
 A seguinte tabela descreve as palavras-chave que podem ser usadas com uma cadeia de conexão do ADO:  
  
|Palavra-chave|Propriedade de inicialização|Description|  
|-------------|-----------------------------|-----------------|  
|**Tentativa de aplicativo**|SSPROP_INIT_APPLICATIONINTENT|Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. Os valores possíveis são **ReadOnly** e **ReadWrite**.<br /><br /> O padrão é **ReadWrite**. Para obter mais informações sobre o Driver do OLE DB para o suporte do SQL Server para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [OLE DB Driver para SQL Server oferecem suporte para alta disponibilidade, recuperação de desastres](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Nome do Aplicativo**|SSPROP_INIT_APPNAME|A cadeia de caracteres que identifica o aplicativo.|  
|**Tradução automática**|SSPROP_INIT_AUTOTRANSLATE|Sinônimo de "Tradução automática".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura a conversão de caracteres OEM/ANSI. Os valores reconhecidos são "verdadeiro" e "falso".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|O tempo (em segundos) para aguardar a conclusão da inicialização da fonte de dados.|  
|**Idioma atual**|SSPROPT_INIT_CURRENTLANGUAGE|O nome do idioma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Fonte de dados**|DBPROP_INIT_DATASOURCE|O nome de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.<br /><br /> Quando não especificado, uma conexão é estabelecida com a instância padrão no computador local.<br /><br /> Para obter mais informações sobre sintaxe de endereço válida, consulte a descrição do **Server** palavra-chave, neste tópico.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica o modo de manuseio do tipo de dados a ser usado. Os valores reconhecidos são "0" para tipos de dados do provedor e "80" para tipos de dados do SQL Server 2000.|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|O nome do servidor de failover usado no espelhamento de banco de dados.|  
|**SPN do parceiro de failover**|SSPROP_INIT_FAILOVERPARTNERSPN|O SPN do parceiro de failover. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o OLE DB Driver para SQL Server usar o padrão, o SPN gerado pelo provedor.|  
|**Catálogo Inicial**|DBPROP_INIT_CATALOG|Nome do banco de dados.|  
|**Nome do arquivo**|SSPROP_INIT_FILENAME|O nome do arquivo primário (com o nome do caminho completo incluído) de um banco de dados anexável. Para usar **AttachDBFileName**, você também deve especificar o nome do banco de dados com a palavra-chave do provedor cadeia banco de dados. Caso o banco de dados já tenha sido anexado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não o anexa novamente (ele usa o banco de dados anexado como sendo o padrão da conexão).|  
|**Segurança Integrada**|DBPROP_AUTH_INTEGRATED|Aceita o valor o "SSPI" para a Autenticação do Windows.|  
|**Conexão do MARS**|SSPROP_INIT_MARSCONNECTION|Habilita ou desabilita MARS na conexão caso o servidor seja [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior. Os valores reconhecidos são "verdadeiro" e "falso".O padrão é "falso".|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|Sempre especifique **MultiSubnetFailover = True** ao se conectar ao ouvinte do grupo de disponibilidade de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o grupo de disponibilidade ou uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância de Cluster de Failover. **MultiSubnetFailover = True** configura OLE DB Driver para SQL Server fornecer detecção mais rápida e conexão ao servidor ativo (atualmente). Os valores possíveis são **True** e **False**. O padrão é **False**. Por exemplo:<br /><br /> `MultiSubnetFailover=True`<br /><br /> Para obter mais informações sobre o Driver do OLE DB para o suporte do SQL Server para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [OLE DB Driver para SQL Server oferecem suporte para alta disponibilidade, recuperação de desastres](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Endereço de rede**|SSPROP_INIT_NETWORKADDRESS|O endereço de rede de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.<br /><br /> Para obter mais informações sobre sintaxe de endereço válida, consulte a descrição do **endereço** palavra-chave, neste tópico.|  
|**Biblioteca de rede**|SSPROP_INIT_NETWORKLIBRARY|A biblioteca de rede usada para estabelecer uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na organização.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Tamanho do pacote de rede. O padrão é 4096.|  
|**Senha**|DBPROP_AUTH_PASSWORD|A senha de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Informações de Persistência de Segurança**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Aceita as cadeias de caracteres "verdadeiro" e "falso" como valores. Quando "falso", o objeto de fonte de dados não tem permissão para manter informações confidenciais de autenticação.|  
|**Provedor**||Para OLE DB Driver para SQL Server, isso deve ser "MSOLEDBSQL".|  
|**SPN do servidor**|SSPROP_INIT_SERVERSPN|O SPN do servidor. O valor padrão é uma cadeia de caracteres vazia. Uma cadeia de caracteres vazia faz com que o OLE DB Driver para SQL Server usar o padrão, o SPN gerado pelo provedor.|  
|**Confiar em Certificado do Servidor**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Aceita as cadeias de caracteres "verdadeiro" e "falso" como valores. O valor padrão é "falso", o que significa que o certificado do servidor será validado.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|Especifica se os dados devem ser criptografados antes de serem enviados pela rede. Os valores possíveis são "verdadeiro" e "falso". O valor padrão é "falso".|  
|**ID de usuário**|DBPROP_AUTH_USERID|O nome de logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**ID de estação de trabalho**|SSPROP_INIT_WSID|O identificador da estação de trabalho.|  
  
 **Observação** na cadeia de conexão, a propriedade "Old Password" define SSPROP_AUTH_OLD_PASSWORD, que é a senha atual (provavelmente expirada) que não está disponível por meio de uma propriedade de cadeia de caracteres do provedor.  
  
## <a name="see-also"></a>Consulte também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
