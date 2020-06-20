---
title: Locais de arquivos para instâncias padrão e nomeadas do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 463c570e-9f75-4653-b3b8-4d61753b0013
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6363dd09dba21273e57b6b087002000bec4e54dc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012597"
---
# <a name="file-locations-for-default-and-named-instances-of-sql-server"></a>Locais de arquivos para instâncias padrão e nomeadas do SQL Server
  Uma instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste em uma ou mais instâncias separadas. Uma instância, seja padrão ou nomeada, tem seu próprio conjunto de arquivos de programas e de dados, bem como um conjunto de arquivos comuns compartilhados entre todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador.  
  
 Para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que inclui o [!INCLUDE[ssDE](../../includes/ssde-md.md)], o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], cada componente tem um conjunto completo de arquivos executáveis e de dados, além de arquivos comuns compartilhados por todos os componentes.  
  
 Para isolar locais de instalação para cada componente, IDs de instância exclusivos são gerados para cada componente em uma determinada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Os arquivos de programas e os arquivos de dados não podem ser instalados em uma unidade de disco removível, em um sistema de arquivos que usa compactação, em um diretório onde os arquivos do sistema estão localizados e em unidades compartilhadas em uma instância de cluster de failover.  
>   
>  Os bancos de dados de sistema (mestre, modelo, MSDB e tempdb) e os bancos de dados de usuário do [!INCLUDE[ssDE](../../includes/ssde-md.md)] podem ser instalados com um servidor de arquivos SMB como uma opção de armazenamento. Isso se aplica a instalações autônomas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a FCI (instalações de cluster de failover) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para saber mais, veja [Instalar o SQL Server com o compartilhamento de arquivos SMB como uma opção de armazenamento](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
>   
>  Não exclua nenhum dos seguintes diretórios ou seus conteúdos: Binn, Data, Ftdata, HTML ou 1046. Você pode excluir outros diretórios, se necessário; entretanto, talvez você não possa recuperar alguma funcionalidade ou dados perdidos sem desinstalar e depois reinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não exclua, nem modifique quaisquer dos arquivos .htm no diretório de HTML. Eles são necessários para que as ferramentas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funcionem corretamente.  
  
## <a name="shared-files-for-all-instances-of-ssnoversion"></a>Arquivos compartilhados para todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Os arquivos comuns usados por todas as instâncias em um único computador são instalados na pasta [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)] , em que \<*drive*> é a letra da unidade na qual os componentes são instalados. Em geral, o padrão é a unidade C.  
  
## <a name="file-locations-and-registry-mapping"></a>Locais de arquivo e mapeamento de registro  
 Durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , um ID de instância é gerado para cada componente do servidor. Os componentes de servidor nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são o [!INCLUDE[ssDE](../../includes/ssde-md.md)], o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 O ID da instância padrão é construído usando o seguinte formato:  
  
-   MSSQL para o [!INCLUDE[ssDE](../../includes/ssde-md.md)], seguido pelo número de versão principal, seguido por um sublinhado e a versão secundária, quando aplicável, e um ponto, seguidos pelo nome da instância.  
  
-   MSAS para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], seguido pelo número de versão principal, seguido por um sublinhado e a versão secundária, quando aplicável, e um ponto, seguidos pelo nome da instância.  
  
-   MSRS para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], seguido pelo número de versão principal, seguido por um sublinhado e a versão secundária, quando aplicável, e um ponto, seguidos pelo nome da instância.  
  
 Exemplos de IDs de instância padrão nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são como segue:  
  
-   MSSQL12.MSSQLSERVER para uma instância padrão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   MSAS12.MSSQLSERVER para uma instância padrão do [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)].  
  
-   MSSQL12.MyInstance para uma instância nomeada do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] denominada "MyInstance."  
  
 A estrutura de diretórios de uma instância nomeada do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que inclua o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], denominada "MyInstance" e instalada nos diretórios padrão seria a seguinte:  
  
-   C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MyInstance\  
  
