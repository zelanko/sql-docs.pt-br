---
title: Instalando atualizações por meio do prompt de comando | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bc98ba2b-aae9-4d01-aa85-d4c36428cb0b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 51ad82519e8afd5e4a871046465e0cafec2f783e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62774976"
---
# <a name="installing-updates-from-the-command-prompt"></a>Instalando atualizações no prompt de comando
  Teste e modifique os scripts de instalação para atender às necessidades da sua organização.  
  
## <a name="sample-syntax-for-installation"></a>Sintaxe de exemplo da instalação  
 O nome do pacote de atualização pode variar e incluir um componente de processador, edição e idioma. Aplique uma atualização em um prompt de comando substituindo <nome_do_pacote> pelo nome do seu pacote de atualização:  
  
-   Atualize uma única instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e todos os componentes compartilhados, como o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e Ferramentas de Gerenciamento: você pode especificar a instância usando o parâmetro InstanceName ou o parâmetro InstanceID. Para atualizar uma instância preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], especifique o parâmetro InstanceID<package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance ou <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceID=\<Instance ID>.  
  
-   A instalação pode integrar as últimas atualizações de produto com a instalação principal, para que ela e as atualizações aplicáveis sejam instaladas ao mesmo tempo. Prepare uma instalação da instância do mecanismo de banco de dados para incluir a atualização do produto: setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=PrepareImage /UpdateEnabled=True /UpdateEnabled=True /UpdateSource=\<path, local em que a atualização foi baixada> /INSTANCEID=\<Instance ID> /FEATURES=SQLEngine.  
  
-   Atualize apenas os componentes compartilhados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e as Ferramentas de Gerenciamento: <nome_do_pacote>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
  
-   Atualize todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador e todos os componentes compartilhados, como o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e as Ferramentas de Gerenciamento: <nome_do_pacote>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances.  
  
 Remova uma atualização pelo prompt de comando substituindo <nome_do_pacote> pelo nome do pacote de atualização:  
  
-   Remova uma atualização de uma única instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de todos os componentes compartilhados, como o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e as Ferramentas de Gerenciamento: <nome_do_pacote>.exe /qs /Action=RemovePatch /InstanceName=MyInstance.  
  
-   Remova uma atualização apenas dos componentes compartilhados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e as Ferramentas de Gerenciamento: <nome_do_pacote>.exe /qs /Action=RemovePatch  
  
    > [!NOTE]  
    >  O instalador de atualização assegura que os componentes compartilhados sempre estejam na versão da instância no nível mais alto ou acima dela.  
  
## <a name="supported-command-prompt-parameters"></a>Parâmetros de prompt de comando suportados  
  
> [!IMPORTANT]  
>  Quando possível, forneça credenciais de segurança em tempo de execução. Se você precisar armazenar credenciais em um arquivo de script, proteja o arquivo para evitar acesso não autorizado.  
  
|Opção|DESCRIÇÃO|  
|------------|-----------------|  
|**/?**|Exibe a ajuda do prompt de comando da instalação autônoma|  
|**/action=Patch ou /action=RemovePatch**|Especifica a ação da instalação: Patch ou RemovePatch.|  
|**/allinstances**|Aplica a atualização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a todos os componentes compartilhados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não reconhecem a instância.|  
|**/InstanceName = InstanceName** <sup>1</sup>|Aplica a atualização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada InstanceName e a todos os componentes compartilhados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não reconhecem a instância.|  
|**/InstanceID=Inst1**|Aplica a atualização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inst1 e a todos os componentes compartilhados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não reconhecem a instância.|  
|**/quiet**|Executa a instalação da atualização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo autônomo.|  
|**/qs**|Exibe somente a caixa de diálogo de progresso na interface do usuário.|  
|**/UpdateEnabled**|Especifica se a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve descobrir e incluir atualizações de produto. Os valores válidos são True e False ou 1 e 0. Por padrão, a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluirá as atualizações localizadas.|  
|**/IAcceptSQLServerLicenseTerms**|Necessário somente quando o parâmetro /Q ou /QS é especificado para instalações autônomas.|  
  
 <sup>1</sup> você não pode especificar esse parâmetro para aplicar uma atualização a uma instância preparada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do. Em vez disso, é necessário especificar o parâmetro /instanceID.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral da instalação de manutenção do SQL Server](../../sql-server/install/overview-of-sql-server-servicing-installation.md)  
  
  
