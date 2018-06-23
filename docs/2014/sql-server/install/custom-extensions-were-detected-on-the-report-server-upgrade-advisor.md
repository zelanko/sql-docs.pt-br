---
title: Extensões personalizadas foram detectadas no servidor de relatório (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- rendering extensions [Reporting Services], custom extensions
- security extensions [Reporting Services]
- custom extensions [Reporting Services]
- data processing extensions [Reporting Services], custom extensions
- delivery extensions [Reporting Services]
ms.assetid: fa184bd7-11d6-4ea3-9249-bc1b13db49e5
caps.latest.revision: 32
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 4ae9dbac7395e44bf67731bd0e7a714c73fac296
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007894"
---
# <a name="custom-extensions-were-detected-on-the-report-server-upgrade-advisor"></a>Extensões personalizadas foram detectadas no servidor de relatório (Supervisor de Atualização)
  O Supervisor de Atualização detectou configurações de extensão personalizada nos arquivos de configuração, o que indica que sua instalação tem uma ou mais extensões personalizadas para processamento de dados, entrega, renderização, segurança ou autenticação. A atualização moverá os parâmetros de configuração de extensão com o servidor de relatório atualizado. No entanto, se houver extensões personalizadas instaladas na pasta existente do servidor de relatório, os arquivos de assembly dessas extensões personalizadas não serão movidos para a nova pasta de instalação durante o processo de atualização. Concluída a atualização, mova os arquivos de assembly para a nova pasta de instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo do SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Fornece uma arquitetura extensível que permite aos desenvolvedores criar extensões personalizadas para processamento de dados, entrega, renderização, segurança e autenticação.  
  
 Se forem usados extensões ou assemblies personalizados na instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], será possível usar a Instalação para fazer uma atualização, mas talvez seja necessário mover as extensões para o novo local de instalação ao final da atualização ou executar as etapas anteriores à atualização.  
  
