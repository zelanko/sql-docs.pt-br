---
title: Logons, usuários e funções de banco de dados (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- security [Master Data Services], database roles
- database [Master Data Services], users
- security [Master Data Services], database users
- database [Master Data Services], roles
- database [Master Data Services], logins
- security [Master Data Services], database logins
ms.assetid: 72ee383e-a619-461b-9f9d-1cac162ab0c5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 2b7430a12c64ab669182ab2877bb6620b42b2f48
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52795408"
---
# <a name="database-logins-users-and-roles-master-data-services"></a>Logons, usuários e funções de banco de dados (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] inclui logons, usuários e funções que são instalados automaticamente na instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] que hospeda o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Esses logons, usuários e funções não devem ser modificados.  
  
## <a name="logins"></a>Logons  
  
|Logon|Descrição|  
|-----------|-----------------|  
|`mds_dlp_login`|Permite a criação de assemblies UNSAFE.<br /><br /> - Logon desabilitado com senha gerada aleatoriamente.<br /><br /> – É mapeado para o dbo do banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .<br /><br /> – Para o msdb, mds_clr_user é mapeado para esse logon.<br /><br /> <br /><br /> Para obter mais informações, consulte [Criando um assembly](../relational-databases/clr-integration/assemblies/creating-an-assembly.md).|  
|`mds_email_login`|Logon habilitado usado para notificações.<br /><br /> No msdb e no banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , mds_email_user é mapeado para esse logon.|  
  
## <a name="msdb-users"></a>Usuários de msdb  
  
|User|Descrição|  
|----------|-----------------|  
|`mds_clr_user`|Não usado.<br /><br /> Mapeia para mds_dlp_login.|  
|`mds_email_user`|Usado para notificações.<br /><br /> Mapeado para mds_dlp_login.<br /><br /> É um membro da função: DatabaseMailUserRole.|  
  
## <a name="master-data-services-database-users"></a>Usuários de banco de dados do Master Data Services  
  
|User|Descrição|  
|----------|-----------------|  
|`mds_email_user`|Usado para notificações.<br /><br /> Tem permissão SELECT para o esquema de mdm.<br /><br /> Tem permissão EXECUTE para o tipo de tabela definida pelo usuário mdm.MemberGetCriteria.<br /><br /> Tem permissão EXECUTE para o procedimento armazenado mdm.udpNotificationQueueActivate.|  
|**mds_schema_user**|É proprietário dos esquemas mdm e mdq. O esquema padrão é mdm.<br /><br /> Não está associado a um logon.|  
|**mds_ssb_user**|Usado para executar tarefas de Service Broker.<br /><br /> Possui permissão DELETE, INSERT, REFERENCES, SELECT e UPDATE em todos os esquemas.<br /><br /> Não está associado a um logon.|  
  
## <a name="master-data-services-database-role"></a>Função de banco de dados do Master Data Services  
  
|Role|Descrição|  
|----------|-----------------|  
|`mds_exec`|Esta função contém a conta designada no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] quando você cria um aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] e designa uma conta para o pool de aplicativos. A função mds_exec tem:<br /><br /> **EXECUTE** permissão em todos os esquemas.<br /><br /> **ALTER**, **inserir**, e **selecione** permissão nessas tabelas:<br />mdm.tblStgMember<br />mdm.tblStgMemberAttribute<br />mdm.tbleStgRelationship<br /><br /> **Selecione** permissão nessas tabelas:<br />mdm.tblUser<br />mdm.tblUserGroup<br />mdm.tblUserPreference<br /><br /> **Selecione** permissão sobre esses modos de exibição:<br />mdm.viw_SYSTEM_SECURITY_NAVIGATION<br />mdm.viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL<br />viw_SYSTEM_SECURITY_ROLE_ACCCESSCONTROL<br />mdm.viw_SYSTEM_SECURITY_USER_MODEL|  
  
## <a name="schemas"></a>Esquemas  
  
|Role|Descrição|  
|----------|-----------------|  
|`mdm`|Contém todo o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] e objetos do Service Broker diferentes das funções contidas no esquema mdq.|  
|`mdq`|Contém funções de banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] relacionadas aos resultados da filtragem de membros com base nas expressões regulares ou similaridade e para formatação de emails de notificação.|  
|**stg**|Contém tabelas de banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , procedimentos armazenados e exibições relacionadas ao processo de preparo. Não exclua nenhum destes objetos. Para obter mais informações sobre o processo de preparo, consulte [importação de dados &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Segurança de objeto de banco de dados &#40;Master Data Services&#41;](../../2014/master-data-services/database-object-security-master-data-services.md)  
  
  
