---
title: SQL Server 2016 Express LocalDB | Microsoft Docs
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user instances
- LocalDB, described
- local database runtime
- file database
- LocalDB
ms.assetid: 5a641a46-7cfb-4d7b-a90d-6e4625719d74
caps.latest.revision: "42"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: d559c1f713a51a51a3b8279f585b0fa48d81ecba
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-2016-express-localdb"></a>SQL Server 2016 Express LocalDB
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > Para obter o conteúdo relacionado a versões anteriores do SQL Server, consulte [SQL Server 2014 Express LocalDB](https://msdn.microsoft.com/en-US/library/hh510202(SQL.120).aspx).

O **LocalDB** do Microsoft SQL Server 2016 Express é um recurso do [SQL Server Express](https://msdn.microsoft.com/library/ms144275(SQL.130).aspx) voltado para desenvolvedores. Ele está disponível no SQL Server 2016 Express with Advanced Services.  

 A instalação do**LocalDB** copia um conjunto mínimo de arquivos necessários para iniciar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Depois do LocalDB ser instalado, você poderá iniciar uma conexão usando uma cadeia de conexão especial. Ao conectar, a infraestrutura necessária do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é criada e iniciada automaticamente, permitindo que o aplicativo use o banco de dados sem tarefas de configuração complexas. O Developer Tools pode fornecer aos desenvolvedores um [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que permite que eles gravem e testem o código [!INCLUDE[tsql](../../includes/tsql-md.md)] sem precisar gerenciar uma instância de servidor inteira do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
 
 
 ## <a name="try-it-out"></a>Experimente! 
  
-   Para baixar e instalar o SQL Server 2016 Express, acesse **[Downloads do SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)**. LocalDB é um recurso selecionado durante a instalação e que está disponível durante o download da mídia. Se você baixar a mídia, escolha **Express Advanced** ou o pacote **LocalDB** . 
  
-   Tem uma conta do Azure?  Então, clique **[aqui](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** para executar uma máquina virtual com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] já instalado.  
  
## <a name="install-localdb"></a>Instalar o LocalDB  
 Instale o **LocalDB** por meio do assistente de instalação ou usando o programa SqlLocalDB.msi. O**LocalDB** é uma opção na instalação do [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]. 
 
Selecione **LocalDB** na página **Seleção de Recursos/Recursos Compartilhados** durante a instalação. Pode haver somente uma instalação dos arquivos binários do **LocalDB** para cada versão principal do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Vários processos do [!INCLUDE[ssDE](../../includes/ssde-md.md)] podem ser iniciados e todos usarão os mesmos binários. Uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] iniciada como o **LocalDB** tem as mesmas limitações do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  

 Uma instância do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] **LocalDB** é gerenciada com o utilitário **SqlLocalDB.exe** . [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] **LocalDB** deve ser usado no lugar do recurso de instância do usuário [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] que foi preterido. 
  
## <a name="description"></a>Description  
 O programa de instalação do **LocalDB** usa o programa SqlLocalDB.msi para instalar os arquivos necessários no computador. Uma vez instalado, o **LocalDB** torna-se uma instância do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] que pode criar e abrir bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os arquivos de banco de dados do sistema para o banco de dados são armazenados no caminho de AppData local dos usuários, que normalmente é oculto. Por exemplo **C:\Usuários\\<usuário\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\\**. Os arquivos de banco de dados do usuário são armazenados onde o usuário determina, normalmente em algum lugar da pasta **C:\Usuários\\<usuário\>\Documents\\**.  
  
 Para obter mais informações sobre como incluir o **LocalDB** em um aplicativo, consulte a documentação do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [Visão geral da arquitetura lógica](http://msdn.microsoft.com/library/ms233817\(VS.110\).aspx), [Passo a passo: criando um banco de dados LocalDB do SQL Server](http://msdn.microsoft.com/library/ms233763\(VS.110\).aspx) e [Passo a passo: conectando-se a dados no banco de dados LocalDB do SQL Server (Windows Forms)](http://msdn.microsoft.com/library/ms171890\(VS.110\).aspx).  
  
 Para obter mais informações sobre a API do **LocalDB** , consulte [Referência de API da instância LocalDB do SQL Server Express](http://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx) e [Função LocalDBStartInstance](http://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx).  
  
 O utilitário SqlLocalDb pode criar novas instâncias do **LocalDB**, iniciar e interromper uma instância do **LocalDB**, e contém opções para ajudar a gerenciar o **LocalDB**.  Para obter mais informações sobre o utilitário SqlLocalDb, consulte [Utilitário SqlLocalDB](../../tools/sqllocaldb-utility.md).  
  
 O agrupamento de instância para **LocalDB** é definido como SQL_Latin1_General_CP1_CI_AS e não pode ser alterado. Normalmente há suporte para agrupamentos nos níveis de banco de dados, de coluna e de expressão. Os bancos de dados independentes seguem os metadados e as regras de agrupamentos tempdb definidas por [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md).  
  
### <a name="restrictions"></a>Restrictions  
 O**LocalDB** não pode ser um assinante de replicação de mesclagem.  
  
 O**LocalDB** não dá suporte a FILESTREAM.  
  
 O**LocalDB** só permite filas locais para Service Broker.  
  
 Uma instância do **LocalDB** pertencente às contas internas, como NT AUTHORITY\SYSTEM, pode ter problemas de capacidade de gerenciamento devido ao redirecionamento do sistema de arquivos do Windows. Em vez disso, use uma conta normal do Windows como o proprietário.  
  
### <a name="automatic-and-named-instances"></a>Instâncias automáticas e nomeadas  
 O**LocalDB** oferece suporte a dois tipos de instâncias: instâncias automáticas e instâncias nomeadas.  
  
-   As instâncias automáticas do **LocalDB** são públicas. Elas são criadas e gerenciadas automaticamente para o usuário e podem ser usadas por qualquer aplicativo. Existe uma instância automática do **LocalDB** para cada versão do **LocalDB** instalada no computador do usuário. As instâncias automáticas do **LocalDB** fornecem gerenciamento de instância contínuo. Não há necessidade de criar a instância; assim é o suficiente. Isso facilita a instalação e migração do aplicativo para um computador diferente. Se o computador de destino tiver a versão especificada do **LocalDB** instalada, a instância automática do **LocalDB** para essa versão também estará disponível no computador de destino. As instâncias automáticas do **LocalDB** têm um padrão especial para o nome de instância que pertence a um namespace reservado. Isso evita conflitos de nomes com instâncias nomeadas do **LocalDB**. O nome da instância automática é **MSSQLLocalDB**.  
  
-   As instâncias nomeadas do **LocalDB** são privadas. Elas pertencem a um único aplicativo, que é responsável por criar e gerenciar a instância. As instâncias nomeadas fornecem isolamento de outras instâncias e melhoram o desempenho reduzindo a contenção de recursos com outros usuários de banco de dados. As instâncias nomeadas devem ser criadas explicitamente pelo usuário por meio da API de gerenciamento do **LocalDB** ou implicitamente por meio do arquivo app.config para um aplicativo gerenciado (embora o aplicativo gerenciado também possa usar a API, se desejado). Cada instância nomeada do **LocalDB** tem uma versão associada do **LocalDB** que aponta para o conjunto respectivo de binários do **LocalDB** . O nome da instância do **LocalDB** é o tipo de dados **sysname** e pode ter até 128 caracteres. (Isso difere das instâncias nomeadas normais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que limitam os nomes a nomes NetBIOS normais de 16 caracteres ASCII.) O nome de uma instância do **LocalDB** pode conter qualquer caractere Unicode legal em um nome de arquivo.  Uma instância nomeada que usa um nome de instância automático torna-se uma instância automática.  
  
 Usuários diferentes de um computador podem ter instâncias com o mesmo nome. Cada instância é um processo diferente executado como um usuário diferente.  
  
## <a name="shared-instances-of-localdb"></a>Instâncias compartilhadas do LocalDB  
 Para oferecer suporte a cenários onde vários usuários do computador precisam se conectar a uma única instância do **LocalDB**, o **LocalDB** oferece suporte ao compartilhamento de instâncias. O proprietário de uma instância pode optar por permitir que os outros usuários do computador se conectem à sua instância. As instâncias automáticas e nomeadas do **LocalDB** podem ser compartilhadas. Para compartilhar uma instância do **LocalDB** , o usuário seleciona um nome compartilhado (alias) para isso. Como o nome compartilhado fica visível para todos os usuários do computador, ele deve ser exclusivo no computador. O nome compartilhado de uma instância do **LocalDB** tem o mesmo formato da instância nomeada do **LocalDB**.  
  
 Somente um administrador no computador pode criar uma instância compartilhada do **LocalDB**. Uma instância compartilhada do **LocalDB** pode ser descompartilhada por um administrador ou pelo proprietário da instância compartilhada do **LocalDB**. Para compartilhar e descompartilhar uma instância do **LocalDB**, use os métodos `LocalDBShareInstance` e `LocalDBUnShareInstance` da API do **LocalDB** ou as opções de compartilhamento e descompartilhamento do utilitário SqlLocalDb.  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>Iniciando o LocalDB e conectando-se ao LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>Conectando-se à instância automática  
 A maneira mais fácil de usar o **LocalDB** é conectar-se à instância automática pertencente ao usuário atual usando a cadeia de conexão **"Server=(localdb)\MSSQLLocalDB;Integrated Security=true"**. Para se conectar a um banco de dados específico usando o nome do arquivo, conecte-se usando uma cadeia de conexão semelhante a **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"**.  
  
> [!NOTE]  
>  A primeira vez que o usuário de um computador tenta conectar-se ao **LocalDB**, a instância automática deve ser criada e iniciada. A tempo adicional para a criação da instância pode causar a falha da tentativa de conexão com uma mensagem de tempo esgotado. Quando isso acontecer, espere alguns segundos para deixar o processo de criação terminar e conecte novamente.  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>Criando e conectando-se a instâncias nomeadas  
 Além da instância automática, o **LocalDB** também oferece suporte a instâncias nomeadas. Use o programa SqlLocalDB.exe para criar, iniciar e interromper uma instância nomeada do **LocalDB**. Para obter mais informações sobre o SqlLocalDB.exe, consulte [Utilitário SqlLocalDB](../../tools/sqllocaldb-utility.md).  
  
```ms-dos  
REM Create an instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" create LocalDBApp1  
REM Start the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" start LocalDBApp1  
REM Gather information about the instance of LocalDB  
"C:\Program Files\Microsoft SQL Server\130\Tools\Binn\SqlLocalDB.exe" info LocalDBApp1  
```  
  
 A última linha acima, retorna informações semelhantes a estas:  
  
|||  
|-|-|  
|Nome|"LocalDBApp1"|  
|Versão|\<Current Version>|  
|Nome compartilhado|""|  
|Proprietário|“\<Your Windows User>”|  
|Criar automaticamente|não|  
|Estado|executando|  
|Hora da última inicialização|\<Date and Time>|  
|Nome do pipe da instância|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  Se o aplicativo usa uma versão do .NET anterior à 4.0.2, conecte-se diretamente ao pipe nomeado do **LocalDB**. O valor do nome do pipe da Instância é o pipe nomeado que a instância do **LocalDB** está ouvindo. A parte do nome do pipe da instância após LOCALDB# mudará sempre que a instância do **LocalDB** for iniciada. Para conectar-se à instância do **LocalDB** usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], digite o nome do pipe da instância na caixa **Nome do servidor** da caixa de diálogo **Conectar-se a [!INCLUDE[ssDE](../../includes/ssde-md.md)]**. Em seu programa personalizado, você pode estabelecer uma conexão com a instância do **LocalDB** usando uma cadeia de conexão semelhante a `SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>Conectando-se a uma instância compartilhada do LocalDB  
 Para conectar-se a uma instância compartilhada do **LocalDB** adicione **.\\** (ponto + barra invertida) à cadeia de conexão para fazer referência ao namespace reservado para instâncias compartilhadas. Por exemplo, para conectar-se a uma instância compartilhada do **LocalDB** denominada `AppData` , use uma cadeia de conexão como `(localdb)\.\AppData` como parte da cadeia de conexão. Um usuário que se conecta a uma instância compartilhada do **LocalDB** que não pertence a ele deve ter uma Autenticação do Windows ou um logon de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="troubleshooting"></a>Solução de problemas  
 Para obter informações sobre como solucionar problemas do **LocalDB**, consulte [Solucionando problemas do SQL Server 2012 Express LocalDB](http://social.technet.microsoft.com/wiki/contents/articles/4609.aspx).  
  
## <a name="permissions"></a>Permissões  
 Uma instância do [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)]**LocalDB** é uma instância criada por um usuário para o seu próprio uso. Qualquer usuário no computador pode criar um banco de dados usando uma instância do **LocalDB**, armazenando arquivos sob o seu perfil do usuário e executando o processo sob suas credenciais. Por padrão, o acesso para a instância de **LocalDB** é limitado a seu proprietário. Os dados contidos no **LocalDB** são protegidos pelo acesso de sistema de arquivos aos arquivos de banco de dados. Se os arquivos de banco de dados do usuário estiverem armazenados em um local compartilhado, o banco de dados poderá ser aberto por qualquer pessoa com acesso de sistema de arquivos ao local, usando uma instância de **LocalDB** de sua propriedade. Se os arquivos de banco de dados estiverem em um local protegido, como a pasta de dados de usuários, somente esse usuário e os administradores com acesso a essa pasta poderão abrir o banco de dados. Os arquivos do **LocalDB** somente podem ser abertos por uma instância do **LocalDB** de cada vez.  
  
> [!NOTE]  
>  O**LocalDB** sempre é executado sob o contexto de segurança de usuários; ou seja, o **LocalDB** nunca é executado com credenciais do grupo de Administradores local. Isto significa que todos os arquivos de banco de dados usados por uma instância do **LocalDB** devem estar acessíveis usando a conta de Windows do usuário proprietário, sem considerar a associação no grupo de Administradores local.  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário SqlLocalDB](../../tools/sqllocaldb-utility.md)  
  
  
