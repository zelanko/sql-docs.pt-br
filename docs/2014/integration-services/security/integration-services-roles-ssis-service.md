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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9c6f7ef38c779b07b9cbeffc2b9300360620e350
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52792855"
---
# <a name="integration-services-roles-ssis-service"></a>Funções do Integration Services (Serviço do SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui três funções de nível de banco de dados fixas, `db_ssisadmin`, **db_ssisltduser**, e **db_ssisoperator**, para controlar o acesso aos pacotes. As funções podem ser implementadas apenas em pacotes que são salvos na `msdb` banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você atribui funções a um pacote por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. As atribuições de função são salvos para o `msdb` banco de dados.  
  
## <a name="read-and-write-actions"></a>Ações de leitura e gravação  
 A tabela a seguir descreve as ações de leitura e gravação do Windows e as funções fixas no nível de banco de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Role|Ação de leitura|Ação de gravação|  
|----------|-----------------|------------------|  
|`db_ssisadmin`<br /><br /> ou em<br /><br /> `sysadmin`|Enumerar os próprios pacotes.<br /><br /> Enumerar todos os pacotes.<br /><br /> Exibir os próprios pacotes.<br /><br /> Exibir todos os pacotes.<br /><br /> Executar os próprios pacotes.<br /><br /> Executar todos os pacotes.<br /><br /> Exportar os próprios pacotes.<br /><br /> Exportar todos os pacotes.<br /><br /> Executar todos os pacotes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|Importar pacotes.<br /><br /> Excluir os próprios pacotes.<br /><br /> Excluir todos os pacotes.<br /><br /> Mudar as funções dos próprio pacotes.<br /><br /> Alterar as funções de todos os pacotes.<br /><br /> <br /><br /> **\*\* Importante \* \***  membros da função db_ssisadmin e dc_admin podem estar aptos a elevar seus privilégios para sysadmin. Essa elevação de privilégios pode ocorrer porque essas funções podem modificar os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] podem ser executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o contexto de segurança sysadmin do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para se proteger contra essa elevação de privilégios ao executar planos de manutenção, conjuntos de coletas de dados e outros pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , configure os trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que executam pacotes para usar uma conta proxy com privilégios limitados ou apenas adicione membros sysadmin às funções db_ssisadmin e dc_admin.|  
|**db_ssisltduser**|Enumerar os próprios pacotes.<br /><br /> Enumerar todos os pacotes.<br /><br /> Exibir os próprios pacotes.<br /><br /> Executar os próprios pacotes.<br /><br /> Exportar os próprios pacotes.|Importar pacotes.<br /><br /> Excluir os próprios pacotes.<br /><br /> Mudar as funções dos próprio pacotes.|  
|**db_ssisoperator**|Enumerar todos os pacotes.<br /><br /> Exibir todos os pacotes.<br /><br /> Executar todos os pacotes.<br /><br /> Exportar todos os pacotes.<br /><br /> Executar todos os pacotes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|None|  
|**Administradores do Windows**|Exibir os detalhes de execução de todos os pacotes em execução.|Parar todos os pacotes em execução.|  
  
## <a name="sysssispackages-table"></a>Tabela Sysssispackages  
 O **sysssispackages** na tabela `msdb` contém os pacotes que são salvos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [sysssispackages &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysssispackages-transact-sql).  
  
 A tabela **sysssispackages** inclui colunas que contêm informações sobre as funções atribuídas aos pacotes.  
  
-   A coluna **readerrole** especifica a função que tem acesso de leitura ao pacote.  
  
-   A coluna **writerrole** especifica a função que tem acesso de gravação ao pacote.  
  
-   A coluna **ownersid** contém o identificador de segurança exclusivo do usuário que criou o pacote. Essa coluna define o proprietário do pacote.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, as permissões do `db_ssisadmin` e **db_ssisoperator** funções fixas de nível de banco de dados e o identificador de segurança exclusivo do usuário que criou o pacote se aplicam à função Leitor para pacotes e as permissões de o `db_ssisadmin` função e o identificador de segurança exclusivo do usuário que criou o pacote se aplicam à função de gravação. Um usuário deve ser um membro do `db_ssisadmin`, **db_ssisltduser**, ou **db_ssisoperator** função para ter acesso de leitura ao pacote. Um usuário deve ser um membro do `db_ssisadmin` função para ter acesso de gravação.  
  
## <a name="access-to-packages"></a>Acesso a pacotes  
 As funções fixas no nível de banco de dados trabalham em conjunto com as funções definidas pelo usuário. As funções definidas pelo usuário são as funções criadas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e então usadas para atribuir permissões aos pacotes. Para acessar um pacote, um usuário deve ser membro da função definida pelo usuário e da função fixa no nível de banco de dados pertinente do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Por exemplo, se os usuários são membros do **AuditUsers** função definida pelo usuário que é atribuída a um pacote, eles devem ser membros do `db_ssisadmin`, **db_ssisltduser**, ou **DB _ ssisoperator** função para ter acesso de leitura ao pacote.  
  
 Se você não atribuir funções definidas pelo usuário aos pacotes, o acesso aos pacotes será determinado pelas funções fixas no nível do banco de dados.  
  
 Se você quiser usar funções definidas pelo usuário, você deve adicioná-los para o `msdb` antes de atribuí-las aos pacotes de banco de dados. Você pode criar funções de banco de dados novas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 As funções em nível de banco de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] concedem direitos nas tabelas do sistema [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no banco de dados msdb.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o serviço MSSQLSERVER) deve ser iniciado antes que você pode se conectar ao mecanismo de banco de dados e acesso a `msdb` banco de dados.  
  
 Para atribuir funções a pacotes, você precisa concluir as seguintes tarefas.  
  
-   **Abrir o Pesquisador de Objetos e conectar-se ao Integration Services**  
  
     Para poder atribuir funções aos pacotes por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você deve abrir o Pesquisador de Objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e conectar-se ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
     O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] deve ser iniciado antes de você se conectar ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   **Atribuir funções de leitor e de gravador aos pacotes**  
  
     Você pode atribuir uma função de leitor e de gravador a cada pacote.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Atribuir uma função de leitor e de gravador a um pacote](../assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [Criar uma função definida pelo usuário](../create-a-user-defined-role.md)  
  
-   [Conectar-se ao Integration Services](../connect-to-integration-services.md)  
  
  