> [!NOTE]  
>  O Supervisor de Atualização não detecta se os assemblies de código personalizados foram configurados para uso em relatórios para calcular valores de item, estilos e formatação. Para obter mais informações, consulte [outros Reporting Services problemas de atualização](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md).  
  
 Se você adquiriu as extensões personalizadas de um fornecedor de software, entre em contato com ele para obter mais informações sobre a atualização da sua funcionalidade personalizada.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Use as seções seguintes para determinar as etapas que devem ser executadas depois ou antes de executar uma atualização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
 [Processamento de dados personalizada ou extensões de entrega](#dataprocdeliver)  
  
 [Extensões de renderização personalizadas](#render)  
  
 [Extensões de segurança ou de autenticação personalizadas em um servidor de relatório do SQL Server 2000](#secauth2000)  
  
 [Extensões de segurança ou de autenticação personalizadas em um servidor de relatório do SQL Server 2005](#secauth2005)  
  
 Concluída a atualização, mova os assemblies de extensão para a nova pasta de instalação e, em seguida, verifique se as extensões personalizadas funcionam como previsto. Se a extensão não funcionar, será necessária uma nova recompilação.  
  
#### <a name="to-recompile-an-extension"></a>Para recompilar uma extensão  
  
1.  Copie o arquivo Microsoft.ReportingServices.Interfaces.dll para a pasta que contém seu código-fonte.  
  
2.  Abra o projeto que contém seus arquivos de origem e adicione uma referência ao arquivo Microsoft.ReportingServices.Interfaces.dll.  
  
3.  Recrie a solução para associá-la à extensão.  
  
 Se você decidir não continuar com a atualização, convém migrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obter etapas sobre migrar extensões personalizadas, consulte [migrando extensões personalizadas](#migrcustext) neste tópico.  
  
###  <a name="dataprocdeliver"></a> Processamento de dados personalizada ou extensões de entrega  
 Se o Supervisor de Atualização detectar extensões de processamento de dados ou de entrega personalizadas, o processo de atualização não será bloqueado. No entanto, concluída a atualização, pode ser necessário executar etapas adicionais para que a funcionalidade personalizada fornecida por essas extensões funcione. Por exemplo, você terá que executar etapas adicionais quando os arquivos de extensão personalizados forem instalados na pasta de instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
##### <a name="post-upgrade-steps-for-custom-data-processing-or-delivery-extensions"></a>Etapas pós-atualização para extensões de processamento de dados ou de entrega personalizadas  
  
1.  Mova os arquivos de extensão para a nova pasta de programa do servidor de relatório. Por padrão, a pasta de programa do servidor de relatório está em \Program Files\Microsoft Server\MSRS10_50 SQL. \< *instance_name*> \report servidor_de_relatório.  
  
 Para obter mais informações, consulte "Implantando uma extensão de processamento de dados" e "Implementando uma extensão de entrega" nos Manuais Online do SQL Server.  
  
###  <a name="render"></a> Extensões de renderização personalizadas  
 Se o Supervisor de Atualização detectar extensões de renderização personalizadas, o processo de atualização será bloqueado. Você pode prosseguir com o processo de atualização removendo as entradas de configuração das extensões personalizadas do arquivo de configuração. No entanto, isso tornará as extensões personalizadas indisponíveis para os usuários depois da atualização. Se você precisar de extensões de renderização personalizadas depois da atualização, terá que criar extensões de renderização atualizadas ou obtê-las com um fornecedor de extensão personalizada.  
  
 Você deve executar etapas para habilitar uma atualização ou pode escolher migrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Não atualize ou migre o servidor de relatório antes de testar e verificar se a extensão de renderização atualizada funciona como esperado.  
  
##### <a name="to-upgrade-custom-rendering-extensions"></a>Para atualizar extensões de renderização personalizadas  
  
1.  Obtenha extensões de renderização com as interfaces mais recentes.  
  
2.  Remova a entrada de extensão de renderização personalizada antiga ou as entradas de RSReportServer.config.  
  
3.  Atualize o servidor de relatório.  
  
4.  Concluída a atualização, instale as extensões atualizadas no servidor de relatório.  
  
 Para obter mais informações, consulte “Implementando uma extensão de renderização" nos Manuais Online do SQL Server.  
  
###  <a name="secauth2000"></a> Extensões de segurança ou de autenticação personalizadas em um servidor de relatório do SQL Server 2000  
 Se o Supervisor de Atualização detectar extensões de segurança ou de autenticação personalizadas em um servidor de relatório do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], o processo de atualização será bloqueado. Você deve executar etapas para habilitar uma atualização ou pode escolher migrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Em qualquer das hipóteses, atualize e recompile as extensões com as interfaces mais recentes em Microsoft.ReportingServices.Interfaces.dll, pois as interfaces mudaram entre o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] e o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
> [!IMPORTANT]  
>  Não atualize ou migre o servidor de relatório antes de testar e verificar se a extensão de segurança ou de autenticação atualizada funciona como esperado.  
  
 Se você estiver usando uma extensão de autenticação personalizada criada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], deverá modificar o código-fonte para que haja suporte para novas classes e membros apresentados nos relatórios controlados por modelos.  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2000-report-server"></a>Para atualizar as extensões de segurança ou de autenticação personalizadas de um servidor de relatório do SQL Server 2000  
  
1.  Atualize e recompile qualquer extensão de segurança ou de autenticação com as interfaces mais recentes.  
  
2.  Remova as entradas de extensão de segurança ou de autenticação de RSReportServer.config.  
  
3.  Atualize o servidor de relatório.  
  
4.  Concluída a atualização, instale as extensões atualizadas no servidor de relatório.  
  
 Para obter mais informações, consulte “Implementando uma extensão de segurança" nos Manuais Online do SQL Server.  
  
###  <a name="secauth2005"></a> Extensões de segurança ou de autenticação personalizadas em um servidor de relatório do SQL Server 2005  
 Se o Supervisor de Atualização detectar extensões de segurança ou de autenticação personalizadas em um servidor de relatório do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o processo de atualização será bloqueado. Você deve executar etapas para habilitar uma atualização ou pode escolher migrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
##### <a name="to-upgrade-custom-security-or-authentication-extensions-from-a-sql-server-2005-report-server"></a>Para atualizar extensões de segurança ou de autenticação personalizadas de um servidor de relatório do SQL Server 2005  
  
1.  Remova as entradas da configuração da extensão de segurança ou de autenticação de RSReportServer.config.  
  
2.  Atualize o servidor de relatório.  
  
3.  Concluída a atualização, adicione as entradas de configuração novamente a RSReportServer.config.  
  
4.  Se os assemblies de extensão foram instalados na pasta de instalação antiga do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], em seguida, mova-os para a nova pasta de instalação.  
  
 Para obter mais informações, consulte “Implementando uma extensão de segurança" nos Manuais Online do SQL Server.  
  
###  <a name="migrcustext"></a> Migrando extensões personalizadas  
 Se você decidir migrar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em vez de executar uma atualização, use as etapas para migrar extensões personalizadas para a nova instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
##### <a name="to-migrate-custom-extensions-to-a-new-reporting-services-instance"></a>Para migrar extensões personalizadas para uma nova instância do Reporting Services  
  
1.  Crie ou obtenha extensões atualizadas com as interfaces mais recentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
2.  Migre o servidor de relatório para uma nova instância.  
  
3.  Configure as extensões na nova instância.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  