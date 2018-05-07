---
title: Atualizando um aplicativo para o SQL Server Native Client do MDAC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQLNCLI, vs. MDAC
- SQL Server Native Client, vs. MDAC
- data access [SQL Server Native Client], vs. MDAC
- SQL Server Native Client, updating applications
ms.assetid: 2860efdd-c59a-4deb-8a0e-5124a8f4e6dd
caps.latest.revision: 81
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 26efb6569ba997ed8eb53036987081b2cf8f5f2a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="updating-an-application-to-sql-server-native-client-from-mdac"></a>Atualizando um aplicativo do MDAC para o SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Há várias diferenças entre o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o MDAC (Microsoft Data Access Components); a partir do Windows Vista, os componentes de acesso aos dados agora são chamados de Windows DAC ou de Windows Data Access Components). Ainda que ambos forneçam acesso a dados em bancos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client foi especificamente projetado para expor os novos recursos do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], ao mesmo tempo em que mantém a compatibilidade com versões anteriores.  
  
 As informações deste tópico ajudam a atualizar o aplicativo MDAC (ou Windows DAC) em relação à versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client incluída no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Para ajudar a tornar este aplicativo a ser atualizado com a versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client fornecida no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], consulte [atualizando um aplicativo do SQL Server 2005 Native Client](../../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md).  
  
 Além disso, muito embora o MDAC contenha componentes para usar OLE DB, ODBC e ADO (ActiveX Data Objects), o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa apenas OLE DB e ODBC (ainda que o ADO possa acessar a funcionalidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client).  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o MDAC são diferentes nas demais áreas a seguir:  
  
-   Aqueles que usam o ADO para acessar um provedor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client podem encontrar menos funcionalidade de filtragem do que quando acessam um provedor OLE DB SQL.  
  
-   Se um aplicativo do ADO usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e tentar atualizar uma coluna computada, será informado um erro. Com o MDAC, a atualização foi aceita, mas ignorada.  
  
-   O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client é um único arquivo DLL (biblioteca de vínculo dinâmico) autossuficiente. As interfaces expostas publicamente foram mantidas no mínimo, tanto para facilitar a distribuição quanto para limitar a exposição de segurança.  
  
-   Só há suporte para interfaces OLE DB e ODBC.  
  
-   O provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e os nomes do driver ODBC são diferentes dos usados com o MDAC.  
  
-   A funcionalidade acessível ao usuário fornecida pelos componentes do MDAC está disponível quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client é usado. Isso inclui, mas não se limita a, o seguinte: pool de conexões, suporte ao ADO e suporte ao cursor do cliente. Quando algum desses recursos é usado, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client fornece apenas conectividade de banco de dados. O MDAC fornece funcionalidades como, por exemplo, rastreamento, controles de gerenciamento e contadores de desempenho.  
  
-   Os aplicativos podem usar os serviços principais do OLE DB com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, mas, se usarem o mecanismo de cursor do OLE DB, eles deverão usar a opção de compatibilidade do tipo de dados para evitar problemas potenciais que possam surgir em decorrência do desconhecimento dos novos tipos de dados do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] pelo mecanismo de cursor.  
  
-   O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client dá suporte a acesso a bancos de dados anteriores ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não contém integração XML. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte a selecione... Consultas, XML, mas não oferece suporte a qualquer outra funcionalidade XML. No entanto, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte a **xml** tipo de dados introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
-   O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte à configuração de bibliotecas de rede do lado do cliente que usam apenas atributos da cadeia de conexão. Caso precise de uma configuração de biblioteca de rede mais completa, você deve usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.  
  
-   O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não é compatível com odbcbcp.dll. Aplicativos que usam ODBC e **bcp** APIs devem ser recriados para vinculados com sqlncli11.lib e para usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
-   Não há suporte para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no Microsoft OLE DB Provider for ODBC (MSDASQL). Se você estiver usando o driver MDAC SQLODBC com MSDASQL ou o driver MDAC SQLODBC com ADO, use OLE DB no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
-   Cadeias de caracteres de conexão MDAC permitem um valor booliano (**true**) para o **Trusted_Connection** palavra-chave. Um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve usar a cadeia de caracteres de conexão de cliente nativo **Sim** ou **sem**.  
  
-   As alterações menores ocorreram por conta de avisos e erros. Avisos e erros retornados pelo servidor agora mantêm a mesma severidade quando passados para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Você não deve se esquecer de testar integralmente o aplicativo caso dependa da interceptação de avisos e erros específicos.  
  
