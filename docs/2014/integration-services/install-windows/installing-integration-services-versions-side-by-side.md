---
title: Interoperabilidade e coexistência (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 901637cc41612b1d1737697175d8e7ad43439bcf
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436703"
---
# <a name="interoperability-and-coexistence-integration-services"></a>Interoperabilidade e coexistência (Integration Services)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] O SSIS (Integration Services) pode coexistir lado a lado com o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services e o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services.  
  
## <a name="features-and-differences"></a>Recursos e diferenças  
 A tabela a seguir lista algumas das diferenças entre a versão atual e as versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Recurso|[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]|[!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]|  
|-------------|-------------------------------|---------------------------------|---------------------------------|  
|Ambiente de desenvolvimento|[Versões anteriores do SQL Server Data Tools (SSDT e SSDT-BI)](https://docs.microsoft.com/sql/ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi?view=sql-server-2014)<br /><br /> [SQL Server 2014 Data Tools - Business Intelligence para Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)|[SQL Server Data Tools para Visual Studio 2010](https://msdn.microsoft.com/library/hh500335\(v=vs.103\).aspx)<br /><br /> [SQL Server Data Tools-Business Intelligence para Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)|Business Intelligence Development Studio ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] )|  
|Ambiente de gerenciamento|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|Principal tabela de sistema do msdb para armazenar pacotes|sysssispackages|sysssispackages|sysssispackages|  
|Principal utilitário de prompt de comando para executar pacotes|**dtexec** (dtexec.exe), versão 2014|**dtexec** (dtexec.exe), versão 2012|**dtexec** (dtexec.exe), versão 2008|  
|Pasta raiz padrão do sistema de arquivos|C:\Arquivos de Programas\Microsoft SQL Server\120\DTS|C:\Arquivos de Programas\Microsoft SQL Server\110\DTS|C:\Arquivos de Programas\Microsoft SQL Server\100\DTS|  
|Chave raiz padrão do Registro|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS|  
  
## <a name="side-by-side-compatibility-issues"></a>Problemas de compatibilidade lado a lado  
 Com o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services instalado lado a lado com o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services e o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services, você pode realizar as seguintes tarefas:  
  
-   **Criar pacotes nas Ferramentas de Dados do SQL Server**. Use as ferramentas a seguir para desenvolver e manter pacotes baseados nas versões correspondentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Use a versão do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] do Business Intelligence Development Studio para desenvolver e manter pacotes baseados no [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]  
  
    -   Use a versão [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para desenvolver e manter pacotes baseados no [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
    -   Use a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para desenvolver e manter pacotes baseados no [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
-   **Carregar e executar pacotes**. Você pode carregar e executar pacotes que foram desenvolvidos no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], na versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Quando você adiciona o pacote a um projeto existente, o pacote é permanentemente atualizado para o formato que o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services usa. Quando você abre o arquivo de pacote no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o pacote é atualizado temporariamente para o formato que o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services usa. Se você salvar a alteração no pacote, o pacote será permanentemente atualizado. Quando você salvar o pacote no formato que o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services usa, os pacotes não poderão mais ser abertos na versão [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] correspondente do Business Intelligence Development Studio nem gerenciados pelas ferramentas [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services correspondentes.  
  
-   **Gerenciar pacotes no SQL Server Management Studio**. Não é possível se conectar a uma instância da versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a partir da versão [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Não é possível se conectar a uma instância da versão [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a partir da versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Você pode usar a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para gerenciar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] armazenados em uma instância do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. É preciso modificar o arquivo de configuração do serviço para adicionar a instância do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] à lista de locais gerenciados pelo serviço. Para obter mais informações, consulte [Configurando o Serviço Integration Services &#40;Serviço SSIS#41;](../service/integration-services-service-ssis-service.md).  
  
-   **Armazenar pacotes no SQL Server**. Você pode armazenar pacotes nos bancos de dados a seguir.  
  
    |Formato do pacote|Banco de dados|  
    |--------------------|--------------|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services|O banco de dados msdb de uma instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services|O banco de dados msdb de uma instância do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|  
    |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services|O banco de dados msdb de uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
     Em uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], é possível importar pacotes de uma instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou de uma instância do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], mas não é possível exportar pacotes para uma instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou para uma instância do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
     Em uma instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou em uma instância do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], não é possível importar pacotes de, nem exportar pacotes para, uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   **Executar pacotes**. Você pode executar os pacotes do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services e o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services usando a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do serviço **dtexec** ou do Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sempre que uma ferramenta do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services carregar um pacote que foi criado no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], a ferramenta converterá temporariamente, na memória, o pacote para o formato de pacote que o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] usa. Se o pacote [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] apresentar problemas que impeçam a conversão bem-sucedida, a ferramenta do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services não poderá executar o pacote até que esses problemas sejam resolvidos. Para saber mais, confira [Upgrade Integration Services Packages](upgrade-integration-services-packages.md).  
  
  
