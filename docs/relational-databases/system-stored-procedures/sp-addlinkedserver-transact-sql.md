---
title: sp_addlinkedserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addlinkedserver_TSQL
- sp_addlinkedserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlinkedserver
ms.assetid: fed3adb0-4c15-4a1a-8acd-1b184aff558f
caps.latest.revision: 70
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 54fc43ecec6c26435165c9c3491bfba2f1f675ea
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spaddlinkedserver-transact-sql"></a>sp_addlinkedserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um servidor vinculado. Um servidor vinculado permite acesso a consultas distribuídas e heterogêneas em fontes de dados OLE DB. Depois que um servidor vinculado é criado usando **sp_addlinkedserver**distribuído consultas podem ser executadas nesse servidor. Se o servidor vinculado estiver definido como uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], poderão ser executados procedimentos armazenados remotos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addlinkedserver [ @server= ] 'server' [ , [ @srvproduct= ] 'product_name' ]   
     [ , [ @provider= ] 'provider_name' ]  
     [ , [ @datasrc= ] 'data_source' ]   
     [ , [ @location= ] 'location' ]   
     [ , [ @provstr= ] 'provider_string' ]   
     [ , [ @catalog= ] 'catalog' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@server=** ] **'***server***'**  
 É o nome do servidor vinculado a ser criado. *server* é **sysname**, sem padrão.  
  
 [  **@srvproduct=** ] **'***product_name***'**  
 É o nome do produto da fonte de dados OLE DB a ser adicionado como um servidor vinculado. *product_name* é **nvarchar (** 128 **)**, com um padrão NULL. Se **do SQL Server**, *provider_name*, *data_source*, *local*, *provider_string*, e *catálogo* não precisa ser especificado.  
  
 [  **@provider=** ] **'***provider_name***'**  
 É o identificador programático exclusivo (PROGID) do provedor OLE DB que corresponde a essa fonte de dados. *provider_name* devem ser exclusivos para o provedor OLE DB especificado instalado no computador atual. *provider_name* é **nvarchar (** 128 **)**, com um padrão de NULL; no entanto, se *provider_name* é omitido, SQLNCLI será usado. (Use SQLNCLI, e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fará o redirecionamento para a última versão do provedor OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.) Espera-se que o provedor OLE DB seja registrado com o PROGID especificado fornecido no Registro.  
  
 [  **@datasrc=** ] **'***data_source***'**  
 É o nome da fonte de dados conforme interpretada pelo provedor OLE DB. *data_source* é **nvarchar (** 4000 **)**. *data_source* é passado como a propriedade DBPROP_INIT_DATASOURCE para inicializar o provedor OLE DB.  
  
 [  **@location=** ] **'***local***'**  
 É o local do banco de dados conforme interpretado pelo provedor OLE DB. *local* é **nvarchar (** 4000 **)**, com um padrão NULL. *local* é passado como a propriedade DBPROP_INIT_LOCATION para inicializar o provedor OLE DB.  
  
 [  **@provstr=** ] **'***provider_string***'**  
 É a cadeia de conexão específica ao provedor OLE DB que identifica uma fonte de dados exclusiva. *provider_string* é **nvarchar (** 4000 **)**, com um padrão NULL. *provstr* é passado para IDataInitialize ou definido como a propriedade DBPROP_INIT_PROVIDERSTRING para inicializar o provedor OLE DB.  
  
 Quando o servidor vinculado é criado em relação a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client, a instância pode ser especificada usando a palavra-chave SERVER como SERVER =*servername*\\*instancename*para especificar uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *servername* é o nome do computador no qual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução, e *instancename* é o nome da instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à qual o usuário será conectado.  
  
