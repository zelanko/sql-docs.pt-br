---
title: Segurança do coletor de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collection [SQL Server]
- security [data collector]
- data collector [SQL Server], security
ms.assetid: e75d6975-641e-440a-a642-cb39a583359a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a7dd2b26662fea95837eabaf61f61e3da04fac69
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62873615"
---
# <a name="data-collector-security"></a>Segurança do coletor de dados
  O coletor de dados usa o modelo de segurança baseado em função implementado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Esse modelo permite que o administrador do banco de dados execute várias tarefas de coletor de dados em um contexto de segurança que tem apenas as permissões exigidas para executar a tarefa. Essa abordagem também é usada para operações que envolvem tabelas internas que só podem ser acessadas usando um procedimento armazenado ou exibição. Nenhuma permissão é concedida a tabelas internas. Em vez disso, as permissões são verificadas no usuário do procedimento armazenado ou na exibição usada para acessar a tabela.  
  
> [!IMPORTANT]  
>  Outro aspecto fundamental desse modelo de segurança são as permissões concêntricas. Nas permissões concêntricas, funções mais privilegiadas herdam as permissões de funções menos privilegiadas nos objetos (incluindo alertas, operadores, tarefas, agendas e proxy). Para obter mais informações, consulte [SQL Server Agent Fixed Database Roles](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 As próximas seções descrevem a segurança da coleta de dados em geral, assim como as funções que você deve conceder aos usuários para que eles possam configurar e usar o coletor de dados e executar tarefas associadas ao data warehouse de gerenciamento.  
  
## <a name="general-security"></a>Segurança em geral  
 O coletor de dados é instalado de acordo com os padrões documentados especificados para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
### <a name="network-security"></a>Segurança de rede  
 Informações confidenciais podem ser passadas entre instâncias de destino, a instância relacional associada ao servidor de configuração, os conjuntos de coleta em execução e o servidor que hospeda o data warehouse de gerenciamento.  
  
 Para proteger qualquer dado transferido em uma rede, são implementados mecanismos de segurança padrão, como criptografia de protocolo para [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="permissions-for-configuring-and-using-the-data-collector"></a>Permissões para configurar e usar o coletor de dados  
 Dependendo da tarefa, os usuários devem ser membros de uma ou mais das funções de banco de dados fixas fornecidas para o coletor de dados. Em ordem de acesso mais privilegiado para acesso menos privilegiado, as funções são as seguintes:  
  
-   `dc_admin`  
  
-   **dc_operator**  
  
-   **dc_proxy**  
  
 Essas funções são armazenadas no banco de dados msdb. Por padrão, nenhum usuário é membro dessas funções de banco de dados. A associação do usuário a elas deve ser explicitamente concedida.  
  
 Os usuários que são membros do `sysadmin` função de servidor fixa têm acesso completo aos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibições do coletor de dados e objetos de agente. Porém, eles precisam ser adicionados explicitamente à funções de coletor de dados.  
  
> [!IMPORTANT]  
>  Os membros das funções db_ssisadmin e dc_admin podem elevar seus privilégios para sysadmin. Essa elevação de privilégios pode ocorrer porque essas funções podem modificar os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] podem ser executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o contexto de segurança sysadmin do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para se proteger contra essa elevação de privilégios ao executar planos de manutenção, conjuntos de coletas de dados e outros pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , configure os trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que executam pacotes para usar uma conta proxy com privilégios limitados ou apenas adicione membros sysadmin às funções db_ssisadmin e dc_admin.  
  
### <a name="dcadmin-role"></a>Função dc_admin  
 Os usuários atribuídos ao `dc_admin` função têm acesso total de administrador (criação, leitura, atualização e exclusão) à configuração do coletor de dados em uma instância de servidor. Membros dessa função podem executar as seguintes operações:  
  
-   Definir propriedades de nível de coletor.  
  
-   Adicionar novos conjuntos de coleta.  
  
-   Instalar novos tipos de coleta.  
  
-   Execute todas as operações permitidas à função **dc_operator** .  
  
 O `dc_admin` função é um membro das funções a seguir:  
  
-   **SQLAgentUserRole**. Essa função é necessária para criar agendas e executar tarefas.  
  
    > [!NOTE]  
    >  Proxies criados para o coletor de dados deve conceder acesso ao `dc_admin` criá-los e usá-los em qualquer etapa de trabalho que exija um proxy.  
  
-   **dc_operator**. Os membros `dc_admin` herdam as permissões dadas a **dc_operator**.  
  
### <a name="dcoperator-role"></a>Função dc_operator  
 Membros da função **dc_operator** têm acesso de Leitura e Atualização. Essa função suporta tarefas de operações relacionadas com a execução e configuração de conjuntos de coleta. Membros dessa função podem executar as seguintes operações:  
  
-   Iniciar ou parar um conjunto de coleta.  
  
-   Enumerar conjuntos de coleta existentes.  
  
-   Exibir informações detalhadas (por exemplo, itens e frequência de coleta) associadas a um conjunto de coleta.  
  
-   Alterar a frequência de carregamento de conjuntos de coleta existentes.  
  
-   Alterar a frequência de coleta de itens de coleta que fazem parte de um conjunto de coleta existente.  
  
 A função **dc_operator** é membro das funções a seguir que são necessárias para enumerar e exibir pacotes do coletor de dados:  
  
-   **db_ssisltduser**  
  
-   **db_ssisoperator**  
  
 Para obter mais informações, veja [Funções do Integration Services &#40;Serviço do SSIS&#41;](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
### <a name="dcproxy-role"></a>Função dc_proxy  
 Membros da função **dc_proxy** têm acesso de Leitura aos conjuntos de coleta do coletor de dados e às propriedades de nível de coletor. Os membros dessa função também podem executar tarefas de sua propriedade e criar etapas de tarefa executadas como uma conta proxy existente.  
  
 Membros dessa função podem executar as seguintes operações:  
  
-   Exibir informações de configuração do conjunto de coleta (por exemplo, parâmetros de entrada de itens de coleta e a frequência de coleta desses itens).  
  
-   Obter informações internas criptografadas que só podem ser acessadas por um procedimento armazenado assinado (por exemplo, informações de conexão de data warehouse usadas para carregamento de dados).  
  
-   Registrar em log eventos de tempo de execução do conjunto de coleta.  
  
 A função **dc_proxy** é membro das seguintes funções que são necessárias para enumerar e exibir pacotes do coletor de dados:  
  
-   **db_ssisltduser**.  
  
-   **db_ssisoperator**  
  
 Para obter mais informações, veja [Funções do Integration Services &#40;Serviço do SSIS&#41;](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
## <a name="permissions-for-configuring-and-using-the-management-data-warehouse"></a>Permissões para configurar e usar o Data Warehouse de gerenciamento  
 Dependendo da tarefa, os usuários devem ser membros de uma ou mais das funções de banco de dados fixas fornecidas para acessar o data warehouse de gerenciamento. Em ordem de acesso mais privilegiado para acesso menos privilegiado, as funções são as seguintes:  
  
-   **mdw_admin**  
  
-   **mdw_writer**  
  
-   **mdw_reader**  
  
 Essas funções são armazenadas no banco de dados msdb. Por padrão, nenhum usuário é membro dessas funções de banco de dados. A associação do usuário a elas deve ser explicitamente concedida.  
  
 Os usuários que são membros do `sysadmin` função de servidor fixa têm acesso total às exibições do coletor de dados. Porém, eles precisam ser adicionados explicitamente à funções do banco de dados para executar outras operações.  
  
### <a name="mdwadmin-role"></a>Função mdw_admin  
 Membros da função **mdw_admin** têm acesso de Leitura, Gravação, Atualização e Exclusão no data warehouse de gerenciamento.  
  
 Membros dessa função podem executar as seguintes operações:  
  
-   Alterar o esquema do data warehouse de gerenciamento quando necessário (por exemplo, adicionando uma tabela nova quando é instalado um novo tipo de coleta).  
  
    > [!NOTE]  
    >  Onde houver uma alteração de esquema, o usuário também deve ser um membro do `dc_admin` função para instalar um novo tipo de coletor, pois esta ação exige permissão para atualizar a configuração do coletor de dados no msdb.  
  
-   Executar tarefas de manutenção no data warehouse de gerenciamento, como arquivo ou limpeza.  
  
### <a name="mdwwriter-role"></a>Função mdw_writer  
 Membros da função **mdw_writer** podem carregar e gravar dados no data warehouse de gerenciamento. Qualquer coletor que armazena dados no data warehouse de gerenciamento deve ser membro dessa função.  
  
### <a name="mdwreader-role"></a>Função mdw_reader  
 Membros da função **mdw_reader** têm acesso de Leitura ao data warehouse de gerenciamento. Como o objetivo dessa função é dar suporte à solução de problemas fornecendo acesso a dados históricos, os membros dessa função não podem exibir outros elementos do esquema do data warehouse de gerenciamento.  
  
## <a name="see-also"></a>Consulte também  
 [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)  
  
  