-   C:\Arquivos de Programas\Microsoft SQL Server\MSAS12.MyInstance\  
  
 Você pode especificar qualquer valor para o ID da instância, mas evite caracteres especiais e palavras-chave reservadas.  
  
 Você pode especificar um ID de instância não padrão durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Em vez de \<Program Files> \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , um \<custom path> \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será usado se o usuário optar por alterar o diretório de instalação padrão. Observe que as IDs de instância que começam com sublinhado (_) ou contêm o sinal numérico (#) ou o cifrão ($) não têm suporte.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e os componentes cliente não reconhecem instâncias e, portanto, não recebem uma ID de instância. Por padrão, os componentes que não reconhecem instância são instalados em um único diretório: [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]. A alteração do caminho de instalação de um componente compartilhado também o altera para os outros componentes compartilhados. Instalações subsequentes instalam componentes sem reconhecimento de instância no mesmo diretório que a instalação original.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]é o único [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componente que dá suporte à renomeação da instância após a instalação. Se uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] for renomeada, o ID da instância não será alterado. Depois que a renomeação da instância for concluída, os diretórios e as chaves do registro continuarão usando o ID de instância criado durante a instalação.  
  
 O hive do Registro é criado em HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*Instance_ID*> para componentes com reconhecimento de instância. Por exemplo,  
  
-   HKLM\Software \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. MyInstance  
  
-   HKLM\Software \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSAS12. MyInstance  
  
-   HKLM\Software \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSRS12. MyInstance  
  
 O registro também mantém um mapeamento do ID da instância para o nome da instância. O mapeamento do ID da instância para o nome da instância é mantido como segue:  
  
-   [HKEY_LOCAL_MACHINE \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] \Software [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \Instance Names\SQL] "InstanceName" = "MSSQL12"  
  
-   [HKEY_LOCAL_MACHINE \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] \Software [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \Instance Names\OLAP] "InstanceName" = "MSAS12"  
  
-   [HKEY_LOCAL_MACHINE \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] \Software [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \Instance Names\RS] "InstanceName" = "MSRS12"  
  
## <a name="specifying-file-paths"></a>Especificando caminhos de arquivos  
 Durante a Instalação, você pode alterar o caminho de instalação dos seguintes recursos:  
  
 O caminho de instalação é exibido na Instalação somente para recursos com uma pasta de destino configurável pelo usuário:  
  
|Componente|Caminho padrão<sup>1, 2</sup>|Caminho configurável<sup>3</sup> ou fixo|  
|---------------|---------------------------------|--------------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] componentes de servidor|\Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceID> \| Configurável|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] arquivos de dados|\Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceID> \| Configurável|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] servidor|\Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSAS12. \<InstanceID> \| Configurável|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] arquivos de dados|\Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSAS12. \<InstanceID> \| Configurável|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servidor de relatório|\Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSRS12. \<InstanceID> \Reporting Services\ReportServer\Bin \| configurável|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] gerenciador de relatórios|\Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSRS12. \<InstanceID> \Reporting \| caminho fixo Services\ReportManager|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|\<Install Directory>\120\DTS \| configurável<sup>4</sup>|  
|Componentes de cliente (exceto bcp.exe e sqlcmd.exe)|\<Install Directory>\120\Tools \| configurável<sup>4</sup>|  
|Componentes de cliente (bcp.exe e sqlcmd.exe)|\<Install Directory>\Client SDK\ODBC\110\Tools\Binn|Caminho fixo|  
|Replicação e objetos COM do lado do servidor|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]COM \\ <sup>5</sup>|Caminho fixo|  
|DLLs de componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o mecanismo de Tempo de Execução de Transformação de Dados, o mecanismo Pipeline de Transformação de Dados e o utilitário de prompt de comando `dtexec`|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|Caminho fixo|  
|DLLs que dão suporte de conexão gerenciado para o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Connections|Caminho fixo|  
|DLLs para cada tipo de enumerador cujo suporte é dado pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\ForEachEnumerators|Caminho fixo|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , provedores de WMI|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]\|Caminho fixo compartilhado|  
|Componentes que são compartilhados entre todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]\|Caminho fixo compartilhado|  
  
 <sup>1</sup> Verifique se a pasta \Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \ está protegida com permissões limitadas.  
  
 <sup>2</sup> A unidade padrão para esses locais é *systemdrive*, normalmente a unidade C.  
  
 <sup>3</sup> Os caminhos de instalação para recursos filho são determinados pelo caminho de instalação do recurso pai.  
  
 <sup>4</sup> Um único caminho de instalação é compartilhado entre o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e os componentes cliente. A alteração do caminho de instalação de um componente também o altera para outros componentes. As instalações subsequentes instalam componentes no mesmo local que a instalação original.  
  
 <sup>5</sup> Esse diretório é usado por todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um computador. Se você aplicar uma atualização a alguma das instâncias no computador, quaisquer alterações em arquivos nessa pasta afetarão todas as instâncias no computador. Ao adicionar recursos a uma instalação existente, não é possível alterar o local de um recurso instalado anteriormente, nem especificar o local para o novo recurso. Você deve instalar recursos adicionais nos diretórios já estabelecidos pela Instalação ou desinstalar e reinstalar o produto.  
  
> [!NOTE]  
>  Para configurações clusterizadas, você deve selecionar uma unidade local que esteja disponível em todo nó do cluster.  
  
 Quando você especifica um caminho de instalação durante a Instalação para os componentes de servidor ou os arquivos de dados, o programa de Instalação usa o ID da instância além do local especificado para arquivos de programas e de dados. A Instalação não usa o ID da instância para ferramentas e outros arquivos compartilhados. A Instalação também não usa nenhum ID de instância para os arquivos de programas e de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , embora use o ID da instância para o repositório do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Se você definir um caminho de instalação para o recurso [!INCLUDE[ssDE](../../includes/ssde-md.md)] , a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará esse caminho como o diretório raiz para todas as pastas específicas da instância para essa instalação, incluindo Arquivos de Dados SQL. Nesse caso, se você definir a raiz como "c:\Arquivos de programas \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceName> \MSSQL \\ ", os diretórios específicos da instância são adicionados ao final desse caminho.  
  
 Os clientes que optarem por usar a funcionalidade de atualização USESYSDB no Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (modo UI da Instalação) poderão facilmente colocar-se em uma situação em que o produto é instalado em uma estrutura de pastas recursiva. Por exemplo, \<*SQLProgramFiles*> \mssql12\mssql\ MSSQL10_50 \MSSQL\Data \\ . Em vez disso, para usar o recurso USESYSDB, defina um caminho de instalação para o recurso Arquivos de Dados SQL em vez do recurso [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
> [!NOTE]
>  Espera-se que os arquivos de dados sempre estejam localizados em um diretório filho denominado Data. Por exemplo, especifique c:\Arquivos de programas \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceName> \ para especificar o caminho raiz para o diretório de dados dos bancos de dado do sistema durante a atualização quando os arquivos de dados são encontrados em c:\Arquivos de programas \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \<InstanceName> \MSSQL\Data.  
  
## <a name="see-also"></a>Consulte Também  
 [Configuração de Mecanismo de Banco de Dados-diretórios de dados](../../../2014/sql-server/install/database-engine-configuration-data-directories.md)   
 [Configuração do Analysis Services - diretórios de dados](../../../2014/sql-server/install/analysis-services-configuration-data-directories.md)  
  
  
