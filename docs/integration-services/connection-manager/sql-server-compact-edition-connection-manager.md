---
title: "SQL Server Compact Edition Conexão Manager | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sqlmobileconnection.connection.f1
- sql13.dts.designer.sqlmobileconnection.all.f1
helpviewer_keywords:
- SQL Server Compact, connection manager
- connections [Integration Services], SQL Server Compact
- connection managers [Integration Services], SQL Server Compact
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: 6b3f09dad60239f595aaae0cac0162283d84430d
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="sql-server-compact-edition-connection-manager"></a>Gerenciador de Conexões do SQL Server Compact Edition
  Um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact permite que um pacote se conecte a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact. O destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui usa esse gerenciador de conexões para carregar dados em uma tabela no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
> [!NOTE]  
>  Em um computador de 64 bits, você deve executar pacotes que se conectam a fontes de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact no modo de 32 bits. O provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa para se conectar a fontes de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, só está disponível na versão de 32 bits.  
  
## <a name="configuration-the-sql-server-compact-edition-connection-manager"></a>Configuração do gerenciador de conexões do SQL Server Compact Edition  
 Quando você adiciona um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que resolverá uma conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact em tempo de execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção de **Conexões** no pacote.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **SQLMOBILE**.  
  
 Você pode configurar um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact das seguintes maneiras:  
  
-   Forneça uma cadeia de conexão que especifique o local do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
-   Forneça uma senha para um banco de dados protegido por senha.  
  
-   Especifique o servidor no qual o banco de dados está armazenado.  
  
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="sql-server-compact-edition-connection-manager-editor-connection-page"></a>Editor do Gerenciador de Conexões do SQL Server Compact Edition (página de Conexão)
  Use a caixa de diálogo **Gerenciador de Conexões do SQL Server Compact Edition** para especificar as propriedades de conexão com um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 Para saber mais sobre o Gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Edition, consulte [Gerenciador de conexões do SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Digite o caminho e o nome do arquivo do banco de dados**  
 Digite o caminho e o nome do arquivo para o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Procurar**  
 Localize o arquivo de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact desejado usando a caixa de diálogo **Selecionar banco de dados do SQL Server Compact Edition** .  
  
 **Digite a senha do banco de dados**  
 Digite a senha para o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
## <a name="sql-server-compact-edition-connection-manager-editor-all-page"></a>Editor do Gerenciador de Conexões do SQL Server Compact Edition (Página Tudo)
  Use a caixa de diálogo **Gerenciador de Conexões do SQL Server Compact Edition** para especificar as propriedades de conexão com um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 Para saber mais sobre o Gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Edition, consulte [Gerenciador de conexões do SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Limite de AutoShrink**  
 Especifique a quantidade de espaço livre, em percentual, que será permitido no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact antes que o processo de redução automática seja executado.  
  
 **Escalonamento de Bloqueio Padrão**  
 Especifique o número de bloqueios de banco de dados que o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact adquire antes de tentar escalonar bloqueios.  
  
 **Tempos Limite de Bloqueio Padrão**  
 Especifique o intervalo padrão, em milissegundos, que uma transação esperará por um bloqueio.  
  
 **Intervalo de Liberação**  
 Especifique o intervalo, em segundos, entre transações confirmadas para liberar os dados para o disco.  
  
 **Identificador de Localidade**  
 Especifique a LCID (Identificação de Localidade) no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Tamanho Máximo do Buffer**  
 Especifique a quantidade máxima de memória, em quilobytes, que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact usa antes de liberar os dados para o disco.  
  
 **Tamanho Máximo do Banco de Dados**  
 Especifique o tamanho máximo, em megabytes, do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Modo**  
 Especifique o modo de arquivo no qual abrir o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact. O valor padrão dessa propriedade é **Leitura Gravação**.  
  
 A opção Modo tem quatro valores, como descrito na tabela seguinte.  
  
|Value|Description|  
|-----------|-----------------|  
|**Somente Leitura**|Especifica acesso somente de leitura ao banco de dados.|  
|**Leitura Gravação**|Especifica a permissão de leitura e gravação ao banco de dados.|  
|**Exclusive**|Especifica o acesso exclusivo ao banco de dados.|  
|**Shared Read**|Especifica que outros usuários podem ler de banco de dados ao mesmo tempo.|  
  
 **Informações de Persistência de Segurança**  
 Especifique se as informações de segurança são retornadas como parte da cadeia de conexão. O valor padrão dessa opção é **False**.  
  
 **Diretório de Arquivo Temporário**  
 Especifique o local do arquivo de banco de dados temporário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Fonte de dados**  
 Especifique o nome do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Senha**  
 Digite a senha para o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  

