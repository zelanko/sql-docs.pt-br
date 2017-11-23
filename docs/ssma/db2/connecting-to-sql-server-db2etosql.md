---
title: Conectando ao SQL Server (DB2eToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: b59803cb-3cc6-41cc-8553-faf90851410e
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: de9a7af8f191f3c979075de204e4a887128b9c1d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="connecting-to-sql-server-db2etosql"></a>Conectando ao SQL Server (DB2eToSQL)
Para migrar bancos de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014 ou do Azure SQL DB deve se conectar a qualquer uma dessas instâncias de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Quando você se conectar, o SSMA obtém metadados sobre todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e exibe os metadados de banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados. O SSMA armazena informações sobre qual instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está conectado, mas não armazena as senhas.  
  
Sua conexão ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve reconectar para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se você quiser uma conexão ativa com o servidor. Você pode trabalhar offline até que você carregar objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e migrar dados.  
  
Metadados sobre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] não será sincronizado automaticamente. Em vez disso, para atualizar os metadados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados, você deve atualizar manualmente o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadados. Para obter mais informações, consulte o "Sincronizando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadados" seção mais adiante neste tópico.  
  
## <a name="required-sql-server-permissions"></a>Permissões de servidor necessários do SQL  
A conta que é usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] requer permissões diferentes dependendo de ações que realiza a conta:  
  
-   Para converter objetos de DB2 para [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxe, para atualizar os metadados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], ou para salvar a sintaxe convertido em scripts, a conta deve ter permissão para fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Ao carregar objetos do banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], a conta deve ser um membro do **sysadmin** função de servidor. Isso é necessário para instalar os assemblies do CLR.  
  
-   Para migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], a conta deve ser um membro do **sysadmin** função de servidor. Isso é necessário para executar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] pacotes de migração de dados do agente.  
  
-   Para executar o código gerado pelo SSMA, a conta deve ter **Execute** permissões para todas as funções definidas pelo usuário no **ssma_DB2** esquema do banco de dados de destino. Essas funções fornecem funcionalidade equivalente de funções de sistema do DB2 e são usadas por objetos convertidos.  
  
Se a conta que é usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é executar a migração de todas as tarefas, a conta deve ser um membro do **sysadmin** função de servidor.  
  
## <a name="establishing-a-sql-server-connection"></a>Estabelecer uma Conexão de servidor SQL  
Antes de converter objetos de banco de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxe, você deve estabelecer uma conexão com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] onde você deseja migrar os bancos de dados ou o banco de dados DB2.  
  
Quando você define as propriedades de conexão, você também especificar o banco de dados onde objetos e dados serão migrados. Você pode personalizar esse mapeamento no nível de esquema do DB2 depois que você se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter mais informações, consulte [mapeando esquemas do DB2 para esquemas SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md).  
  
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
  
    Essa opção não está disponível quando você se reconectar à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
5.  No **autenticação** , selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta do Windows atual, selecione **autenticação do Windows**. Para usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] logon, selecione **autenticação do SQL Server**e, em seguida, forneça o nome de logon e senha.  
  
6.  Conexão segura, dois controles são adicionados, o **criptografar Conexão** e **TrustServerCertificate** caixas de seleção. Somente quando **criptografar Conexão** estiver marcada, o **TrustServerCertificate** caixa de seleção está visível. Quando **criptografar Conexão** estiver marcada (true) e **TrustServerCertificate** está desmarcado (false), ele validará o certificado SSL do SQL Server. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para garantir isso, um certificado deve ser instalado no lado do cliente, bem como no lado do servidor.  
  
7.  Clique em **Conectar**.  
  
**Compatibilidade de versão superior**  
  
-   Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 quando o projeto de migração criado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
-   Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 quando o projeto de migração criado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, mas não será capaz de se conectar a versões anteriores, ou seja, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
-   Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 quando o projeto criado for SQL Server 2012.  
  
||||||  
|-|-|-|-|-|  
|**VERSÃO do servidor de destino do projeto tipo Vs**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 <br />(Version:13.x)|Banco de dados SQL do Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014|||Sim||  
|Banco de dados SQL do Azure||||Sim|  
  
> [!IMPORTANT]  
> Conversão dos objetos de banco de dados é executada de acordo com o tipo de projeto, mas não de acordo com a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] você está conectado. No caso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados SQL 2016 ou do Azure.  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizando os metadados do SQL Server  
Metadados sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bancos de dados não é atualizada automaticamente. Os metadados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados é um instantâneo dos metadados quando conectado primeiro à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], ou a última vez que você metadados atualizados manualmente. Você pode atualizar manualmente os metadados para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados.  
  
**Para sincronizar os metadados**  
  
1.  Certifique-se de que você está conectado à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
2.  Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados, marque a caixa de seleção ao lado do banco de dados ou banco de dados do esquema que você deseja atualizar.  
  
    Por exemplo, para atualizar os metadados para todos os bancos de dados, marque a caixa próxima **bancos de dados**.  
  
3.  Clique com botão direito **bancos de dados**, ou o banco de dados individual ou esquema de banco de dados e, em seguida, selecione **sincronizar com o banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento entre esquemas de DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bancos de dados e esquemas, consulte [mapeamento DB2 esquemas para esquemas SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md).  
  
-   Para personalizar opções de configuração para os projetos, consulte [configurações de projeto &#40; Conversão de &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) e seções relacionadas.  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeamento DB2 e tipos de dados do SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
-   Se você não precisa executar qualquer uma dessas tarefas, você pode converter as definições de objeto de banco de dados do DB2 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] definições de objeto. Para obter mais informações, consulte [convertendo esquemas de DB2 &#40; DB2ToSQL &#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do DB2 para SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
