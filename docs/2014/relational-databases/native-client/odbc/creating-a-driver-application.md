---
title: Criando um aplicativo de driver ODBC SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, architecture
- SQL Server Native Client ODBC driver, creating applications
- ODBC function calls
- ODBC, header files
- ODBC applications
- ODBC applications, creating
- SQL Server Native Client ODBC driver, extensions
- applications [SQL Server Native Client]
- SQL Server Native Client ODBC driver, ODBC architecture
- extensions [ODBC]
- ODBC, driver extensions
- function calls [ODBC]
ms.assetid: c83c36e2-734e-4960-bc7e-92235910bc6f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db71e2ca03cbefdccf0bdf879fdb43d775125064
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63205269"
---
# <a name="creating-a-sql-server-native-client-odbc-driver-application"></a>Criando um aplicativo de driver ODBC do SQL Server Native Client
  A arquitetura ODBC tem quatro componentes que executam as funções a seguir.  
  
|Componente|Função|  
|---------------|--------------|  
|Aplicativo|Chama funções ODBC para se comunicar com uma fonte de dados ODBC, envia instruções SQL e processa os conjuntos de resultados.|  
|Gerenciador de Driver|Gerencia a comunicação entre um aplicativo e todos os drivers ODBC usados por ele.|  
|Driver|Processa todas as chamadas de funções ODBC do aplicativo, conecta-se a uma fonte de dados, passa instruções SQL do aplicativo para a fonte de dados e retorna os resultados para o aplicativo. Se necessário, o driver converte SQL ODBC do aplicativo em SQL nativo usado pela fonte de dados.|  
|Fonte de dados|Contém todas as informações necessárias a um driver para acessar uma instância específica de dados em um DBMS.|  
  
 Um aplicativo que usa o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client para se comunicar com uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância do executa as seguintes tarefas:  
  
-   Conecta-se com uma fonte de dados  
  
-   Envia instruções SQL para a fonte de dados  
  
-   Processa os resultados das instruções da fonte de dados  
  
-   Processa erros e mensagens  
  
-   Finaliza a conexão com a fonte de dados  
  
 Um aplicativo mais complexo escrito para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client também pode executar as seguintes tarefas:  
  
-   Usar cursores para controlar o local em um conjunto de resultados  
  
-   Solicitar operações de confirmação ou reversão para o controle de transações  
  
-   Executar transações distribuídas que envolvem dois ou mais servidores  
  
-   Executar procedimentos armazenados no servidor remoto  
  
-   Chamar funções de catálogo para perguntar sobre os atributos de um conjunto de resultados  
  
-   Executar operações de cópia em massa  
  
-   Gerenciar operações de dados grandes (**varchar (max)**, **nvarchar (max)** e **varbinary (max)** )  
  
-   Usar lógica de reconexão para facilitar o failover quando o espelhamento de banco de dados é configurado  
  
-   Registrar dados de desempenho e consultas de execução demorada  
  
 Para fazer chamadas de função ODBC, um aplicativo C ou C++ deve incluir os arquivos de cabeçalhos sql.h, sqlext.h e sqltypes.h. Para fazer chamadas às funções de API do instalador ODBC, um aplicativo deve incluir o arquivo de cabeçalho odbcinst.h. Um aplicativo ODBC Unicode deve incluir o arquivo de cabeçalho sqlucode.h. Os aplicativos ODBC devem ser vinculados ao arquivo odbc32.lib. Os aplicativos ODBC que chamam as funções de API do instalador ODBC devem ser vinculados ao arquivo odbccp32.lib. Esses arquivos são incluídos no SDK da Plataforma Windows.  
  
 Muitos drivers ODBC, incluindo o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client, oferecem extensões ODBC específicas do driver. Para aproveitar as extensões [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] específicas do driver ODBC do Native Client, um aplicativo deve incluir o arquivo de cabeçalho sqlncli. h. Esse arquivo de cabeçalho contém:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Atributos de conexão específicos do driver ODBC do Native Client.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Atributos de instrução específicos do driver ODBC do Native Client.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Atributos de coluna específicos do driver ODBC do Native Client.  
  
-   Tipos de dados específicos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Tipos de dados definidos pelo usuário específicos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Tipos específicos de [SQLGetInfo](../../native-client-odbc-api/sqlgetinfo.md) do driver ODBC do Native Client.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Campos de diagnóstico de driver ODBC do Native Client.  
  
-   Códigos de função dinâmica de diagnóstico específicos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Definições de tipos C/C++ para tipos de dados C nativos específicos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (retornados quando as colunas são associadas ao tipo de dados C, SQL_C_BINARY).  
  
-   Definição de tipo para a estrutura de dados de SQLPERF.  
  
-   Macros e protótipos de cópia em massa para oferecer suporte ao uso de APIs de cópia em massa através de uma conexão ODBC.  
  
-   Chame as funções de API de metadados de consulta distribuída para listas de servidores vinculados e seus catálogos.  
  
 Qualquer aplicativo ODBC C ou C++ que usa o recurso de cópia em massa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do driver ODBC do Native Client deve ser vinculado ao arquivo sqlncli11. lib. Aplicativos que chamam as funções de API de metadados de consulta distribuída também devem ser vinculados ao sqlncli11.lib. Os arquivos sqlncli. h e sqlncli11. lib são distribuídos como parte das ferramentas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do desenvolvedor. Os diretórios Include e Lib do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devem estar nos caminhos INCLUDE e LIB do compilador conforme o exemplo a seguir:  
  
```  
LIB=c:\Program Files\Microsoft Data Access SDK 2.8\Libs\x86\lib;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Lib;  
INCLUDE=c:\Program Files\Microsoft Data Access SDK 2.8\inc;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Include;  
```  
  
 Uma decisão de design que deve ser tomada no início do processo de criação de um aplicativo é se ele precisa ter várias chamadas ODBC pendentes ao mesmo tempo. Há dois métodos de suporte a várias chamadas ODBC simultâneas, que são descritos nos próximos tópicos desta seção. Para obter mais informações, consulte a [referência do programador de ODBC](https://go.microsoft.com/fwlink/?LinkId=45250).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Modo assíncrono e SQLCancel](../../native-client-odbc-api/sqlcancel.md)  
  
-   [Aplicativos multi-threaded](creating-a-driver-application-multithreaded-applications.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
