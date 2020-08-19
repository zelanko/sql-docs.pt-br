---
description: OPENDATASOURCE (Transact-SQL)
title: OPENDATASOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/26/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPENDATASOURCE
- OPENDATASOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENDATASOURCE function
- remote data access [SQL Server], OPENDATASOURCE
- ad hoc distributed queries
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: 5510b846-9cde-4687-8798-be9a273aad31
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: a10994ac46bc1070304823dd5ae698a5b94c017d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445634"
---
# <a name="opendatasource-transact-sql"></a>OPENDATASOURCE (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Fornece informações de conexão ad hoc como parte de um nome de objeto de quatro partes sem usar um nome de servidor vinculado.  

 ![Ícone de link](../../database-engine/configure-windows/media/topic-link.gif "ícone de link") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
OPENDATASOURCE ( 'provider_name', 'init_string' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 '*provider_name*'  
 É o nome registrado como PROGID do provedor OLE DB usado para acessar a fonte de dados. *provider_name* é um tipo de dados **char** sem nenhum valor padrão.  

 > [!IMPORTANT]
 > O Microsoft OLE DB Provider para SQL Server (SQLOLEDB) anterior e o provedor SQL Server Native Client OLE DB (SQLNCLI) permanecem preteridos e não é recomendável usar nenhum dos dois para um novo trabalho de desenvolvimento. Em vez disso, use o novo [Driver do Microsoft OLE DB para SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL), que será atualizado com os recursos de servidor mais recentes.
 
 '*init_string*'  
 É a cadeia de conexão passada à interface IDataInitialize do provedor de destino. A sintaxe de cadeia de caracteres de provedor é baseada em pares palavra-chave e valor separados por ponto e vírgula, como: **'** _palavra-chave1_=_valor_ **;** _palavra-chave2_=_valor_ **'** .  
  
 Para ver os pares de valor e palavra-chave específicos com suporte no provedor, consulte o SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access. Essa documentação define a sintaxe básica. A tabela a seguir lista as palavras-chave mais usadas no argumento *init_string*.  
  
|Palavra-chave|Propriedade OLE DB|Valores válidos e descrição|  
|-------------|---------------------|----------------------------------|  
|fonte de dados|DBPROP_INIT_DATASOURCE|Nome da fonte de dados à qual se conectar. Provedores diferentes interpretam isso de várias formas. Para o provedor OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, isso indica o nome do servidor. Para o provedor OLE DB Jet, indica o caminho completo do arquivo .mdb ou .xls.|  
|Local|DBPROP_INIT_LOCATION|Local do banco de dados ao qual se conectar.|  
|Propriedades estendidas|DBPROP_INIT_PROVIDERSTRING|A cadeia de conexão específica do provedor.|  
|Tempo limite de conexão|DBPROP_INIT_TIMEOUT|Valor de tempo limite após o qual a tentativa de conexão falha.|  
|Id de Usuário|DBPROP_AUTH_USERID|ID de usuário a ser usada para a conexão.|  
|Senha|DBPROP_AUTH_PASSWORD|Senha a ser usada para a conexão.|  
|Catálogo|DBPROP_INIT_CATALOG|O nome do catálogo inicial ou padrão durante a conexão à fonte de dados.|  
|Segurança Integrada|DBPROP_AUTH_INTEGRATED|SSPI, para especificar a Autenticação do Windows|  
  
## <a name="remarks"></a>Comentários  
`OPENROWSET` sempre herda o agrupamento da instância, independentemente do conjunto de agrupamentos para colunas.

`OPENDATASOURCE` pode ser usado para acessar dados remotos de fontes de dados OLE DB somente quando a opção do Registro DisallowAdhocAccess está definida explicitamente como 0 para o provedor especificado, e a opção de configuração avançada Consultas Distribuídas Ad Hoc está habilitada. Quando essas opções não estão definidas, o comportamento padrão não permite acesso ad hoc.  
  
A função `OPENDATASOURCE` pode ser usada nos mesmos locais da sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] que um nome do servidor vinculado. Portanto, `OPENDATASOURCE` pode ser usada como a primeira parte de um nome de quatro partes que faz referência a um nome de tabela ou exibição em uma instrução SELECT, INSERT, UPDATE ou DELETE, ou a um procedimento armazenado remoto em uma instrução EXECUTE. Ao executar procedimentos armazenados remotos, `OPENDATASOURCE` deve fazer referência a outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. OPENDATASOURCE não aceita variáveis para seus argumentos.  
  
