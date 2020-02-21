---
title: Atualização de um aplicativo do Driver do OLE DB para SQL Server no MDAC | Microsoft Docs
description: Atualização de um aplicativo do Driver do OLE DB para SQL Server no MDAC
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, vs. MDAC
- OLE DB Driver for SQL Server, vs. MDAC
- data access [OLE DB Driver for SQL Server], vs. MDAC
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: pelopes
ms.openlocfilehash: ad36a17367b14a48810d83137b2887eaa75f6ef1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67989266"
---
# <a name="updating-an-application-to-ole-db-driver-for-sql-server-from-mdac"></a>Atualização de um aplicativo do Driver do OLE DB para SQL Server no MDAC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Há várias diferenças entre o Driver do OLE DB para SQL Server e o MDAC (Microsoft Data Access Components); começando pelo Windows Vista, os componentes de acesso a dados agora são chamados de Windows DAC (ou de Windows Data Access Components). Ainda que ambos forneçam acesso nativo a dados em bancos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o Driver do OLE DB para SQL Server foi especificamente projetado para expor os novos recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ao mesmo tempo em que mantém a compatibilidade com versões anteriores.   

 Além disso, embora o MDAC contenha componentes para usar o OLE DB, ODBC e ADO (ActiveX Data Objects), o Driver do OLE DB para SQL Server implementa apenas o OLE DB (ainda que o ADO possa acessar a funcionalidade do Driver do OLE DB para SQL Server).  

 O Driver do OLE DB para SQL Server e o MDAC são diferentes nas demais áreas a seguir:  

-   Aqueles que usam o ADO para acessar o Driver do OLE DB para SQL Server podem encontrar menos funcionalidade de filtragem do que quando acessam o provedor OLE DB do SQL.  

-   Se um aplicativo do ADO usar o Driver do OLE DB para SQL Server e tentar atualizar uma coluna computada, será informado um erro. Com o MDAC, a atualização foi aceita, mas ignorada.  

-   O Driver do OLE DB para SQL Server é um único arquivo DLL (biblioteca de vínculo dinâmico) autossuficiente. As interfaces expostas publicamente foram mantidas no mínimo, tanto para facilitar a distribuição quanto para limitar a exposição de segurança.  

-   Só há suporte para interfaces OLE DB.  

-   Os nomes do Driver do OLE DB para SQL Server são diferentes dos nomes usados no MDAC.  

-   A funcionalidade acessível ao usuário fornecida pelos componentes do MDAC está disponível quando o Driver do OLE DB para SQL Server é usado. Isso inclui, mas não se limita a, o seguinte: pool de conexões, suporte ao ADO e suporte ao cursor do cliente. Quando algum desses recursos é usado, o Driver do OLE DB para SQL Server só fornece a conectividade de banco de dados. O MDAC fornece funcionalidades como, por exemplo, rastreamento, controles de gerenciamento e contadores de desempenho.  

-   Os aplicativos podem usar os serviços principais do OLE DB com o Driver do OLE DB para SQL Server, mas, se usarem o mecanismo de cursor do OLE DB, eles deverão usar a opção de compatibilidade do tipo de dados para evitar problemas potenciais que possam surgir em decorrência do desconhecimento dos novos tipos de dados do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] pelo mecanismo de cursor.  

-   O Driver do OLE DB para SQL Server dá suporte ao acesso a bancos de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores.  

-   O Driver do OLE DB para SQL Server não tem integração XML. O Driver do OLE DB para SQL Server dá suporte a consultas SELECT ... FOR XML, mas não a qualquer outra funcionalidade XML. No entanto, o Driver do OLE DB para SQL Server dá suporte ao tipo de dados **xml** introduzido em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

-   O Driver do OLE DB para SQL Server dá suporte à configuração de bibliotecas de rede do lado do cliente que usam apenas atributos da cadeia de conexão. Caso precise de uma configuração de biblioteca de rede mais completa, você deve usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.  

-   As cadeias de conexão MDAC permitem um valor booliano (**true**) para a palavra-chave **Trusted_Connection**. Uma cadeia de conexão Driver do Microsoft OLE DB para SQL Server deve usar **yes** ou **no**.  

-   As alterações menores ocorreram por conta de avisos e erros. Avisos e erros retornados pelo servidor agora mantêm a mesma severidade quando passados para o Driver do OLE DB para SQL Server. Você não deve se esquecer de testar integralmente o aplicativo caso dependa da interceptação de avisos e erros específicos.  

-   O Driver do OLE DB para SQL Server apresenta uma verificação de erro mais rígida do que o MDAC, o que significa que alguns aplicativos que não se adaptam rigidamente às especificações do OLE DB podem se comportar de maneira diferente. Por exemplo, o provedor SQLOLEDB não impunha a regra de que os nomes de parâmetro devem começar com '\@' em parâmetros de resultado, mas o Driver do OLE DB para SQL Server, sim.  

