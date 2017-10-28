---
title: Desinstalar e remover o Master Data Services | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: efc2431c-588b-42e7-b23b-c875145a33f6
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9d936f9a9726a5d7dd5a214cdc813a8634119600
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="uninstall-and-remove-master-data-services"></a>Desinstalar e remover o Master Data Services
  Para desinstalar o recurso [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], siga as etapas em [Desinstalar uma instância existente do SQL Server &#40;Instalação&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md) e especifique [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] como um recurso a ser removido na página **Selecionar Recursos**. O processo de desinstalação remove as pastas e arquivos do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e desinstala o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] do computador local.  
  
 Para impedir a perda de dados e evitar que outros computadores no sistema sejam afetados, alguns itens não são removidos nem alterados pelo processo de desinstalação. Revise a tabela a seguir para determinar se os itens deverão permanecer ou ser removidos.  
  
|Item|Descrição|  
|----------|-----------------|  
|Pastas e arquivos|O processo de desinstalação remove a maioria das pastas e arquivos do caminho de instalação.<br /><br /> O processo de desinstalação não remove as pastas Master Data Services e MDSTempDir do local de instalação. Depois que o processo de desinstalação estiver concluído, você poderá excluir essas pastas manualmente do sistema de arquivos. Para obter mais informações, veja [Permissões de pasta e arquivo &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md).|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] assemblies|O processo de desinstalação remove os assemblies do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] do GAC (Cache Global de Assemblies).|  
|Banco de dados|O processo de desinstalação não afeta o banco de dados do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] . O banco de dados permanece intacto na instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que nenhum dado seja perdido, inclusive dados mestres, objetos modelo, permissões de usuário e grupo, regras de negócio, e assim por diante.<br /><br /> Se você não precisa do banco de dados e não pretende conectá-lo futuramente a outro site ou aplicativo do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , talvez queira excluir o banco de dados da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que o hospeda. Para obter mais informações, veja [Excluir um banco de dados](../../relational-databases/databases/delete-a-database.md).|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e Web.config|O processo de desinstalação remove a pasta WebApplication do sistema de arquivos. A pasta WebApplication contém os arquivos do aplicativo Web e o arquivo Web.config do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].<br /><br /> **\*\* Importante \*\*** Antes de desinstalar, talvez você queira copiar o arquivo Web.config para outro local para preservar quaisquer configurações personalizadas ou outras informações existentes no arquivo. Depois que o processo de desinstalação for concluído, o arquivo Web.config não será recuperável.|  
|Itens do IIS (Serviços de Informações da Internet)|O processo de desinstalação não afeta os pools de aplicativos, sites ou aplicativos Web existentes no IIS no computador local. Como o processo de desinstalação remove a pasta WebApplication e o arquivo Web.config do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], qualquer aplicativo Web do [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] que exija esses arquivos deixará de fornecer conteúdo. Se os usuários tentarem acessar o aplicativo Web, receberão o erro HTTP 500.19 – Erro interno do servidor: “A página solicitada não pode ser acessada porque os dados de configuração relacionados à página são inválidos.”<br /><br /> Se você não precisar mais do site ou aplicativo e do pool de aplicativos que atende seu site ou aplicativo, poderá usar uma ferramenta do IIS para excluí-los. Para obter mais informações, veja o [IIS 7 Operations Guide](http://go.microsoft.com/fwlink/?LinkId=184885) (Guia de Operações do IIS 7) no [!INCLUDE[msCoName](../../includes/msconame-md.md)] TechNet.|  
|Grupo**MDS_ServiceAccounts** |Após a conclusão do processo de desinstalação, o grupo do Windows **MDS_ServiceAccounts** e qualquer conta de serviço adicionada ao grupo permanecerão. Se você não precisar mais do grupo e das contas, poderá removê-los.|  
|Registro|O processo de desinstalação remove todas as chave relativas ao [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] do Registro do Windows.|  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  