-   O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client apresenta uma verificação de erro mais rígida do que o MDAC, o que significa que alguns aplicativos que não se adaptam rigidamente às especificações do ODBC e do OLE DB podem se comportar de maneira diferente. Por exemplo, o provedor SQLOLEDB não impunha a regra de que os nomes de parâmetro devem começar com '@' em parâmetros de resultado, mas o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, sim.  
  
-   O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se comporta de maneira diferente em relação ao MDAC no que diz respeito a falhas de conexão. Por exemplo, o MDAC retorna valores de propriedade armazenados em cache para uma falha de conexão, ao passo que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client informa um erro ao aplicativo de chamada.  
  
-   O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não gera eventos do Analisador do Visual Studio, e sim eventos de rastreamento do Windows.  
  
-   O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não pode ser usado com perfmon. Perfmon é uma ferramenta do Windows que pode ser usada apenas com DSNs que usem o driver SQLODBC do MDAC incluído no Windows.  
  
-   Quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client é conectado ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versões posteriores, o erro de servidor 16947 é retornado como SQL_ERROR. Esse erro ocorre quando uma atualização ou exclusão posicionada não atualiza ou exclui uma linha. Com o MDAC, ao estabelecer conexão com qualquer versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o erro de servidor 16947 é retornado como um aviso (SQL_SUCCESS_WITH_INFO).  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa o **IDBDataSourceAdmin** interface, que é uma interface OLE DB opcional não foi implementada anteriormente, mas apenas o **CreateDataSource** método nesse opcional interface é implementada. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   O provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client retorna sinônimos nos conjuntos de linhas de esquema TABLES e TABLE_INFO, com TABLE_TYPE definido como SYNONYM.  
  
-   Retornar valores de tipo de dados **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, **udt**, ou outros tipos de objeto grande não podem ser retornados para as versões do cliente anteriores ao [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Caso queira usar esses tipos como valores de retorno, você deve usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
-   O MDAC permite que as seguintes instruções sejam executadas no início das transações manuais e implícitas, mas o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, não. Elas devem ser executadas no modo de confirmação automática.  
  
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
  
     Esse mapeamento de tipo afeta os valores retornados para metadados da coluna. Por exemplo, um **texto** coluna tem um tamanho máximo de 2.147.483.647, mas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC Native Client informa o tamanho máximo de **varchar (max)** colunas como SQL_SS_LENGTH_UNLIMITED e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]OLE DB native Client informa o tamanho máximo de **varchar (max)** colunas como 2.147.483.647 ou -1, dependendo da plataforma.  
  
-   O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client permite ambiguidade em cadeias de conexão (por exemplo, algumas palavras-chave podem ser especificadas mais de uma vez e outras, conflitantes, permitidas tendo a resolução baseada na posição ou na precedência) tendo em vista a compatibilidade com versões anteriores. Futuras versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client talvez não permitam ambiguidade em cadeias de conexão. Trata-se de uma boa prática, ao modificar aplicativos, usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para eliminar todas as dependências relacionadas à ambiguidade da cadeia de conexão.  
  
-   Caso você use uma chamada ODBC ou OLE DB para iniciar transações, existe uma diferença de comportamento entre o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o MDAC. As transações começarão imediatamente com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, e só começarão no MDAC depois do primeiro acesso ao banco de dados. Isso pode afetar o comportamento de procedimentos armazenados e lotes porque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requer@TRANCOUNT para ser o mesmo depois que um lote ou procedimento armazenado finaliza a execução como ele era quando o lote ou procedimento armazenado iniciado.  
  
-   Com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, ITransactionLocal::BeginTransaction fará com que uma transação seja iniciada imediatamente. Com o MDAC, o início da transação foi atrasado até que o aplicativo executasse uma instrução que exigia uma transação em modo de transação implícita. Para obter mais informações, confira [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
-   Você pode encontrar erros ao usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver Native Client com ODBC para acessar um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] computador do servidor que expõe novos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-tipos de dados específicos ou recursos. ODBC fornece uma implementação de ODBC genérica e subsequentemente não expõe a funcionalidade específica do fornecedor ou extensões. (O driver do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client é atualizado para oferecer suporte nativo aos recursos mais recentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].) Para solucionar esse problema, você pode voltar ao MDAC ou migrar para o SqlClient.  
  
 Tanto o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client quanto o MDAC oferecem suporte ao isolamento de transação de leitura confirmada usando controle de versão de linha, mas apenas o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte ao isolamento da transação de instantâneo. (Em termos de programação, isolamento de transação de leitura confirmada usando controle de versão de linha é igual à transação de leitura confirmada.).  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos com o SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
