---
title: Atualizando um aplicativo para o Driver do OLE DB para SQL Server do MDAC | Microsoft Docs
description: Atualizando um aplicativo para o Driver do OLE DB para SQL Server do MDAC
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, vs. MDAC
- OLE DB Driver for SQL Server, vs. MDAC
- data access [OLE DB Driver for SQL Server], vs. MDAC
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 11597ed3b7cd80cae8604291bd8b662bf6a9ed80
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612101"
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>Atualizando um aplicativo para o Driver do OLE DB para SQL Server do MDAC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Há algumas diferenças entre o OLE DB Driver para SQL Server e o Microsoft Data Access Components (MDAC); começando com o Windows Vista, os componentes de acesso de dados agora são chamados de Windows Data Access Components (ou Windows DAC). Ainda que ambos forneçam acesso a dados nativos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bancos de dados, Driver OLE DB para SQL Server foi projetado para expor os novos recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ao mesmo tempo que mantém a compatibilidade com versões anteriores.   

 Além disso, embora o MDAC contenha componentes para uso do OLE DB, ODBC e ActiveX Data Objects (ADO), OLE DB Driver para SQL Server implementa apenas OLE DB (embora o ADO pode acessar a funcionalidade do Driver do OLE DB para SQL Server).  

 OLE DB Driver para SQL Server e o MDAC são diferentes nas seguintes áreas:  

-   Os usuários que usam o ADO para acessar o Driver OLE DB para SQL Server podem encontrar menos funcionalidade de filtragem de acesso ao provedor SQL OLE DB.  

-   Se um aplicativo ADO usa o Driver do OLE DB para SQL Server e tenta atualizar uma coluna computada, um erro será relatado. Com o MDAC, a atualização foi aceita, mas ignorada.  

-   OLE DB Driver para SQL Server é um arquivo de biblioteca (DLL) único vínculo dinâmico autossuficiente. As interfaces expostas publicamente foram mantidas no mínimo, tanto para facilitar a distribuição quanto para limitar a exposição de segurança.  

-   Somente as interfaces OLE DB têm suporte.  

-   O Driver OLE DB para nomes do SQL Server são diferentes dos nomes usados com o MDAC.  

-   Funcionalidade acessível ao usuário fornecida pelos componentes do MDAC está disponível ao usar o Driver do OLE DB para SQL Server. Isso inclui, mas não se limita a, o seguinte: pool de conexões, suporte ao ADO e suporte ao cursor do cliente. Quando esses recursos são usados, o OLE DB Driver para SQL Server fornece apenas conectividade de banco de dados. O MDAC fornece funcionalidades como, por exemplo, rastreamento, controles de gerenciamento e contadores de desempenho.  

-   Aplicativos podem usar os serviços principais do OLE DB com o Driver do OLE DB para SQL Server, mas se usar o mecanismo de cursor de OLE DB, eles devem usar a opção de compatibilidade de tipo de dados para evitar problemas potenciais que podem surgir porque o mecanismo de cursor não tem conhecimento do novo [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] tipos de dados.  