-   O Driver do OLE DB para SQL Server se comporta de maneira diferente em relação ao MDAC no que diz respeito a falhas de conexão. Por exemplo, o MDAC retorna valores de propriedade armazenados em cache para uma falha de conexão, ao passo que o Driver do OLE DB para SQL Server informa um erro ao aplicativo de chamada.  

-   O Driver do OLE DB para SQL Server não gera eventos do Visual Studio Analyzer, e sim eventos de rastreamento do Windows.  

-   O Driver do OLE DB para SQL Server não pode ser usado com perfmon. Perfmon é uma ferramenta do Windows que pode ser usada apenas com DSNs que usem o driver SQLODBC do MDAC incluído no Windows.  

-   Quando o Driver do OLE DB para SQL Server é conectado ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versões posteriores, o erro de servidor 16947 é retornado como SQL_ERROR. Esse erro ocorre quando uma atualização ou exclusão posicionada não atualiza ou exclui uma linha. Com o MDAC, ao estabelecer conexão com qualquer versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o erro de servidor 16947 é retornado como um aviso (SQL_SUCCESS_WITH_INFO).  

-   O Driver do OLE DB para SQL Server implementa a interface **IDBDataSourceAdmin**, que é uma interface OLE DB opcional não implementada anteriormente, mas apenas o método **CreateDataSource** dessa interface opcional é implementado. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  

-   O provedor OLE DB do Driver do OLE DB para SQL Server retorna sinônimos nos conjuntos de linhas de esquema TABLES e TABLE_INFO, com TABLE_TYPE definido como SYNONYM.  

-   Valores de retorno do tipo de dados **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , **xml**, **udt** ou outros tipos de objeto grandes não podem ser retornados a versões do cliente anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Caso queira usar esses tipos como valores de retorno, você deve usar o Driver do OLE DB para SQL Server.  

-   O MDAC permite que as seguintes instruções sejam executadas no início das transações manuais e implícitas, mas o Driver do OLE DB para SQL Server, não. Elas devem ser executadas no modo de confirmação automática.  

    -   Todas as operações de texto completo (indexar e catalogar DDL)  

    -   Todas as operações de banco de dados (criar, alterar, descartar banco de dados)  

    -   Reconfigurar  

    -   Shutdown  

    -   Encerrar  

    -   Backup  

-   Quando os aplicativos do MDAC se conectarem ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], os tipos de dados introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] serão exibidos como tipos de dados compatíveis com o [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)], como mostrado na seguinte tabela.  

    |Tipo SQL Server 2005|Tipo do SQL Server 2000|  
    |--------------------------|--------------------------|  
    |**varchar(max)**|**text**|  
    |**nvarchar(max)**|**ntext**|  
    |**varbinary(max)**|**imagem**|  
    |**udt**|**varbinary**|  
    |**xml**|**ntext**|  

     Esse mapeamento de tipo afeta os valores retornados para metadados da coluna. Por exemplo, uma coluna **text** tem um tamanho máximo de 2.147.483.647, mas o Driver do OLE DB para SQL Server relata o tamanho máximo das colunas **varchar (max)** como 2.147.483.647 ou -1, dependendo da plataforma.  

-   O Driver do OLE DB para SQL Server permite ambiguidade em cadeias de conexão (por exemplo, algumas palavras-chave podem ser especificadas mais de uma vez e outras, conflitantes, permitidas tendo a resolução baseada na posição ou na precedência) tendo em vista a compatibilidade com versões anteriores. Futuras versões do Driver do OLE DB para SQL Server talvez não permitam ambiguidade em cadeias de conexão. Trata-se de uma boa prática, ao modificar aplicativos, usar o Driver do OLE DB para SQL Server para eliminar todas as dependências relacionadas à ambiguidade da cadeia de conexão.  

-   Caso você use uma chamada OLE DB para iniciar transações, existe uma diferença de comportamento entre o Driver do OLE DB para SQL Server e o MDAC. As transações começarão imediatamente com o Driver do OLE DB para SQL Server e só começarão no MDAC depois do primeiro acesso ao banco de dados. Isso pode afetar o comportamento de procedimentos armazenados e lotes porque o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exige que @@TRANCOUNT seja o mesmo de quando o lote o ou procedimento armazenado começou após a conclusão da execução.  

-   Com o Driver do OLE DB para SQL Server, ITransactionLocal::BeginTransaction fará com que uma transação seja iniciada imediatamente. Com o MDAC, o início da transação foi atrasado até que o aplicativo executasse uma instrução que exigia uma transação em modo de transação implícita. Para obter mais informações, confira [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md).  


 Tanto o Driver do OLE DB para SQL Server quanto o MDAC oferecem suporte ao isolamento de transação de leitura confirmada usando controle de versão de linha, mas apenas o Driver do OLE DB para SQL Server dá suporte ao isolamento da transação de instantâneo. (Em termos de programação, o isolamento de transação de leitura confirmada por meio do controle de versão de linha é igual à transação de leitura confirmada.)  

## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
