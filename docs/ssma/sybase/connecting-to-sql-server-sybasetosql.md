---
title: Conectando ao SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connecting to SQL Server
ms.assetid: dd368a1a-45b0-40e9-b4d3-5cdb48c26606
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 64d7dd2cf9ac9a0a83e35a8d6a0e4a7abc81eaff
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34778682"
---
# <a name="connecting-to-sql-server-sybasetosql"></a>Conectando ao SQL Server (SybaseToSQL)
Para migrar bancos de dados do Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você deve se conectar a qualquer uma das instâncias de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Quando você se conectar, o SSMA obtém metadados sobre todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e exibe os metadados de banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados. O SSMA armazena informações sobre qual instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está conectado, mas não armazena as senhas.  
  
Sua conexão ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve reconectar para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se você quiser uma conexão ativa com o servidor. Você pode trabalhar offline até que você carregar objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e migrar dados.  
  
Metadados sobre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] não será sincronizado automaticamente. Em vez disso, se você quiser atualizar os metadados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados, você deve atualizar manualmente o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadados, conforme descrito no "Sincronizando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadados" seção mais adiante neste tópico.  
  
## <a name="required-sql-server-permissions"></a>Permissões de servidor necessários do SQL  
A conta que é usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] requer permissões diferentes dependendo de ações que são executadas por essa conta.  
  
-   Para converter objetos ASE [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxe, para atualizar os metadados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], ou para salvar a sintaxe convertido em scripts, a conta deve ter permissão para fazer logon instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Ao carregar objetos do banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o requisito mínimo de permissão é a associação de **db_owner** função de banco de dados no banco de dados de destino.  
  
-   Para migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], a conta deve ser um membro do **sysadmin** função de servidor. Isso é necessário para executar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] pacotes de migração de dados do agente.  
  
-   Para executar o código gerado pelo SSMA, a conta deve ter **Execute** permissões para todas as funções definidas pelo usuário no **ssma_syb** esquema do **sysdb** banco de dados. Essas funções fornecem funcionalidade equivalente ASE de funções do sistema e são usadas por objetos convertidos.  
  
Se a conta que é usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é executar a migração de todas as tarefas, a conta deve ser um membro do **sysadmin** função de servidor.  
  
## <a name="establishing-a-sql-server-connection"></a>Estabelecer uma Conexão de servidor SQL  
Antes de converter objetos de banco de dados ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxe, você deve estabelecer uma conexão com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] onde você deseja migrar o ASE ou bancos de dados.  
  
Quando você define as propriedades de conexão, você também especificar o banco de dados onde objetos e dados serão migrados. Você pode personalizar esse mapeamento no nível do esquema ASE depois que você se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter mais informações, consulte [mapeamento Sybase ASE esquemas para esquemas SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
> [!IMPORTANT]  
> Antes de tentar se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], verifique se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está em execução e pode aceitar conexões.  
  
**Para se conectar ao SQL Server**  
  
1.  Sobre o **arquivo** menu, selecione **conectar ao SQL Server**.  
  
    Se conectado anteriormente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o nome do comando será **reconectar-se ao SQL Server**.  
  
2.  Na caixa de diálogo de conexão, digite ou selecione o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Se você estiver se conectando à instância padrão no computador local, você pode inserir **localhost** ou um ponto (**.**).  
  
    -   Se você estiver se conectando à instância padrão em outro computador, digite o nome do computador.  
  
    -   Se você estiver se conectando a uma instância nomeada em outro computador, digite o nome do computador seguido por uma barra invertida e o nome da instância, como MyServer\MyInstance.  
  
3.  Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está configurado para aceitar conexões em uma porta não padrão, insira o número da porta que é usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] conexões a **porta do servidor** caixa. Para a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tentará obter o número da porta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] serviço do navegador.  
  
4.  No **banco de dados** , digite o nome do banco de dados de destino.  
  
    Essa opção não está disponível ao reconectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
5.  No **autenticação** , selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta do Windows atual, selecione **autenticação do Windows**. Para usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] logon, selecione **autenticação do SQL Server** e, em seguida, forneça o nome de logon e senha.  
  
6.  Conexão segura, dois controles são adicionados, o **criptografar Conexão** e **TrustServerCertificate** caixas de seleção. Somente quando **criptografar Conexão** estiver marcada, o **TrustServerCertificate** caixa de seleção está visível. Quando **criptografar Conexão** estiver marcada (true) e **TrustServerCertificate** está desmarcado (false), ele validará o certificado SSL do SQL Server. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para garantir isso, um certificado deve ser instalado no lado do cliente, bem como no lado do servidor.  
  
7.  Clique em **Conectar**.  
  
**Compatibilidade de versão superior**  
  
-   Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 quando o projeto de migração criado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
-   Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 quando o projeto de migração criado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, mas não será capaz de se conectar a versões anteriores, ou seja, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
-   Você será capaz de se conectar a apenas [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 quando o projeto criado for SQL Server 2012.  
  
-   Maior compatibilidade de versão não é válida para o SQL Azure.  
  
||||||||
|-|-|-|-|-|-|-|
|**VERSÃO do servidor de destino do projeto tipo Vs**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005<br /> (Versão: 9)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008<br /> (Versão: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 <br />(Version:13.x)|SQL Azure|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|Sim|Sim|Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||Sim|Sim|Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||||Sim|Sim|| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016|||||Sim||  
|SQL Azure||||||Sim|  
  
> [!IMPORTANT]  
> Conversão dos objetos de banco de dados é executada de acordo com o tipo de projeto, mas não de acordo com a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] você está conectado. No caso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] projeto 2005, conversão é executada de acordo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 mesmo que você está conectado a uma versão posterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016)  
  
## <a name="reconnecting-to-sql-server"></a>Reconectar-se ao SQL Server  
Sua conexão ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve reconectar para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se você quiser uma conexão ativa com o servidor. Você pode trabalhar offline até que você atualizar os metadados, objetos de banco de dados de carga em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], e migrar dados.  
  
O procedimento para reconectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é o mesmo que o procedimento para estabelecer uma conexão.  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizando os metadados do SQL Server  
Metadados sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bancos de dados não é atualizada automaticamente. Os metadados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados é um instantâneo dos metadados quando conectado primeiro à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], ou a última vez que você metadados atualizados manualmente. Você pode atualizar manualmente os metadados para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados.  
  
**Para sincronizar os metadados**  
  
1.  Certifique-se de que você está conectado à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
2.  Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados, marque a caixa de seleção ao lado do banco de dados ou banco de dados do esquema que você deseja atualizar.  
  
    Por exemplo, para atualizar os metadados para todos os bancos de dados, marque a caixa próxima **bancos de dados**.  
  
3.  Bancos de dados ou o banco de dados individual ou o esquema de banco de dados e, em seguida, selecione **sincronizar com o banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Se você deseja personalizar o mapeamento entre os bancos de dados ASE e esquemas e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bancos de dados e esquemas, consulte [mapeamento Sybase ASE esquemas para esquemas SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
-   Se você quiser personalizar opções de configuração para os projetos, consulte [definindo opções de projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
-   Se você quiser personalizado para o mapeamento de tipos de dados de origem e de destino, consulte [mapeamento Sybase ASE e tipos de dados do SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   Se você não precisa fazer qualquer uma dessas, você pode converter as definições de objeto de banco de dados Sybase ASE em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] definições de objeto. Para obter mais informações, consulte [converter objetos de banco de dados do Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados Sybase ASE para o SQL Server - banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