> [!NOTE]  
>  Para acessar um banco de dados espelho, uma cadeia de conexão deve conter o nome do banco de dados. Esse nome é necessário para habilitar tentativas de failover pelo provedor de acesso de dados. O banco de dados pode ser especificado no **@provstr** ou **@catalog** parâmetro. Opcionalmente, a cadeia de conexão também pode fornecer um nome de parceiro de failover.  
  
 [  **@catalog=** ] **'***catálogo***'**  
 É o catálogo a ser usado quando uma conexão for feita ao provedor OLE DB. *catálogo* é **sysname**, com um padrão NULL. *catálogo* é passado como a propriedade DBPROP_INIT_CATALOG para inicializar o provedor OLE DB. Quando o servidor vinculado for definido em relação a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o catálogo se referirá ao banco de dados padrão ao qual o servidor vinculado estará mapeado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma.  
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir mostra as formas que um servidor vinculado pode ser definido para que as fontes de dados possam ser acessadas através do OLE DB. Um servidor vinculado pode ser definido em mais de uma forma para uma fonte de dados em particular; pode haver mais de uma linha para um tipo de fonte de dados. Esta tabela também mostra o **sp_addlinkedserver** valores de parâmetro a ser usado para configurar o servidor vinculado.  
  
|Fonte de dados remota OLE DB.|Provedor OLE DB|product_name|provider_name|data_source|local|provider_string|catálogo|  
|-------------------------------|---------------------|-------------------|--------------------|------------------|--------------|----------------------|-------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Provedor OLE DB Native Client|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <sup>1</sup> (padrão)||||||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Provedor OLE DB Native Client||**SQLNCLI**|Nome de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (para instância padrão)|||Nome do banco de dados (opcional)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Provedor OLE DB Native Client||**SQLNCLI**|*servername*\\*instancename* (para instância específica)|||Nome do banco de dados (opcional)|  
|Oracle, versão 8 e posterior|Provedor Oracle para OLE DB|Any (qualquer)|**OraOLEDB**|Alias para o banco de dados de Oracle||||  
|Access/Jet|Microsoft OLE DB Provider for Jet|Any (qualquer)|**Microsoft.Jet.OLEDB.4.0**|Caminho completo de arquivo de banco de dados de Jet||||  
|Fonte de dados ODBC|Microsoft OLE DB Provider para ODBC|Any (qualquer)|**MSDASQL**|DSN do sistema da fonte de dados ODBC||||  
|Fonte de dados ODBC|[!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider para ODBC|Any (qualquer)|**MSDASQL**|||Cadeia de conexão ODBC||  
|Sistema de arquivos|[!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Indexing Service|Any (qualquer)|**MSIDXS**|Nome do catálogo do Indexing Service||||  
|Planilha do [!INCLUDE[msCoName](../../includes/msconame-md.md)]Excel|[!INCLUDE[msCoName](../../includes/msconame-md.md)]OLE DB Provider for Jet|Any (qualquer)|**Microsoft.Jet.OLEDB.4.0**|Caminho completo do arquivo de Excel||Excel 5.0||  
|Banco de dados IBM DB2|[!INCLUDE[msCoName](../../includes/msconame-md.md)]Provedor OLE DB para DB2|Any (qualquer)|**DB2OLEDB**|||Consulte [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for DB2 documentação.|Nome de catálogo do banco de dados DB2|  
  
 <sup>1</sup> essa maneira de configurar um servidor vinculado impõe o nome do servidor vinculado para ser o mesmo que o nome de rede da instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use *data_source* para especificar o servidor.  
  
 <sup>2</sup> "Qualquer" indica que o nome do produto pode ser qualquer coisa.  
  
 O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client é o provedor que é usado com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se nenhum nome de provedor for especificado ou se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é especificado como o nome do produto. Mesmo se você especificar o nome do provedor anterior, SQLOLEDB, será alterado para SQLNCLI quando for persistente para o catálogo.  
  
 O *data_source*, *local*, *provider_string*, e *catálogo* parâmetros identificam o banco de dados ou bancos de dados vinculados servidor aponta. Se qualquer um destes parâmetros for NULL, a propriedade de inicialização OLE DB correspondente não será definida.  
  
 Em um ambiente clusterizado, quando você especificar os nomes de arquivo para apontarem para fontes de dados OLE DB, use o nome UNC (Convenção Universal de nomenclatura) ou um drive compartilhado para especificar o local.  
  
 **sp_addlinkedserver** não pode ser executado em uma transação definida pelo usuário.  
  
> [!IMPORTANT]  
>  Quando um servidor vinculado é criado usando **sp_addlinkedserver**, um automapeamento padrão é adicionado para todos os logons locais. Para provedores não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os logos autenticados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem conseguir acesso ao provedor sob a conta de serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os administradores deveriam considerar o uso de `sp_droplinkedsrvlogin <linkedserver_name>, NULL` para remover o mapeamento global.  
  
## <a name="permissions"></a>Permissões  
 O `sp_addlinkedserver` instrução requer o `ALTER ANY LINKED SERVER` permissão. (O SSMS **novo servidor vinculado** caixa de diálogo é implementada de maneira que requer a participação no `sysadmin` função de servidor fixa.)  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-microsoft-sql-server-native-client-ole-db-provider"></a>A. Usando o provedor OLE DB do Microsoft SQL Server Native Client  
 O exemplo abaixo cria um servidor vinculado chamado `SEATTLESales`. O nome de produto é `SQL Server` e nenhum nome de provedor é usado.  
  
```  
USE master;  
GO  
EXEC sp_addlinkedserver   
   N'SEATTLESales',  
   N'SQL Server';  
GO  
```  
  
 O exemplo a seguir cria um servidor vinculado `S1_instance1` em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client.  
  
```  
EXEC sp_addlinkedserver     
   @server=N'S1_instance1',   
   @srvproduct=N'',  
   @provider=N'SQLNCLI',   
   @datasrc=N'S1\instance1';  
```  
  
### <a name="b-using-the-microsoft-ole-db-provider-for-microsoft-access"></a>B. Usando o Provedor Microsoft OLE DB para Microsoft Access  
 O provedor Microsoft.Jet.OLEDB.4.0 se conecta a bancos de dados Microsoft Access que usam o formato 2002-2003. O exemplo abaixo cria um servidor vinculado chamado `SEATTLE Mktg`.  
  
> [!NOTE]  
>  Este exemplo presume que [!INCLUDE[msCoName](../../includes/msconame-md.md)] acesso e o exemplo **Northwind** banco de dados estão instalados e que o **Northwind** banco de dados reside em c:\msoffice\access\samples.  
  
```  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Mktg',   
   @provider = N'Microsoft.Jet.OLEDB.4.0',   
   @srvproduct = N'OLE DB Provider for Jet',  
   @datasrc = N'C:\MSOffice\Access\Samples\Northwind.mdb';  
GO  
```  
  
 O provedor Microsoft.ACE.OLEDB.12.0 se conecta a bancos de dados Microsoft Access que usam o formato 2007. O exemplo abaixo cria um servidor vinculado chamado `SEATTLE Mktg`.  
  
> [!NOTE]  
>  Este exemplo presume que [!INCLUDE[msCoName](../../includes/msconame-md.md)] acesso e o exemplo **Northwind** banco de dados estão instalados e que o **Northwind** banco de dados reside em c:\msoffice\access\samples.  
  
```  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Mktg',   
   @provider = N'Microsoft.ACE.OLEDB.12.0',   
   @srvproduct = N'OLE DB Provider for ACE',  
   @datasrc = N'C:\MSOffice\Access\Samples\Northwind.accdb';  
GO  
```  
  
### <a name="c-using-the-microsoft-ole-db-provider-for-odbc-with-the-datasource-parameter"></a>C. Usando o Microsoft OLE DB Provider para ODBC com o parâmetro data_source  
 O exemplo a seguir cria um servidor vinculado chamado `SEATTLE Payroll` que usa o [!INCLUDE[msCoName](../../includes/msconame-md.md)] provedor OLE DB para ODBC (`MSDASQL`) e o *data_source* parâmetro.  
  
> [!NOTE]  
>  O nome da fonte de dados ODBC especificado deve ser definido como DSN do sistema antes de você usar o servidor vinculado.  
  
```  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Payroll',   
   @srvproduct = N'',  
   @provider = N'MSDASQL',   
   @datasrc = N'LocalServer';  
GO  
```  
  
### <a name="d-using-the-microsoft-ole-db-provider-for-excel-spreadsheet"></a>D. Usando o Provedor Microsoft OLE DB para planilha do Excel  
 Para criar uma definição de servidor vinculado usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet para acessar uma planilha do Excel no formato 1997-2003, primeiro crie um intervalo nomeado no Excel especificando as colunas e linhas da planilha do Excel para selecionar. O nome do intervalo pode ser então referenciado como um nome de tabela em uma consulta distribuída.  
  
```  
EXEC sp_addlinkedserver 'ExcelSource',  
   'Jet 4.0',  
   'Microsoft.Jet.OLEDB.4.0',  
   'c:\MyData\DistExcl.xls',  
   NULL,  
   'Excel 5.0';  
GO  
```  
  
 Para acessar dados de uma planilha do Excel, associe um intervalo de células com um nome. A consulta a seguir pode ser usada para acessar um intervalo nomeado especificado `SalesData` como uma tabela usando a configuração do servidor vinculado anterior.  
  
```  
SELECT *  
   FROM ExcelSource...SalesData;  
GO  
```  
  
 Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver sendo executado sob uma conta de domínio que tenha acesso a um compartilhamento remoto, um caminho UNC poderá ser usado ao invés de um drive mapeado.  
  
```  
EXEC sp_addlinkedserver 'ExcelShare',  
   'Jet 4.0',  
   'Microsoft.Jet.OLEDB.4.0',  
   '\\MyServer\MyShare\Spreadsheets\DistExcl.xls',  
   NULL,  
   'Excel 5.0';  
```  
  
 Para se conectar a uma planilha do Excel no formato Excel 2007, use o provedor ACE.  
  
```  
EXEC sp_addlinkedserver @server = N'ExcelDataSource',   
@srvproduct=N'ExcelData', @provider=N'Microsoft.ACE.OLEDB.12.0',   
@datasrc=N'C:\DataFolder\People.xlsx',  
@provstr=N'EXCEL 12.0' ;  
  
```  
  
### <a name="e-using-the-microsoft-ole-db-provider-for-jet-to-access-a-text-file"></a>E. Usando o Microsoft OLE DB Provider para Jet para acessar um arquivo de texto  
 O exemplo a seguir cria um servidor vinculado para acessar arquivos de texto diretamente sem vincular os arquivos como tabelas em um arquivo .mdb do Access. O provedor é `Microsoft.Jet.OLEDB.4.0` e a cadeia de caracteres do provedor é `Text`.  
  
 A fonte de dados é o caminho completo do diretório que contém os arquivos de texto. Um arquivo schema.ini, que descreve a estrutura dos arquivos de texto, deve existir no mesmo diretório que os arquivos de texto. Para obter mais informações sobre como criar um arquivo Schema.ini, consulte a documentação do Mecanismo de Banco de Dados do Jet.  
  
```  
--Create a linked server.  
EXEC sp_addlinkedserver txtsrv, N'Jet 4.0',   
   N'Microsoft.Jet.OLEDB.4.0',  
   N'c:\data\distqry',  
   NULL,  
   N'Text';  
GO  
  
--Set up login mappings.  
EXEC sp_addlinkedsrvlogin txtsrv, FALSE, Admin, NULL;  
GO  
  
--List the tables in the linked server.  
EXEC sp_tables_ex txtsrv;  
GO  
  
--Query one of the tables: file1#txt  
--using a four-part name.   
SELECT *   
FROM txtsrv...[file1#txt];  
```  
  
### <a name="f-using-the-microsoft-ole-db-provider-for-db2"></a>F. Usando o Microsoft OLE DB Provider para DB2  
 O exemplo seguinte cria um servidor vinculado nomeado `DB2` que usa a `Microsoft OLE DB Provider for DB2`.  
  
```  
EXEC sp_addlinkedserver  
   @server=N'DB2',  
   @srvproduct=N'Microsoft OLE DB Provider for DB2',  
   @catalog=N'DB2',  
   @provider=N'DB2OLEDB',  
   @provstr=N'Initial Catalog=PUBS;  
       Data Source=DB2;  
       HostCCSID=1252;  
       Network Address=XYZ;  
       Network Port=50000;  
       Package Collection=admin;  
       Default Schema=admin;';  
```  
  
### <a name="g-add-a-includesssdsfullincludessssdsfull-mdmd-as-a-linked-server-for-use-with-distributed-queries-on-cloud-and-on-premise-databases"></a>G. Adicionar um [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] como um servidor vinculado para uso com consultas distribuídas em bancos de dados locais e de nuvem  
 Você pode adicionar um [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] como um servidor vinculado e usá-lo com consultas distribuídas que abrangem os bancos de dados locais e de nuvem. Esse é um componente para as soluções híbridas de banco de dados que abrangem redes corporativas locais e a nuvem do Windows Azure.  
  
 O produto da caixa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém o recurso de consulta distribuída, que permite gravar consultas para combinar dados de fontes de dados locais e dados de fontes remotas (inclusive dados de fontes de dados não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) definidos como servidores vinculados. Cada [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (exceto o mestre virtual) pode ser adicionado como um servidor vinculado individual e pode ser usado diretamente em seus aplicativos de banco de dados, como qualquer outro banco de dados.  
  
 Os benefícios de usar o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] incluem capacidade de gerenciamento, alta disponibilidade, escalabilidade, trabalhando com um modelo familiar de desenvolvimento, e um modelo de dados relacionais. Os requisitos de seu aplicativo de banco de dados determinam como ele usaria o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] na nuvem. Você pode mover todos os dados imediatamente para o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], ou mover progressivamente alguns de seus dados, mantendo os demais dados no local. Para um aplicativo de banco de dados tão híbrido, o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] agora pode ser adicionado como servidores vinculados, e o aplicativo de banco de dados pode emitir consultas distribuídas para combinar dados do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e fontes de dados locais.  
  
 Aqui está um exemplo simples que explica como conectar-se a um [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] usando consultas distribuídas:  
  
