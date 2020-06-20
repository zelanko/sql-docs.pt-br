---
title: SQL Server do 2014 Express LocalDB | Microsoft Docs
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
ms.openlocfilehash: f3c43604604580c5924be4daf4d473407564d247
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934866"
---
# <a name="sql-server-2014-express-localdb"></a>SQL Server 2014 Express LocalDB
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` é um modo de execução [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] destinado a desenvolvedores de programas. `LocalDB`a instalação copia um conjunto mínimo de arquivos necessários para iniciar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Uma vez `LocalDB` instalado, os desenvolvedores iniciam uma conexão usando uma cadeia de conexão especial. Na conexão, a infraestrutura necessária do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é criada e iniciada automaticamente, permitindo que o aplicativo use o banco de dados sem tarefas de configuração complexas ou demoradas. O Developer Tools pode fornecer aos desenvolvedores um [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que permite que eles gravem e testem o código [!INCLUDE[tsql](../../includes/tsql-md.md)] sem precisar gerenciar uma instância de servidor inteira do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Uma instância do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] `LocalDB` é gerenciada usando o `SqlLocalDB.exe` Utilitário do. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]`LocalDB`deve ser usado no lugar do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] recurso de instância de usuário que é preterido.  
  
## <a name="installing-localdb"></a>Instalando o LocalDB  
 O principal método de instalação do `LocalDB` é usar o programa SqlLocalDB.msi. `LocalDB`é uma opção ao instalar qualquer SKU do [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] . Selecione `LocalDB` na página **seleção de recursos** durante a instalação do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] . Pode haver apenas uma instalação dos `LocalDB` arquivos binários para cada versão principal [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Vários processos do [!INCLUDE[ssDE](../../includes/ssde-md.md)] podem ser iniciados e todos usarão os mesmos binários. Uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] iniciada como `LocalDB` tem as mesmas limitações de[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]  
  
## <a name="description"></a>Descrição  
 O `LocalDB` programa de instalação usa o programa SqlLocalDB.msi para instalar os arquivos necessários no computador. Uma vez instalado, `LocalDB` é uma instância do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] que pode criar e abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados. Os arquivos de banco de dados do sistema para o banco de dados são armazenados no caminho de AppData local dos usuários, que normalmente é oculto. Por exemplo **C:\Usuários\\<usuário\>\AppData\Local\Microsoft\Microsoft SQL Server Local DB\Instances\LocalDBApp1\\**. Os arquivos de banco de dados do usuário são armazenados onde o usuário determina, normalmente em algum lugar da pasta **C:\Usuários\\<usuário\>\Documents\\**.  
  
 Para obter mais informações sobre como incluir `LocalDB` em um aplicativo, consulte a [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] documentação [visão geral dos dados locais](https://msdn.microsoft.com/library/ms233817\(VS.110\).aspx), [passo a passos: Criando um SQL Server banco](https://msdn.microsoft.com/library/ms233763\(VS.110\).aspx)de dado do LocalDB e [passo a passos: conectando-se a dados em um banco de SQL Server do LocalDB (Windows Forms)](https://msdn.microsoft.com/library/ms171890\(VS.110\).aspx).  
  
 Para obter mais informações sobre a `LocalDB` API, consulte [referência de API da instância LocalDB SQL Server Express](https://msdn.microsoft.com/library/hh234692\(SQL.110\).aspx) e [função LocalDBStartInstance](https://msdn.microsoft.com/library/hh217143\(SQL.110\).aspx).  
  
 O utilitário SqlLocalDb pode criar novas instâncias do `LocalDB` , iniciar e parar uma instância do `LocalDB` e inclui opções para ajudá-lo a gerenciar o `LocalDB` .  Para obter mais informações sobre o utilitário SqlLocalDb, consulte [Utilitário SqlLocalDB](../../tools/sqllocaldb-utility.md).  
  
 O agrupamento de instância para `LocalDB` é definido como SQL_Latin1_General_CP1_CI_AS e não pode ser alterado. Normalmente há suporte para ordenações nos níveis de banco de dados, de coluna e de expressão. Os bancos de dados independentes seguem os metadados e as regras de ordenações tempdb definidas por [Ordenações de banco de dados independentes](../../relational-databases/databases/contained-database-collations.md).  
  
### <a name="restrictions"></a>Restrições  
 `LocalDB`Não pode ser um assinante de replicação de mesclagem.  
  
 `LocalDB`não oferece suporte a FILESTREAM.  
  
 `LocalDB`permite apenas filas locais para Service Broker.  
  
 Uma instância de `LocalDB` propriedade das contas internas, como NT AUTHORITY\SYSTEM, pode ter problemas de gerenciamento devido ao redirecionamento do sistema de arquivos do Windows; Em vez disso, use uma conta normal do Windows como o proprietário.  
  
### <a name="automatic-and-named-instances"></a>Instâncias automáticas e nomeadas  
 `LocalDB`dá suporte a dois tipos de instâncias: instâncias automáticas e instâncias nomeadas.  
  
-   As instâncias automáticas do `LocalDB` são públicas. Elas são criadas e gerenciadas automaticamente para o usuário e podem ser usadas por qualquer aplicativo. Uma instância automática do `LocalDB` existe para cada versão do `LocalDB` instalada no computador do usuário. Instâncias automáticas do `LocalDB` fornecem gerenciamento de instância contínuo. Não há necessidade de criar a instância; assim é o suficiente. Isso facilita a instalação e migração do aplicativo para um computador diferente. Se o computador de destino tiver a versão especificada do `LocalDB` instalada, a instância automática do `LocalDB` para essa versão também estará disponível no computador de destino. As instâncias automáticas do `LocalDB` têm um padrão especial para o nome da instância que pertence a um namespace reservado. Isso impede conflitos de nome com instâncias nomeadas do `LocalDB` . O nome da instância automática é **MSSQLLocalDB**.  
  
-   As instâncias nomeadas do `LocalDB` são privadas. Elas pertencem a um único aplicativo, que é responsável por criar e gerenciar a instância. As instâncias nomeadas fornecem isolamento de outras instâncias e melhoram o desempenho reduzindo a contenção de recursos com outros usuários de banco de dados. As instâncias nomeadas devem ser criadas explicitamente pelo usuário por meio da `LocalDB` API de gerenciamento ou implicitamente por meio do arquivo de app.config para um aplicativo gerenciado (embora o aplicativo gerenciado também possa usar a API, se desejado). Cada instância nomeada do `LocalDB` tem uma `LocalDB` versão associada que aponta para o respectivo conjunto de `LocalDB` binários. O nome da instância de a `LocalDB` é um `sysname` tipo de dados e pode ter até 128 caracteres. (Isso difere de instâncias nomeadas regulares do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que limitam os nomes a nomes NetBIOS regulares de 16 caracteres ASCII.) O nome de uma instância do `LocalDB` pode conter qualquer caractere Unicode que seja válido em um nome de arquivo.  Uma instância nomeada que usa um nome de instância automático torna-se uma instância automática.  
  
 Usuários diferentes de um computador podem ter instâncias com o mesmo nome. Cada instância é um processo diferente executado como um usuário diferente.  
  
## <a name="shared-instances-of-localdb"></a>Instâncias compartilhadas do LocalDB  
 Para oferecer suporte a cenários em que vários usuários do computador precisam se conectar a uma única instância do `LocalDB` , o `LocalDB` oferece suporte ao compartilhamento de instância. O proprietário de uma instância pode optar por permitir que os outros usuários do computador se conectem à sua instância. As instâncias automáticas e nomeadas do `LocalDB` podem ser compartilhadas. Para compartilhar uma instância do `LocalDB`, o usuário seleciona um nome compartilhado (alias) para isso. Como o nome compartilhado fica visível para todos os usuários do computador, ele deve ser exclusivo no computador. O nome compartilhado de uma instância do `LocalDB` tem o mesmo formato da instância nomeada do `LocalDB` .  
  
 Somente um administrador no computador pode criar uma instância compartilhada do `LocalDB` . Uma instância compartilhada do `LocalDB` pode ser descompartilhada por um administrador ou pelo proprietário da instância compartilhada do `LocalDB` . Para compartilhar e descompartilhar uma instância do `LocalDB` , use os `LocalDBShareInstance` métodos e `LocalDBUnShareInstance` da `LocalDB` API, ou as opções compartilhamento e não compartilhado do utilitário SqlLocalDb.  
  
## <a name="starting-localdb-and-connecting-to-localdb"></a>Iniciando o LocalDB e conectando-se ao LocalDB  
  
### <a name="connecting-to-the-automatic-instance"></a>Conectando-se à instância automática  
 A maneira mais fácil de usar `LocalDB` é conectar-se à instância automática de Propriedade do usuário atual usando a cadeia de conexão **"Server = (LocalDB) \MSSQLLocalDB; Integrated Security = true"**. Para se conectar a um banco de dados específico usando o nome do arquivo, conecte-se usando uma cadeia de conexão semelhante a **"Server=(LocalDB)\MSSQLLocalDB; Integrated Security=true ;AttachDbFileName=D:\Data\MyDB1.mdf"**.  
  
> [!NOTE]  
>  Na primeira vez que um usuário em um computador tenta se conectar `LocalDB` , a instância automática deve ser criada e iniciada. O tempo adicional para a criação da instância pode causar falha durante a tentativa de conexão e exibir uma mensagem de tempo esgotado. Quando isso acontecer, espere alguns segundos para deixar o processo de criação terminar e conecte novamente.  
  
### <a name="creating-and-connecting-to-a-named-instances"></a>Criando e conectando-se a instâncias nomeadas  
 Além da instância automática, o `LocalDB` também dá suporte a instâncias nomeadas. Use o programa SqlLocalDB.exe para criar, iniciar e parar uma instância nomeada do `LocalDB` . Para obter mais informações sobre o SqlLocalDB.exe, consulte [Utilitário SqlLocalDB](../../tools/sqllocaldb-utility.md).  
  
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
|Proprietário|"\<Your Windows User>"|  
|Criar automaticamente|Não|  
|Estado|executando|  
|Hora da última inicialização|\<Date and Time>|  
|Nome do pipe da instância|np:\\\\.\pipe\LOCALDB#F365A78E\tsql\query|  
  
> [!NOTE]  
>  Se seu aplicativo usa uma versão do .NET antes de 4.0.2, você deve se conectar diretamente ao pipe nomeado do `LocalDB` . O valor do nome do pipe da instância é o pipe nomeado em que a instância do `LocalDB` está escutando. A parte do nome do pipe da instância após LOCALDB # será alterada sempre que a instância do `LocalDB` for iniciada. Para se conectar à instância do `LocalDB` usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , digite o nome do pipe da instância na caixa **nome do servidor** da caixa de diálogo **conectar-se a [!INCLUDE[ssDE](../../includes/ssde-md.md)] ** . Em seu programa personalizado, você pode estabelecer conexão com a instância do `LocalDB` usando uma cadeia de conexão semelhante a`SqlConnection conn = new SqlConnection(@"Server=np:\\.\pipe\LOCALDB#F365A78E\tsql\query");`  
  
### <a name="connecting-to-a-shared-instance-of-localdb"></a>Conectando-se a uma instância compartilhada do LocalDB  
 Para se conectar a uma instância compartilhada `LocalDB` de **Add \\ .** (ponto + barra invertida) à cadeia de conexão para referenciar o namespace reservado para instâncias compartilhadas. Por exemplo, para se conectar a uma instância compartilhada do `LocalDB` denominada, `AppData` use uma cadeia de conexão como `(localdb)\.\AppData` parte da cadeia de conexão. Um usuário que se conecta a uma instância compartilhada do `LocalDB` que não possui deve ter um logon de autenticação ou autenticação do Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="troubleshooting"></a>Solução de problemas  
 Para obter informações sobre como solucionar problemas `LocalDB` , consulte [solução de problemas SQL Server 2012 Express LocalDB](https://social.technet.microsoft.com/wiki/contents/articles/4609.aspx).  
  
## <a name="permissions"></a>Permissões  
 Uma instância do [!INCLUDE[ssExpCurrent](../../includes/ssexpcurrent-md.md)] `LocalDB` é uma instância criada por um usuário para seu uso. Qualquer usuário no computador pode criar um banco de dados usando uma instância do `LocalDB` , armazenando arquivos em seu perfil de usuário e executando o processo sob suas credenciais. Por padrão, o acesso à instância do `LocalDB` é limitado ao seu proprietário. Os dados contidos no `LocalDB` são protegidos pelo acesso do sistema de arquivos aos arquivos de banco de dado. Se os arquivos de banco de dados do usuário forem armazenados em um local compartilhado, o banco de dados poderá ser aberto por qualquer pessoa com acesso ao sistema de arquivos para esse local usando uma instância do `LocalDB` que ele possui. Se os arquivos de banco de dados estiverem em um local protegido, como a pasta de dados de usuários, somente esse usuário e os administradores com acesso a essa pasta poderão abrir o banco de dados. Os `LocalDB` arquivos só podem ser abertos por uma instância do `LocalDB` por vez.  
  
> [!NOTE]  
>  `LocalDB`sempre é executado sob o contexto de segurança dos usuários; ou seja, `LocalDB` nunca é executado com credenciais do grupo do administrador local. Isso significa que todos os arquivos de banco de dados usados por uma `LocalDB` instância devem ser acessíveis usando a conta do Windows do usuário proprietário, sem considerar a associação no grupo local de administradores.  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário SqlLocalDB](../../tools/sqllocaldb-utility.md)  
  
  
