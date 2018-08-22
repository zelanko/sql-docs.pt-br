---
title: Conectando ao SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server,Synchronizing SQL Server Metadata
ms.assetid: 1b2a8059-1829-4904-a82f-9c06de1e245f
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 3360da5567d1ff1efef7cbac8e235bc508bef3bb
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40393109"
---
# <a name="connecting-to-sql-server-oracletosql"></a>Conectar-se ao SQL Server (OracleToSQL)
Migrar bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 R2 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014, você deve se conectar a qualquer uma dessas instâncias de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando você se conectar, o SSMA obtém metadados sobre todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exibe metadados de banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados. O SSMA armazena informações sobre qual instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão conectados ao, mas não armazena as senhas.  
  
Sua conexão ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se você quiser que uma conexão ativa com o servidor. Você pode trabalhar offline até que você carrega objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e migrar dados.  
  
Metadados sobre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não será sincronizado automaticamente. Em vez disso, para atualizar os metadados na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, você deve atualizar manualmente o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados. Para obter mais informações, consulte o "Sincronizando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados" seção mais adiante neste tópico.  
  
## <a name="required-sql-server-permissions"></a>Permissões de servidor necessários do SQL  
A conta que é usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exige permissões diferentes, dependendo das ações que executa a conta:  
  
-   Para converter objetos Oracle [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, para atualizar os metadados da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ou para salvar a sintaxe convertido em scripts, a conta deve ter permissão para fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Carregar objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a conta deve ser um membro do **sysadmin** função de servidor. Isso é necessário para instalar assemblies do CLR.  
  
-   A migração de dados a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a conta deve ser um membro do **sysadmin** função de servidor. Isso é necessário para executar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pacotes de migração de dados do agente.  
  
-   Para executar o código que é gerado pelo SSMA, a conta deve ter **Execute** permissões para todas as funções definidas pelo usuário na **ssma_oracle** esquema do banco de dados de destino. Essas funções fornecem funcionalidade equivalente Oracle de funções do sistema e são usadas por objetos convertidos.  
  
Se a conta que é usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é para executar a migração de todas as tarefas, a conta deve ser um membro do **sysadmin** função de servidor.  
  
## <a name="establishing-a-sql-server-connection"></a>Estabelecer uma Conexão de servidor SQL  
Antes de converter objetos de banco de dados Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe, você deve estabelecer uma conexão à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde você deseja migrar o banco de dados Oracle ou bancos de dados.  
  
Quando você define as propriedades de conexão, você também especificar o banco de dados onde objetos e dados serão migrados. Você pode personalizar esse mapeamento no nível do esquema Oracle depois de conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [mapeando esquemas do Oracle para esquemas SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
> [!IMPORTANT]  
> Antes de tentar se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verifique se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução e pode aceitar conexões.  
  
**Para se conectar ao SQL Server**  
  
1.  Sobre o **arquivo** menu, selecione **conectar ao SQL Server**.  
  
    Se conectado anteriormente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o nome do comando será **reconectar-se ao SQL Server**.  
  
2.  Na caixa de diálogo de conexão, insira ou selecione o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Se você estiver se conectando à instância padrão no computador local, você pode inserir **localhost** ou um ponto (**.**).  
  
    -   Se você estiver se conectando à instância padrão em outro computador, digite o nome do computador.  
  
    -   Se você estiver se conectando a uma instância nomeada em outro computador, insira o nome do computador seguido por uma barra invertida e, em seguida, o nome de instância, como MyServer\MyInstance.  
  
3.  Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para aceitar conexões em uma porta não padrão, insira o número da porta que é usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexões na **porta do servidor** caixa. Para a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tentará obter o número da porta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço localizador.  
  
4.  No **banco de dados** , digite o nome do banco de dados de destino.  
  
    Essa opção não está disponível quando você se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  No **autenticação** , selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta atual do Windows, selecione **autenticação do Windows**. Para usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login, selecione **autenticação do SQL Server**e, em seguida, forneça o nome de logon e senha.  
  
6.  Para uma conexão segura, dois controles são adicionados, o **criptografar Conexão** e **TrustServerCertificate** caixas de seleção. Somente quando **criptografar Conexão** estiver marcada, o **TrustServerCertificate** caixa de seleção está visível. Quando **criptografar Conexão** estiver marcada (true) e **TrustServerCertificate** está desmarcado (false), ele validará o certificado SSL do SQL Server. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para garantir isso, um certificado deve ser instalado no lado do cliente, bem como no lado do servidor.  
  
7.  Clique em **Conectar**.  
  
**Maior compatibilidade de versão**  
  
-   Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto de migração criado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto de migração criado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, mas não será capaz de se conectar a versões anteriores, ou seja, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto criado é o SQL Server 2012.  
  
||||||||  
|-|-|-|-|-|-|-|  
|**VERSÃO do servidor de destino do projeto tipo Vs**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (Versão: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (Versão: 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Version:13.x)|Azure SQL DB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Sim|Sim|Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Sim|Sim|Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Sim|Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||||Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||Sim||
|Azure SQL DB||||||Sim|
  
> [!IMPORTANT]  
> Conversão dos objetos de banco de dados é executada, de acordo com o tipo de projeto, mas não de acordo com a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] você está conectado. No caso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] projeto de 2005, conversão é executada de acordo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 mesmo que você está conectado a uma versão posterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizando os metadados do SQL Server  
Metadados sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados não são atualizados automaticamente. Os metadados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados é um instantâneo dos metadados quando você conectou primeiro à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ou a última vez em que você metadados atualizados manualmente. Você pode atualizar manualmente os metadados para todos os bancos de dados ou para qualquer banco de dados individual ou um objeto de banco de dados.  
  
**Para sincronizar os metadados**  
  
1.  Certifique-se de que você está conectado à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, marque a caixa de seleção ao lado do banco de dados ou que você deseja atualizar o esquema de banco de dados.  
  
    Por exemplo, para atualizar os metadados para todos os bancos de dados, marque a caixa próxima **bancos de dados**.  
  
3.  Clique com botão direito **bancos de dados**, ou o banco de dados individual ou esquema de banco de dados e selecione **sincronizar com o banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento entre esquemas Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados e esquemas, consulte [mapeamento de esquemas de Oracle para esquemas SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
-   Para personalizar opções de configuração para os projetos, consulte [definir opções do projeto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md).  
  
-   Para personalizar o mapeamento de tipos de dados de origem e destino, consulte [mapeamento Oracle e tipos de dados do SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
-   Se você não precisa executar qualquer uma dessas tarefas, você pode converter as definições de objeto de banco de dados Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definições de objeto. Para obter mais informações, consulte [converter esquemas do Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Migrando do Oracle bancos de dados para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
