---
title: Interoperabilidade e coexistência (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: d0db34c7b894dc7b92ad6061d4f3c53c1cd2dbe9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007734"
---
# <a name="interoperability-and-coexistence-integration-services"></a>Interoperabilidade e coexistência (Integration Services)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] O SSIS (Integration Services) pode coexistir lado a lado com o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services e o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services.  
  
## <a name="features-and-differences"></a>Recursos e diferenças  
 A tabela a seguir lista algumas das diferenças entre a versão atual e as versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Recurso|[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]|[!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]|  
|-------------|-------------------------------|---------------------------------|---------------------------------|  
|Ambiente de desenvolvimento|[SQL Server 2014 Data Tools – Business Intelligence para Visual Studio 2012 CTP 2](http://www.microsoft.com/download/details.aspx?id=40736)<br /><br /> [SQL Server 2014 Data Tools - Business Intelligence para Visual Studio 2013](http://www.microsoft.com/download/details.aspx?id=42313)|[SQL Server Data Tools para Visual Studio 2010](http://msdn.microsoft.com/library/hh500335\(v=vs.103\).aspx)<br /><br /> [SQL Server Data Tools – Business Intelligence para Visual Studio 2012](http://www.microsoft.com/download/details.aspx?id=36843)|Business Intelligence Development Studio ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)])|  
|Ambiente de gerenciamento|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|Principal tabela de sistema do msdb para armazenar pacotes|sysssispackages|sysssispackages|sysssispackages|  
|Principal utilitário de prompt de comando para executar pacotes|**dtexec** (dtexec.exe), versão 2014|**dtexec** (dtexec.exe), versão 2012|**dtexec** (dtexec.exe), versão 2008|  
|Pasta raiz padrão do sistema de arquivos|C:\Arquivos de Programas\Microsoft SQL Server\120\DTS|C:\Arquivos de Programas\Microsoft SQL Server\110\DTS|C:\Arquivos de Programas\Microsoft SQL Server\100\DTS|  
|Chave raiz padrão do Registro|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS|  
  
## <a name="side-by-side-compatibility-issues"></a>Problemas de compatibilidade lado a lado  
 Com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services instalado lado a lado com o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services e o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services, você pode realizar as seguintes tarefas:  
  
-   **Criar pacotes nas Ferramentas de Dados do SQL Server**. Use as ferramentas a seguir para desenvolver e manter pacotes baseados nas versões correspondentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Use a versão do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] do Business Intelligence Development Studio para desenvolver e manter pacotes baseados no [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]  
  
    -   Use o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] versão do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para desenvolver e manter pacotes baseados no [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
    -   Use o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para desenvolver e manter pacotes baseados no [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
-   **Carregar e executar pacotes**. Você pode carregar e executar pacotes que foram desenvolvidos no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], além de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Quando você adiciona o pacote a um projeto existente, o pacote é permanentemente atualizado para o formato que o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services usa. Quando você abre o arquivo de pacote no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o pacote é atualizado temporariamente para o formato que o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services usa. Se você salvar a alteração no pacote, o pacote será permanentemente atualizado. Depois de salvos no formato que [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services usa, os pacotes não poderão mais ser abertos no correspondente [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] versão do Business Intelligence Development Studio nem gerenciados pelas correspondente [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Serviços de integração ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ferramentas do Integration Services.  
  
-   **Gerenciar pacotes no SQL Server Management Studio**. Você não pode se conectar a uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] do serviço o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] versão do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Você não pode se conectar a uma instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] versão do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] serviço o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Você pode usar a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para gerenciar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] armazenados em uma instância do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. É preciso modificar o arquivo de configuração do serviço para adicionar a instância do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] à lista de locais gerenciados pelo serviço. Para obter mais informações, consulte [Configurando o serviço Integration Services &#40; Serviço SSIS&#41;](../service/integration-services-service-ssis-service.md).  
  
-   **Armazenar pacotes no SQL Server**. Você pode armazenar pacotes nos bancos de dados a seguir.  
  
    |Formato do pacote|banco de dados|  
    |--------------------|--------------|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Serviços de integração|banco de dados msdb de uma instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Serviços de integração|banco de dados msdb de uma instância do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|  
    |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Serviços de integração|banco de dados msdb de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
     Em uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você pode importar pacotes de uma instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou de uma instância do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], mas você não pode exportar pacotes para uma instância de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou a uma instância de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
     Em uma instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou em uma instância do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], não é possível importar pacotes de, nem exportar pacotes para, uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   **Executar pacotes**. Você pode executar [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] pacotes do Integration Services usando o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão do **dtexec** utilitário ou de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. Sempre que um [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ferramenta do Integration Services carrega um pacote que foi desenvolvido em [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], a ferramenta converterá temporariamente, na memória, o pacote para o pacote do formato que [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] usa. Se o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] pacote tiver problemas que impedem uma conversão bem-sucedida, o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ferramenta do Integration Services não é possível executar o pacote até que esses problemas sejam resolvidos. Para saber mais, confira [Upgrade Integration Services Packages](upgrade-integration-services-packages.md).  
  
  