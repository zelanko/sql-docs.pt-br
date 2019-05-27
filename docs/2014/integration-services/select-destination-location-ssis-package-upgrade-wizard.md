---
title: Selecionar local de destino (Assistente de atualização da pacotes SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectdestinationlocation.f1
ms.assetid: 89274a71-0ffe-4889-84df-f5a7d78459ef
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d891f456f9c4922b3c680913f767d4e9b14a76a0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66056006"
---
# <a name="select-destination-location-ssis-package-upgrade-wizard"></a>Selecionar Local de Destino (Assistente de Atualização de Pacotes SSIS)
  Use a página **Selecionar Local de Destino** para especificar o destino no qual os pacotes atualizados serão salvos.  
  
> [!NOTE]  
>  Essa página só está disponível quando o Assistente de Atualização de Pacotes do [!INCLUDE[ssIS](../includes/ssis-md.md)] é executado por meio do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou no prompt de comando.  
  
 **Para executar o Assistente de Atualização de Pacotes SSIS**  
  
-   [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>Opções estáticas  
 **Salvar no local de origem**  
 Salve os pacotes atualizados ao mesmo local especificado na página **Selecionar Local de Origem** do assistente.  
  
 Se os pacotes originais estiverem armazenados no sistema de arquivos e você desejar que o assistente faça backup desses pacotes, selecione a opção **Salvar no local de origem** . Para obter mais informações, consulte [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
 **Selecionar novo local de destino**  
 Salve os pacotes atualizados no local de destino especificado nesta página.  
  
 **Origem do pacote**  
 Especifique onde os pacotes de atualização serão armazenados. Os valores dessa opção estão relacionados na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Sistema de Arquivos**|Indica que os pacotes atualizados serão salvos em uma pasta no computador local.|  
|**Armazenamento de Pacotes SSIS**|Indica que os pacotes atualizados serão salvos no armazenamento de pacotes do Integration Services. O repositório de pacotes consiste no conjunto de pastas do sistema de arquivos gerenciado pelo serviço do Integration Services. Para obter mais informações, consulte [Gerenciamento de pacotes &#40;Serviço SSIS&#41;](service/package-management-ssis-service.md).<br /><br /> Selecione esse valor para exibir as opções dinâmicas de **Origem do pacote** correspondentes.|  
|**Microsoft SQL Server**|Indica que os pacotes atualizados serão salvos em uma instância existente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].<br /><br /> Selecione esse valor para exibir as opções dinâmicas de **Origem do pacote** correspondentes.|  
  
 **Pasta**  
 Digite o nome de uma pasta na qual os pacotes atualizados serão salvos ou clique em **Procurar** e localize a pasta.  
  
 **Procurar**  
 Procure para localizar a pasta na qual os pacotes atualizados serão salvos.  
  
## <a name="package-source-dynamic-options"></a>Opções dinâmicas de Origem do pacote  
  
### <a name="package-source--ssis-package-store"></a>Origem do pacote = Repositório de Pacotes SSIS  
 **Servidor**  
 Digite o nome do servidor onde os pacotes de atualização serão salvos ou selecione um servidor na lista.  
  
### <a name="package-source--microsoft-sql-server"></a>Origem do pacote = Microsoft SQL Server  
 **Servidor**  
 Digite o nome do servidor onde os pacotes de atualização serão salvos ou selecione esse servidor na lista.  
  
 **Usar a autenticação do Windows**  
 Selecione para usar a Autenticação do Windows para estabelecer conexão com o servidor.  
  
 **Usar Autenticação do SQL Server**  
 Selecione para usar a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para estabelecer conexão com o servidor. Se você usar a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , será preciso fornecer um nome de usuário e uma senha.  
  
 **Nome de usuário**  
 Digite o nome de usuário a ser usado quando a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] for usada para estabelecer conexão com o servidor.  
  
 **Senha**  
 Digite a senha a ser usada quando a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] for usada para estabelecer conexão com o servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar pacotes do Integration Services](install-windows/upgrade-integration-services-packages.md)  
  
  