-   OLE DB Driver para SQL Server dá suporte a acesso a anterior [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bancos de dados.  

-   OLE DB Driver para SQL Server não contém integração XML. OLE DB Driver para SQL Server dá suporte a selecione... Consultas, XML, mas não oferece suporte a qualquer outra funcionalidade XML. No entanto, o OLE DB Driver para SQL Server oferece suporte a **xml** tipo de dados introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

-   OLE DB Driver para SQL Server dá suporte à configuração de bibliotecas de rede do cliente usando somente atributos de cadeia de caracteres de conexão. Caso precise de uma configuração de biblioteca de rede mais completa, você deve usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.  

-   Cadeias de caracteres de conexão MDAC permitem um valor booliano (**true**) para o **Trusted_Connection** palavra-chave. Um Driver OLE DB para a cadeia de conexão do SQL Server deve usar **Sim** ou **sem**.  

-   As alterações menores ocorreram por conta de avisos e erros. Avisos e erros retornados pelo servidor agora mantêm a mesma severidade quando passados para o Driver do OLE DB para SQL Server. Você não deve se esquecer de testar integralmente o aplicativo caso dependa da interceptação de avisos e erros específicos.  

-   OLE DB Driver para SQL Server tem mais uma verificação de erro MDAC, o que significa que alguns aplicativos que não se adaptam rigidamente às especificações do OLE DB podem se comportar de maneira diferente. Por exemplo, o provedor SQLOLEDB não impunha a regra que nomes de parâmetro devem começar com ' \@' para o resultado faz os parâmetros, mas o Driver OLE DB para SQL Server.  

-   OLE DB Driver para SQL Server tem um comportamento diferente do MDAC sobre as conexões com falha. Por exemplo, o MDAC retorna valores de propriedade em cache para uma conexão que falhou, enquanto o OLE DB Driver para SQL Server relata um erro para o aplicativo de chamada.  

-   OLE DB Driver para SQL Server não gera eventos de analisador do Visual Studio, mas em vez disso gera eventos de rastreamento do Windows.  

-   OLE DB Driver para SQL Server não pode ser usado com perfmon. Perfmon é uma ferramenta do Windows que pode ser usada apenas com DSNs que usem o driver SQLODBC do MDAC incluído no Windows.  

-   Quando o OLE DB Driver para SQL Server está conectado à [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versões posteriores, o erro de servidor 16947 é retornado como SQL_ERROR. Esse erro ocorre quando uma atualização ou exclusão posicionada não atualiza ou exclui uma linha. Com o MDAC, ao estabelecer conexão com qualquer versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o erro de servidor 16947 é retornado como um aviso (SQL_SUCCESS_WITH_INFO).  

-   OLE DB Driver para SQL Server implementa o **IDBDataSourceAdmin** interface, que é uma interface OLE DB opcional não foi implementada anteriormente, mas apenas o **CreateDataSource** método deste interface opcional é implementado. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   O Driver OLE DB para SQL Server retorna sinônimos em tabelas e TABLE_INFO conjuntos de linhas de esquema, com TABLE_TYPE definido como sinônimo.  

-   Retornar valores de tipo de dados **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, **udt**, ou outros tipos de objeto grande não podem ser retornados para as versões do cliente anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Se você quiser usar esses tipos como valores de retorno, você deve usar o Driver do OLE DB para SQL Server.  

-   MDAC permite que as instruções a seguir ser executado no início das transações manuais e implícitas, mas não OLE DB Driver para SQL Server. Elas devem ser executadas no modo de confirmação automática.  

    -   Todas as operações de texto completo (indexar e catalogar DDL)  

    -   Todas as operações de banco de dados (criar, alterar, descartar banco de dados)  

    -   Reconfiguração  

    -   Shutdown  

    -   Eliminação  

    -   Backup  

-   Quando os aplicativos do MDAC se conectarem ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], os tipos de dados introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] serão exibidos como tipos de dados compatíveis com o [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)], como mostrado na seguinte tabela.  

    |Tipo SQL Server 2005|Tipo do SQL Server 2000|  
    |--------------------------|--------------------------|  
    |**varchar(max)**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**image**|  
    |**udt**|**varbinary**|  
    |**xml**|**ntext**|  

     Esse mapeamento de tipo afeta os valores retornados para metadados da coluna. Por exemplo, um **texto** coluna tem um tamanho máximo de 2.147.483.647, mas OLE DB Driver para SQL Server informa o tamanho máximo de **varchar (max)** colunas como 2.147.483.647 ou -1, dependendo da plataforma.  

-   OLE DB Driver para SQL Server permite ambiguidade em cadeias de caracteres de conexão (por exemplo, algumas palavras-chave pode ser especificado mais de uma vez e conflitantes, permitidas tendo a resolução baseada na posição ou na precedência) para fins de compatibilidade com versões anteriores. Versões futuras do OLE DB Driver for SQL Server talvez não permitam ambiguidade em cadeias de caracteres de conexão. É uma boa prática ao modificar aplicativos para usar o OLE DB Driver para SQL Server para eliminar qualquer dependência em ambiguidade da cadeia de caracteres de conexão.  

-   Se você usar uma chamada OLE DB para iniciar transações, há uma diferença de comportamento entre o OLE DB Driver para SQL Server e o MDAC; as transações começarão imediatamente com o Driver do OLE DB para SQL Server, mas as transações começarão após o primeiro banco de dados de acesso usando o MDAC. Isso pode afetar o comportamento de procedimentos armazenados e lotes porque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requer@TRANCOUNT para ser o mesmo depois que um lote ou procedimento armazenado finaliza a execução como ele era quando o lote ou procedimento armazenado iniciado.  

-   Com OLE DB para SQL Server, ITransactionLocal::BeginTransaction fará com que uma transação seja iniciada imediatamente. Com o MDAC o início da transação foi atrasado até que o aplicativo executasse uma instrução que exigia uma transação em modo de transação implícita. Para obter mais informações, confira [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md).  


 Ambos os Driver OLE DB para o suporte do SQL Server e o MDAC isolamento de transação confirmada usando controle de versão de linha, mas somente OLE DB Driver para isolamento de transação do SQL Server dá suporte a instantâneo de leitura. (Em termos de programação, isolamento de transação de leitura confirmada usando controle de versão de linha é igual à transação de leitura confirmada.).  

## <a name="see-also"></a>Consulte também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
