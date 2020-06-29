---
title: Funções do Integration Services (Serviço SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- security [Integration Services], roles
- db_ssisoperator role
- db_ssisadmin role
- fixed database roles [Integration Services]
- packages [Integration Services], security
- roles [Integration Services]
- db_ssisltduser role
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5bc65a7a3ff30deb429ceeb8458ac477432a758c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85422083"
---
# <a name="integration-services-roles-ssis-service"></a>Funções do Integration Services (Serviço do SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]inclui as três funções fixas de nível de banco de dados, `db_ssisadmin` , **db_ssisltduser**e **db_ssisoperator**, para controlar o acesso a pacotes. As funções podem ser implementadas somente em pacotes que são salvos `msdb` no banco de dados do no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você atribui funções a um pacote por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. As atribuições de função são salvas no `msdb` banco de dados.  
  
## <a name="read-and-write-actions"></a>Ações de leitura e gravação  
 A tabela a seguir descreve as ações de leitura e gravação do Windows e as funções fixas no nível de banco de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Função|Ação de leitura|Ação de gravação|  
|----------|-----------------|------------------|  
|`db_ssisadmin`<br /><br /> ou<br /><br /> `sysadmin`|Enumerar os próprios pacotes.<br /><br /> Enumerar todos os pacotes.<br /><br /> Exibir os próprios pacotes.<br /><br /> Exibir todos os pacotes.<br /><br /> Executar os próprios pacotes.<br /><br /> Executar todos os pacotes.<br /><br /> Exportar os próprios pacotes.<br /><br /> Exportar todos os pacotes.<br /><br /> Executar todos os pacotes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|Importar pacotes.<br /><br /> Excluir os próprios pacotes.<br /><br /> Excluir todos os pacotes.<br /><br /> Mudar as funções dos próprio pacotes.<br /><br /> Alterar as funções de todos os pacotes.<br /><br /> <br /><br /> Os membros ** \* \* \* importantes \* ** da função db_ssisadmin e a função dc_admin podem ser capazes de elevar seus privilégios para sysadmin. Essa elevação de privilégios pode ocorrer porque essas funções podem modificar os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] podem ser executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o contexto de segurança sysadmin do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para se proteger contra essa elevação de privilégios ao executar planos de manutenção, conjuntos de coletas de dados e outros pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , configure os trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que executam pacotes para usar uma conta proxy com privilégios limitados ou apenas adicione membros sysadmin às funções db_ssisadmin e dc_admin.|  
|**db_ssisltduser**|Enumerar os próprios pacotes.<br /><br /> Enumerar todos os pacotes.<br /><br /> Exibir os próprios pacotes.<br /><br /> Executar os próprios pacotes.<br /><br /> Exportar os próprios pacotes.|Importar pacotes.<br /><br /> Excluir os próprios pacotes.<br /><br /> Mudar as funções dos próprio pacotes.|  
|**db_ssisoperator**|Enumerar todos os pacotes.<br /><br /> Exibir todos os pacotes.<br /><br /> Executar todos os pacotes.<br /><br /> Exportar todos os pacotes.<br /><br /> Executar todos os pacotes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|Nenhum|  
|**Administradores do Windows**|Exibir os detalhes de execução de todos os pacotes em execução.|Parar todos os pacotes em execução.|  
  
## <a name="sysssispackages-table"></a>Tabela Sysssispackages  
 A tabela **sysssispackages** no `msdb` contém os pacotes que são salvos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [sysssispackages &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysssispackages-transact-sql).  
  
 A tabela **sysssispackages** inclui colunas que contêm informações sobre as funções atribuídas aos pacotes.  
  
-   A coluna **readerrole** especifica a função que tem acesso de leitura ao pacote.  
  
-   A coluna **writerrole** especifica a função que tem acesso de gravação ao pacote.  
  
-   A coluna **ownersid** contém o identificador de segurança exclusivo do usuário que criou o pacote. Essa coluna define o proprietário do pacote.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, as permissões de `db_ssisadmin` e **db_ssisoperator** funções de nível de banco de dados fixas e o identificador de segurança exclusivo do usuário que criou o pacote se aplicam à função de leitor para pacotes e as permissões da `db_ssisadmin` função e o identificador de segurança exclusivo do usuário que criou o pacote se aplicam à função de gravador. Um usuário deve ser membro da `db_ssisadmin` função, **db_ssisltduser**ou **db_ssisoperator** para ter acesso de leitura ao pacote. Um usuário deve ser um membro da `db_ssisadmin` função para ter acesso de gravação.  
  
## <a name="access-to-packages"></a>Acesso a pacotes  
 As funções fixas no nível de banco de dados trabalham em conjunto com as funções definidas pelo usuário. As funções definidas pelo usuário são as funções criadas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e então usadas para atribuir permissões aos pacotes. Para acessar um pacote, um usuário deve ser membro da função definida pelo usuário e da função fixa no nível de banco de dados pertinente do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Por exemplo, se os usuários forem membros da função definida pelo usuário **AuditUsers** que é atribuída a um pacote, eles também deverão ser membros de `db_ssisadmin` , **db_ssisltduser**ou **db_ssisoperator** função para ter acesso de leitura ao pacote.  
  
 Se você não atribuir funções definidas pelo usuário aos pacotes, o acesso aos pacotes será determinado pelas funções fixas no nível do banco de dados.  
  
 Se você quiser usar funções definidas pelo usuário, deverá adicioná-las ao banco de `msdb` dados antes de atribuí-las a pacotes. Você pode criar funções de banco de dados novas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 As funções em nível de banco de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] concedem direitos nas tabelas do sistema [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no banco de dados msdb.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](o serviço MSSQLSERVER) deve ser iniciado antes que você possa se conectar ao Mecanismo de Banco de Dados e acessar o `msdb` banco de dados.  
  
 Para atribuir funções a pacotes, você precisa concluir as seguintes tarefas.  
  
-   **Abrir o Pesquisador de Objetos e conectar-se ao Integration Services**  
  
     Para poder atribuir funções aos pacotes por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você deve abrir o Pesquisador de Objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e conectar-se ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
     O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] deve ser iniciado antes de você se conectar ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   **Atribuir funções de leitor e de gravador aos pacotes**  
  
     Você pode atribuir uma função de leitor e de gravador a cada pacote.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Atribuir uma função de leitor e gravador a um pacote](../assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [Criar uma função definida pelo usuário](../create-a-user-defined-role.md)  
  
-   [Conectar-se ao Integration Services](../connect-to-integration-services.md)  
  
  