Assim como a função `OPENROWSET`, `OPENDATASOURCE` deve referenciar apenas fontes de dados OLE DB que são acessadas com pouca frequência. Defina um servidor vinculado para qualquer fonte de dados acessada muitas vezes. Nem OPENDATASOURCE nem OPENROWSET fornecem todas as funcionalidades de definições de servidor vinculado, como gerenciamento de segurança e capacidade de consultar informações do catálogo. Todas as informações de conexão, inclusive senhas, devem ser fornecidas sempre que OPENDATASOURCE é chamada.  
  
> [!IMPORTANT]  
> A Autenticação do Windows é muito mais segura do que a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sempre que possível, você deve usar a Autenticação do Windows. `OPENDATASOURCE` não deve ser usada com senhas explícitas na cadeia de conexão.  
  
Os requisitos de conexão de cada provedor são semelhantes aos requisitos desses parâmetros durante a criação de servidores vinculados. Os detalhes dos muitos provedores comuns estão listados no artigo [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
Qualquer chamada a `OPENDATASOURCE`, `OPENQUERY` ou `OPENROWSET` na cláusula `FROM` é avaliada separada e independentemente de qualquer chamada a essas funções usadas como o destino da atualização, mesmo se argumentos idênticos forem fornecidos às duas chamadas. Em particular, as condições de filtro ou junção aplicadas no resultado de uma dessas chamadas não têm efeito sobre os resultados da outra.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode executar OPENDATASOURCE. As permissões usadas para estabelecer conexão com o servidor remoto são determinadas na cadeia de conexão.  
  
## <a name="examples"></a>Exemplos  

### <a name="a-using-opendatasource-with-select-and-the-sql-server-ole-db-driver"></a>a. Usar OPENDATASOURCE com SELECT e o Driver do OLE DB para SQL Server  
 O exemplo a seguir usa o [Driver do Microsoft OLE DB para SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) Native Client para acessar a tabela `HumanResources.Department` do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] no servidor remoto `Seattle1`. Uma instrução `SELECT` é usada para definir o conjunto de linhas retornado. A cadeia de caracteres de provedor contém as palavras-chave `Server` e `Trusted_Connection`. Essas palavras-chave são reconhecidas pelo Driver do OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
SELECT GroupName, Name, DepartmentID  
FROM OPENDATASOURCE('MSOLEDBSQL', 'Server=Seattle1;Database=AdventureWorks2016;TrustServerCertificate=Yes;Trusted_Connection=Yes;').HumanResources.Department  
ORDER BY GroupName, Name;  
``` 

### <a name="b-using-opendatasource-with-select-and-the-sql-server-ole-db-provider"></a>B. Usar OPENDATASOURCE com SELECT e o Provedor do OLE DB para SQL Server  
O exemplo a seguir cria uma conexão com a instância `Payroll` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor `London` e consulta `AdventureWorks2012.HumanResources.Employee`. 

> [!NOTE] 
> Usar SQLNCLI redirecionará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a última versão do provedor OLE DB do SQL Server Native Client. Espera-se que o provedor OLE DB seja registrado com o PROGID especificado fornecido no Registro. 

> [!IMPORTANT]  
> O SQL Server Native Client OLE DB (SQLNCLI) permanece preterido e não é recomendável usá-lo para um novo trabalho de desenvolvimento. Em vez disso, use o novo [Driver do Microsoft OLE DB para SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL), que será atualizado com os recursos de servidor mais recentes.
  
```sql  
SELECT *  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=London\Payroll;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Employee;  
```  

### <a name="c-using-the-microsoft-ole-db-provider-for-jet"></a>C. Usando o Microsoft OLE DB Provider for Jet   
 O exemplo a seguir cria uma conexão ad hoc com uma planilha do Excel no formato 1997 - 2003.  
  
```sql  
SELECT * FROM OPENDATASOURCE('Microsoft.Jet.OLEDB.4.0',  
    'Data Source=C:\DataFolder\Documents\TestExcel.xls;Extended Properties=EXCEL 5.0')...[Sheet1$] ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