```  
------ Configure the linked server  
-- Add one Windows Azure SQL DB as Linked Server  
EXEC sp_addlinkedserver  
@server='myLinkedServer', -- here you can specify the name of the linked server  
@srvproduct='',       
@provider='sqlncli', -- using SQL Server Native Client  
@datasrc='myServer.database.windows.net',   -- add here your server name  
@location='',  
@provstr='',  
@catalog='myDatabase'  -- add here your database name as initial catalog (you cannot connect to the master database)  
-- Add credentials and options to this linked server  
EXEC sp_addlinkedsrvlogin  
@rmtsrvname = 'myLinkedServer',  
@useself = 'false',  
@rmtuser = 'myLogin',             -- add here your login on Azure DB  
@rmtpassword = 'myPassword' -- add here your password on Azure DB  
EXEC sp_serveroption 'myLinkedServer', 'rpc out', true;  
------ Now you can use the linked server to execute 4-part queries  
-- You can create a new table in the Azure DB  
exec ('CREATE TABLE t1tutut2(col1 int not null CONSTRAINT PK_col1 PRIMARY KEY CLUSTERED (col1) )') at myLinkedServer  
-- Insert data from your local SQL Server  
exec ('INSERT INTO t1tutut2 VALUES(1),(2),(3)') at myLinkedServer  
  
-- Query the data using 4-part names  
select * from myLinkedServer.myDatabase.dbo.myTable  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de consultas de Distributed &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [sp_setnetname &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setnetname-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
