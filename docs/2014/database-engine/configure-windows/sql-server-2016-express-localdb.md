---
title: SQL Server 2014 Express LocalDB | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- user instances
- LocalDB, described
- local database runtime
- file database
- LocalDB
ms.assetid: 5a641a46-7cfb-4d7b-a90d-6e4625719d74
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 224facf54b0cde09f97010be472e3cc28754e94b
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368298"
---
# <a name="sql-server-2014-express-localdb"></a>SQL Server 2014 Express LocalDB
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` é um modo de execução do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] destinado a desenvolvedores de programa. `LocalDB` instalação copia um conjunto mínimo de arquivos necessários para iniciar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Uma vez `LocalDB` é instalado, os desenvolvedores iniciam uma conexão usando uma cadeia de conexão especial. Na conexão, a infraestrutura necessária do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é criada e iniciada automaticamente, permitindo que o aplicativo use o banco de dados sem tarefas de configuração complexas ou demoradas. O Developer Tools pode fornecer aos desenvolvedores um [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que permite que eles gravem e testem o código [!INCLUDE[tsql](../../includes/tsql-md.md)] sem precisar gerenciar uma instância de servidor inteira do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uma instância do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] `LocalDB` é gerenciado por meio de `SqlLocalDB.exe` utilitário. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB` deve ser usado em vez do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] recurso de instância de usuário que foi preterido.  
  
## <a name="installing-localdb"></a>Instalando o LocalDB  
 O principal método de instalação `LocalDB` é usando o programa Sqllocaldb. `LocalDB` é uma opção na instalação de qualquer SKU do [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]. Selecione `LocalDB` sobre o **seleção de recursos** página durante a instalação do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Pode haver apenas uma instalação do `LocalDB` arquivos binários para cada principal [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] versão. Vários processos do [!INCLUDE[ssDE](../../includes/ssde-md.md)] podem ser iniciados e todos usarão os mesmos binários. Uma instância das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] começou como o `LocalDB` tem as mesmas limitações do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  
  
