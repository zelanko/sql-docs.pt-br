---
title: "Segurança de objeto de banco de dados (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database [Master Data Services], object security
- security [Master Data Services], database objects
ms.assetid: dd5ba503-7607-45d9-ad0d-909faaade179
caps.latest.revision: 10
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: f4aef82cdb9291215f41bad29e4de8ff61b031a8
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="database-object-security-master-data-services"></a>Segurança de objeto de banco de dados (Master Data Services)
  No banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , os dados são armazenados em várias tabelas de banco de dados e estão visíveis em exibições. As informações que você pode ter protegido no aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] são visíveis aos usuários com acesso ao banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
 Especificamente, as informações sobre salários de funcionários podem estar contidas em um modelo de Funcionário, ou as informações financeiras da empresa podem estar em um modelo de Conta. Você pode negar o acesso de um usuário a esses modelos na interface do usuário do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , mas os usuários com acesso ao banco de dados poderão exibir esses dados.  
  
 Você pode conceder permissões a objetos de banco de dados para disponibilizar dados específicos aos usuários. Para obter mais informações sobre como conceder permissões, consulte [Permissões de objeto GRANT &#40;Transact-SQL&#41;](../t-sql/statements/grant-object-permissions-transact-sql.md). Para obter mais informações sobre como proteger o SQL Server, consulte [Protegendo o SQL Server](../relational-databases/security/securing-sql-server.md).  
  
 As seguintes tarefas exigem o acesso ao banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] :  
  
-   [Preparação de dados](#Staging)  
  
-   [Validando dados em relação a regras de negócio](#rules)  
  
-   [Exclusão de versões](#Versions)  
  
-   [Aplicação imediata de permissões de membro de hierarquia](#Hierarchy)  
  
-   [Definição de configurações do sistema](#SysSettings)  
  
##  <a name="Staging"></a> Preparação de dados  
 Na tabela a seguir, cada protegível tem "name" como parte do nome. Isso indica o nome da tabela de preparo que é especificada quando uma entidade é criada. Para obter mais informações, consulte [Visão geral: Importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
|Ação|Protegíveis|Permissões|  
|------------|----------------|-----------------|  
|Criar, atualizar e excluir membros folha e seus atributos.|stg.name_Leaf|Obrigatória: INSERT<br /><br /> Opcional: SELECT e UPDATE|  
|Carregar os dados da tabela de preparo de Folha nas tabelas adequadas do banco de dados do MDS.|stg.udp_name_Leaf|EXECUTE|  
|Criar, atualizar e excluir membros consolidados e seus atributos.|stg.name_Consolidated|Obrigatória: INSERT<br /><br /> Opcional: SELECT e UPDATE|  
|Carregar os dados da tabela de preparo de Consolidados nas tabelas adequadas do banco de dados do MDS.|stg.udp_name_Consolidated|EXECUTE|  
|Mover membros em uma hierarquia explícita.|stg.name_Relationship|Obrigatória: INSERT<br /><br /> Opcional: SELECT e UPDATE|  
|Carregar os dados da tabela de preparo Relação nas tabelas adequadas do banco de dados do MDS.|stg.udp_name_Relationship|EXECUTE|  
|Exibir erros ocorridos quando os dados das tabelas de preparo estavam sendo inseridos nas tabelas do banco de dados do MDS.|stg.udp_name_Relationship|SELECT|  
  
 Para obter mais informações, consulte [Visão geral: Importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md).  
  
##  <a name="rules"></a> Validando dados em relação a regras de negócio  
  
|Ação|Protegível|Permissões|  
|------------|---------------|-----------------|  
|Validar uma versão de dados em relação às regras de negócio|mdm.udpValidateModel|EXECUTE|  
  
 Para obter mais informações, consulte [Procedimento armazenado de validação &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md).  
  
##  <a name="Versions"></a> Exclusão de versões  
  
|Ação|Protegíveis|Permissões|  
|------------|----------------|-----------------|  
|Determinar a ID da versão que deseja excluir|mdm.viw_SYSTEM_SCHEMA_VERSION|SELECT|  
|Excluir uma versão de um modelo|mdm.udpVersionDelete|EXECUTE|  
  
 Para obter mais informações, consulte [Excluir uma versão &#40;Master Data Services&#41;](../master-data-services/delete-a-version-master-data-services.md).  
  
##  <a name="Hierarchy"></a> Aplicação imediata de permissões de membro de hierarquia  
  
|Ação|Protegíveis|Permissões|  
|------------|----------------|-----------------|  
|Aplicação imediata de permissões de membro|mdm.udpSecurityMemberProcessRebuildModel|EXECUTE|  
  
 Para obter mais informações, consulte [Aplicar permissões de membros imediatamente &#40;Master Data Services&#41;](../master-data-services/immediately-apply-member-permissions-master-data-services.md).  
  
##  <a name="SysSettings"></a> Definição de configurações do sistema  
 Há configurações de sistema que você pode ajustar para controlar o comportamento no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Você poderá ajustar essas configurações no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ou, se tiver acesso UPDATE, diretamente na tabela de banco de dados mdm.tblSystemSetting. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Segurança &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  

