---
title: OPENDATASOURCE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd106322dfc78186aefaadac42622852d87d40f2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="opendatasource-transact-sql"></a>OPENDATASOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fornece informações de conexão ad hoc como parte de um nome de objeto de quatro partes sem usar um nome de servidor vinculado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
OPENDATASOURCE ( provider_name, init_string )  
```  
  
## <a name="arguments"></a>Argumentos  
 *provider_name*  
 É o nome registrado como PROGID do provedor OLE DB usado para acessar a fonte de dados. *provider_name* é um **char** tipo de dados, sem nenhum valor padrão.  
  
 *init_string*  
 A cadeia de caracteres de conexão é passada para a interface IDataInitialize do provedor de destino. A sintaxe da cadeia de caracteres de provedor baseia-se em pares de palavra-chave-valor separados por ponto e vírgula, como: **'***keyword1*=*valor***;** *keyword2*=*valor***'**.  
  
 Para ver os pares de valor e palavra-chave específicos com suporte no provedor, consulte o SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access. Essa documentação define a sintaxe básica. A tabela a seguir listas usadas mais frequentemente palavras-chave no *init_string* argumento.  
  
|Palavra-chave|Propriedade OLE DB|Valores válidos e descrição|  
|-------------|---------------------|----------------------------------|  
|Fonte de dados|DBPROP_INIT_DATASOURCE|Nome da fonte de dados à qual se conectar. Provedores diferentes interpretam isso de várias formas. Para o provedor OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, isso indica o nome do servidor. Para o provedor OLE DB Jet, indica o caminho completo do arquivo .mdb ou .xls.|  
|Local|DBPROP_INIT_LOCATION|Local do banco de dados ao qual se conectar.|  
|Propriedades estendidas|DBPROP_INIT_PROVIDERSTRING|A cadeia de conexão específica do provedor.|  
|Tempo limite de conexão|DBPROP_INIT_TIMEOUT|Valor de tempo limite após o qual a tentativa de conexão falha.|  
|ID de usuário|DBPROP_AUTH_USERID|ID de usuário a ser usada para a conexão.|  
|Senha|DBPROP_AUTH_PASSWORD|Senha a ser usada para a conexão.|  
|Catálogo|DBPROP_INIT_CATALOG|O nome do catálogo inicial ou padrão durante a conexão à fonte de dados.|  
|Segurança Integrada|DBPROP_AUTH_INTEGRATED|SSPI, para especificar a Autenticação do Windows|  
  
## <a name="remarks"></a>Comentários  
 A função OPENDATASOURCE pode ser usada para acessar dados remotos de fontes de dados OLE DB somente quando a opção do Registro DisallowAdhocAccess está definida explicitamente como 0 para o provedor especificado, e a opção de configuração avançada Ad Hoc Distributed Queries está habilitada. Quando essas opções não estão definidas, o comportamento padrão não permite acesso ad hoc.  
  
 A função OPENDATASOURCE pode ser usada nos mesmos locais da sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] que um nome de servidor vinculado. Portanto, OPENDATASOURCE pode ser usada como a primeira parte de um nome de quatro partes que faz referência a um nome de tabela ou exibição em uma instrução SELECT, INSERT, UPDATE ou DELETE, ou a um procedimento armazenado remoto em uma instrução EXECUTE. Ao executar procedimentos armazenados remotos, OPENDATASOURCE deve fazer referência a outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. OPENDATASOURCE não aceita variáveis para seus argumentos.  
  
 Assim como a função OPENROWSET, OPENDATASOURCE deve referenciar apenas fontes de dados OLE DB que são acessadas com pouca frequência. Defina um servidor vinculado para qualquer fonte de dados acessada muitas vezes. Nem OPENDATASOURCE nem OPENROWSET fornecem todas as funcionalidades de definições de servidor vinculado, como gerenciamento de segurança e capacidade de consultar informações do catálogo. Todas as informações de conexão, inclusive senhas, devem ser fornecidas sempre que OPENDATASOURCE é chamada.  
  
> [!IMPORTANT]  
>  A Autenticação do Windows é muito mais segura do que a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sempre que possível, você deve usar a Autenticação do Windows. OPENDATASOURCE não deve ser usada com senhas explícitas na cadeia de conexão.  
  
 Os requisitos de conexão de cada provedor são semelhantes aos requisitos desses parâmetros durante a criação de servidores vinculados. Os detalhes dos muitos provedores comuns estão listados no tópico [sp_addlinkedserver &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
 Qualquer chamada para OPENDATASOURCE, OPENQUERY ou OPENROWSET na cláusula FROM é avaliada separada e independentemente de qualquer chamada para essas funções usadas como o destino da atualização, mesmo se argumentos idênticos forem fornecidos às duas chamadas. Em particular, as condições de filtro ou junção aplicadas no resultado de uma dessas chamadas não têm efeito sobre os resultado da outra.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode executar OPENDATASOURCE. As permissões usadas para estabelecer conexão com o servidor remoto são determinadas na cadeia de conexão.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma conexão com a instância `Payroll` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor `London` e consulta `AdventureWorks2012.HumanResources.Employee`. (Use SQLNCLI, e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fará o redirecionamento para a última versão do provedor OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.)  
  
```  
SELECT *  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=London\Payroll;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Employee  
```  
  
 O exemplo a seguir cria uma conexão ad hoc com uma planilha do Excel no formato 1997 - 2003.  
  
```  
SELECT * FROM OPENDATASOURCE('Microsoft.Jet.OLEDB.4.0',  
'Data Source=C:\DataFolder\Documents\TestExcel.xls;Extended Properties=EXCEL 5.0')...[Sheet1$] ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
  