## <a name="description"></a>Descrição  
 O `LocalDB` programa de instalação usa o programa Sqllocaldb para instalar os arquivos necessários no computador. Uma vez instalado, `LocalDB` é uma instância de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] que pode criar e abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados. Os arquivos de banco de dados do sistema para o banco de dados são armazenados no caminho de AppData local dos usuários, que normalmente é oculto. Por exemplo **C:\Usuários\\<usuário\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\\**. Os arquivos de banco de dados do usuário são armazenados onde o usuário determina, normalmente em algum lugar da pasta **C:\Usuários\\<usuário\>\Documents\\**.  
  
 Para obter mais informações sobre como incluir `LocalDB` em um aplicativo, consulte a [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] documentação [visão geral de dados locais](https://msdn.microsoft.com/library/ms233817\(VS.110\).aspx), [passo a passo: Criando um banco de dados do SQL Server LocalDB](https://msdn.microsoft.com/library/ms233763\(VS.110\).aspx), e [passo a passo: Conectando a dados em um banco de dados do SQL Server LocalDB (Windows Forms)](https://msdn.microsoft.com/library/ms171890\(VS.110\).aspx).  
  
 Para obter mais informações sobre o `LocalDB` API, consulte [SQL Server Express LocalDB instância referência da API](https://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx) e [função LocalDBStartInstance](https://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx).  
  
 O utilitário SqlLocalDb pode criar novas instâncias de `LocalDB`, iniciar e interromper uma instância do `LocalDB`e inclui opções para ajudá-lo a gerenciar `LocalDB`.  Para obter mais informações sobre o utilitário SqlLocalDb, consulte [Utilitário SqlLocalDB](../../tools/sqllocaldb-utility.md).  
  
 O agrupamento de instância para `LocalDB` é definido como SQL_Latin1_General_CP1_CI_AS e não pode ser alterado. Normalmente há suporte para ordenações nos níveis de banco de dados, de coluna e de expressão. Os bancos de dados independentes seguem os metadados e as regras de ordenações tempdb definidas por [Ordenações de banco de dados independentes](../../relational-databases/databases/contained-database-collations.md).  
  
### <a name="restrictions"></a>Restrictions  
 `LocalDB` não pode ser um assinante de replicação de mesclagem.  
  
 `LocalDB` não oferece suporte a FILESTREAM.  
  
 `LocalDB` só permite filas locais para o Service Broker.  
  
 Uma instância de `LocalDB` pertencentes as contas internas, como NT AUTHORITY\SYSTEM pode ter problemas de capacidade de gerenciamento devido ao redirecionamento de sistema de arquivos do windows. Em vez disso, use uma conta normal do windows como o proprietário.  
  
### <a name="automatic-and-named-instances"></a>Instâncias automáticas e nomeadas  
 `LocalDB` dá suporte a dois tipos de instâncias: Instâncias automáticas e instâncias nomeadas.  
  
-   As instâncias automáticas do `LocalDB` são públicos. Elas são criadas e gerenciadas automaticamente para o usuário e podem ser usadas por qualquer aplicativo. Uma instância automática do `LocalDB` existe para todas as versões do `LocalDB` instalado no computador do usuário. As instâncias automáticas do `LocalDB` fornecem gerenciamento de instância contínuo. Não há necessidade de criar a instância; assim é o suficiente. Isso facilita a instalação e migração do aplicativo para um computador diferente. Se o computador de destino tiver a versão especificada do `LocalDB` instalada, a instância automática do `LocalDB` para essa versão também estará disponível no computador de destino. As instâncias automáticas do `LocalDB` têm um padrão especial para o nome da instância que pertence a um namespace reservado. Isso evita conflitos de nomes com instâncias nomeadas do `LocalDB`. O nome da instância automática é **MSSQLLocalDB**.  
  
-   Instâncias nomeadas do `LocalDB` são particulares. Elas pertencem a um único aplicativo, que é responsável por criar e gerenciar a instância. As instâncias nomeadas fornecem isolamento de outras instâncias e melhoram o desempenho reduzindo a contenção de recursos com outros usuários de banco de dados. Instâncias nomeadas devem ser criadas explicitamente pelo usuário através do `LocalDB` API de gerenciamento ou implicitamente por meio de App. config de arquivos para um aplicativo gerenciado (embora o aplicativo gerenciado também possa usar a API, se desejado). Cada instância nomeada do `LocalDB` tem um associado `LocalDB` versão que aponta para o conjunto respectivo de `LocalDB` binários. O nome da instância de um `LocalDB` é `sysname` dados de tipo e pode ter até 128 caracteres. (Isso difere das instâncias nomeadas normais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que limitam os nomes a nomes NetBIOS normais de 16 caracteres ASCII.) O nome de uma instância de `LocalDB` pode conter qualquer caractere Unicode legal em um nome de arquivo.  Uma instância nomeada que usa um nome de instância automático torna-se uma instância automática.  
  
 Usuários diferentes de um computador podem ter instâncias com o mesmo nome. Cada instância é um processo diferente executado como um usuário diferente.  
  
## <a name="shared-instances-of-localdb"></a>Instâncias compartilhadas do LocalDB  
 Para dar suporte a cenários onde vários usuários do computador precisam se conectar a uma única instância de `LocalDB`, `LocalDB` oferece suporte ao compartilhamento de instância. O proprietário de uma instância pode optar por permitir que os outros usuários do computador se conectem à sua instância. Instâncias automáticas e nomeadas do `LocalDB` podem ser compartilhados. Para compartilhar uma instância do `LocalDB`, o usuário seleciona um nome compartilhado (alias) para isso. Como o nome compartilhado fica visível para todos os usuários do computador, ele deve ser exclusivo no computador. O nome compartilhado de uma instância do `LocalDB` tem o mesmo formato que a instância nomeada do `LocalDB`.  
  
 Somente um administrador no computador pode criar uma instância compartilhada do `LocalDB`. Uma instância compartilhada do `LocalDB` pode ser descompartilhada por um administrador ou pelo proprietário da instância compartilhada do `LocalDB`. Para compartilhar e descompartilhar uma instância do `LocalDB`, use o `LocalDBShareInstance` e `LocalDBUnShareInstance` métodos do `LocalDB` API, ou o compartilhamento e descompartilhadas opções do utilitário SqlLocalDb.  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>Iniciando o LocalDB e conectando-se ao LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>Conectando-se à instância automática  
 A maneira mais fácil de usar `LocalDB` é conectar-se à instância automática pertencente ao usuário atual usando a cadeia de caracteres de conexão **"Server = (localdb) \MSSQLLocalDB;Integrated Security = true"**. Para se conectar a um banco de dados específico usando o nome do arquivo, conecte-se usando uma cadeia de conexão semelhante a **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"**.  
  
> [!NOTE]  
>  Na primeira vez que um usuário em um computador tenta se conectar a `LocalDB`, a instância automática deve ser criada e iniciada. A tempo adicional para a criação da instância pode causar a falha da tentativa de conexão com uma mensagem de tempo esgotado. Quando isso acontecer, espere alguns segundos para deixar o processo de criação terminar e conecte novamente.  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>Criando e conectando-se a instâncias nomeadas  
 Além da instância automática, `LocalDB` também o dá suporte a instâncias nomeadas. Use o programa de SqlLocalDB.exe para criar, iniciar e interromper uma instância nomeada do `LocalDB`. Para obter mais informações sobre o SqlLocalDB.exe, consulte [Utilitário SqlLocalDB](../../tools/sqllocaldb-utility.md).  
  
```ms-dos  
REM Create an instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1  
REM Start the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1  
REM Gather information about the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\120\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1  
```  
  
 A última linha acima, retorna informações semelhantes a estas:  
  
|||  
|-|-|  
|Nome|"LocalDBApp1"|  
|Versão|\<Current Version>|  
|Nome compartilhado|""|  
|Proprietário|“\<Your Windows User>”|  
|Criar automaticamente|Não|  
|Estado|executando|  
|Hora da última inicialização|\<Date and Time>|  
|Nome do pipe da instância|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  Se seu aplicativo usa uma versão do .NET anterior à 4.0.2 você deve se conectar diretamente ao pipe nomeado do `LocalDB`. O valor de nome de pipe de instância é o pipe nomeado que a instância do `LocalDB` está escutando. A parte do nome do pipe da instância após LOCALDB # mudará sempre que a instância do `LocalDB` é iniciado. Para se conectar à instância do `LocalDB` por meio [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], digite o nome do pipe da instância na **nome do servidor** caixa dos **se conectar ao [!INCLUDE[ssDE](../../includes/ssde-md.md)]**  caixa de diálogo. Em seu programa personalizado você pode estabelecer conexão com a instância do `LocalDB` usando uma cadeia de conexão semelhante a `SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>Conectando-se a uma instância compartilhada do LocalDB  
 Para se conectar a uma instância compartilhada do `LocalDB` adicione **.\\**  (ponto + barra invertida) à cadeia de conexão para fazer referência ao namespace reservado para instâncias compartilhadas. Por exemplo, para se conectar a uma instância compartilhada do `LocalDB` nomeado `AppData` usar uma cadeia de caracteres de conexão, como `(localdb)\.\AppData` como parte da cadeia de conexão. Um usuário se conectar a uma instância compartilhada do `LocalDB` que não possuem deve ter uma autenticação do Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon de autenticação.  
  
## <a name="troubleshooting"></a>Solução de problemas  
 Para obter informações sobre solução de problemas `LocalDB`, consulte [solução de problemas de SQL Server 2012 Express LocalDB](https://social.technet.microsoft.com/wiki/contents/articles/4609.aspx).  
  
## <a name="permissions"></a>Permissões  
 Uma instância do [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` é uma instância criada por um usuário para seu uso. Qualquer usuário no computador pode criar um banco de dados usando uma instância de `LocalDB`, armazenando arquivos sob o seu perfil de usuário e executar o processo sob suas credenciais. Por padrão, o acesso à instância do `LocalDB` é limitado a seu proprietário. Os dados contidos no `LocalDB` é protegido pelo acesso de sistema de arquivos para os arquivos de banco de dados. Se os arquivos de banco de dados do usuário são armazenados em um local compartilhado, o banco de dados pode ser aberto por qualquer pessoa com acesso de sistema de arquivos para esse local usando uma instância de `LocalDB` que eles possuem. Se os arquivos de banco de dados estiverem em um local protegido, como a pasta de dados de usuários, somente esse usuário e os administradores com acesso a essa pasta poderão abrir o banco de dados. O `LocalDB` arquivos só podem ser abertos por uma instância de `LocalDB` por vez.  
  
> [!NOTE]  
>  `LocalDB` sempre é executado sob o contexto de segurança de usuários; ou seja, `LocalDB` nunca é executado com credenciais do grupo de administradores locais. Isso significa que todos os banco de dados arquivos usados por um `LocalDB` instância deve estar acessível usando a conta do Windows do usuário proprietário, sem considerar a associação no grupo Administradores local.  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário SqlLocalDB](../../tools/sqllocaldb-utility.md)  
  
  
