---
title: "Ajuda do Assistente de Instalação | Microsoft Docs"
ms.custom: 
ms.date: 2017-04-21
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install
ms.reviewer: 
ms.suite: sql
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
caps.latest.revision: "62"
ms.author: mikeray
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 611c6f16d9b7e278a64af18e13c24ae7217a3d95
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="installation-wizard-help"></a>Ajuda do Assistente de Instalação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve algumas das páginas de configuração no Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

## <a name="instance-configuration"></a>Configuração da instância
Use a página **Configuração de Instância** do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para especificar se uma instância padrão ou uma instância nomeada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser criada. Se uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é ainda não estiver instalada, uma instância padrão será criada, a menos que você especifique uma instância nomeada.  
  
Cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste em um conjunto distinto de serviços que têm configurações específicas para agrupamentos e outras opções. A estrutura de diretórios, a estrutura do Registro e os nomes do serviço refletem o nome da instância e uma ID de instância específica criada durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Uma instância é a instância padrão ou uma instância nomeada. O nome de instância padrão é MSSQLSERVER. Não é necessário que um cliente especifique o nome da instância para estabelecer uma conexão. Uma instância nomeada é determinada pelo usuário durante a Instalação. Você pode instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como uma instância nomeada sem instalar a instância padrão em primeiro lugar. Apenas uma instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independentemente da versão, pode ser a instância padrão em determinado momento.  
  
> [!NOTE]  
> Com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep, você pode especificar o nome da instância ao concluir uma instância preparada na página de **Configuração da Instância**. Você pode optar por configurar a instância preparada que está concluindo como uma instância padrão, se não houver nenhuma instância padrão existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador.  
  
### <a name="multiple-instances"></a>Várias instâncias  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um único servidor ou processador, mas somente uma instância pode ser a padrão. Todas as demais devem ser instâncias nomeadas. Um computador pode executar várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] simultaneamente e cada instância é executada independentemente das demais.  
  
 Para obter mais informações, consulte [Especificações de capacidade máxima para o SQL Server](../maximum-capacity-specifications-for-sql-server.md).  
  
### <a name="options"></a>Opções  
 Somente instâncias de cluster de failover — Especifique o nome de rede de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse nome identifica a instância do cluster de failover na rede.  
  
 Instância padrão ou nomeada — Considere as seguintes informações ao decidir se deve instalar uma instância padrão ou nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Se você planeja instalar uma única instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um servidor de banco de dados, ela deve ser uma instância padrão.  
  
-   Use uma instância nomeada para situações em que planeja ter várias instâncias no mesmo computador. Um servidor pode hospedar somente uma instância padrão.  
  
-   Qualquer aplicativo que instale o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] deve instalá-lo como uma instância nomeada. Isso minimizará conflitos quando vários aplicativos forem instalados no mesmo computador.  
  
 **Instância padrão**  
 Selecione esta opção para instalar uma instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um computador pode hospedar apenas uma instância padrão; todas as demais devem ser nomeadas. Entretanto, se você tiver uma instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada, poderá adicionar uma instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no mesmo computador.  
  
 **Instância nomeada**  
 Selecione esta opção para criar uma nova instância nomeada. Esteja ciente do seguinte ao nomear uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Os nomes de instância não diferenciam maiúsculas de minúsculas.  
  
-   Nomes de instância não podem iniciar nem terminar com um sublinhado (_).  
  
-   Os nomes de instância não podem conter o termo "Padrão" ou outras palavras-chave reservadas. Se uma palavra-chave reservada for usada em um nome de instância, ocorrerá um erro de Instalação. Para obter mais informações, consulte [Palavras-chave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md).  
  
-   Se você especificar MSSQLServer para o nome de instância, uma instância padrão será criada.  
  
-   Uma instalação do [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] sempre é instalada como uma instância nomeada de '[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]'. Você não pode especificar um nome de instância diferente para essa função de recurso.  
  
-   Os nomes de instância estão limitados a 16 caracteres.  
  
-   O primeiro caractere do nome da instância deve ser uma letra. As letras aceitáveis são as definidas pelo Padrão Unicode 2.0. Elas incluem os caracteres latinos de a-z, A-Z e caracteres de letra de outros idiomas.  
  
-   Os caracteres subsequentes podem ser letras definidas pelo Padrão Unicode 2.0, números decimais de Latim Básico ou outros scripts nacionais, o sinal de cifrão ($) ou um sublinhado (_).  
  
-   Não são permitidos espaços inseridos ou outros caracteres especiais em nomes de instância. Os caracteres barra invertida (\\), vírgula (,), dois-pontos (:), ponto-e-vírgula (;), aspas simples ('), E comercial (&), hífen (-) e arroba (@) também não são permitidos.  
  
     Somente caracteres válidos na página de código atual do Windows podem ser usados em nomes de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se um caractere Unicode sem-suporte for usado, ocorrerá um erro de Instalação.  
  
 **Instâncias e recursos detectados**  
 Exiba uma lista de instâncias e componentes instalados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador em que a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada.  
  
 **ID da Instância** – Por padrão, o nome da instância é usado como a ID da Instância. Isso é usado para identificar os diretórios de instalação e as chaves do Registro da sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse é o caso para instâncias padrão e instâncias nomeadas. Para uma instância padrão, o nome de instância e o ID da instância seriam MSSQLSERVER. Para usar uma ID de instância não padrão, especifique-a no campo **ID da Instância** .  
  
> [!IMPORTANT]  
>  Com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep, a ID da Instância exibida nesta página é a ID da Instância especificada durante a etapa de preparação da imagem do processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep. Você não poderá especificar uma ID da Instância diferente durante a etapa de conclusão de imagem.  
  
> [!NOTE]  
>  As IDs de instância que começam com sublinhado (_) ou contêm o sinal numérico (#) ou o cifrão ($) não têm suporte.  
  
 Para obter mais informações sobre nomenclatura de ID de instância, locais de arquivos e diretórios, consulte [Locais de arquivo para instâncias nomeadas e padrão do SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  
 Todos os componentes de uma determinada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são gerenciados como uma unidade. Todos os service packs e atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serão aplicados a cada componente de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que compartilham o mesmo nome de instância devem atender aos seguintes critérios:  
  
-   **Mesma versão**  
  
-   **Mesma edição**  
  
-   **Mesmas configurações de idioma**  
  
-   **Mesmo estado clusterizado**  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não dá suporte a cluster.  
  
-   **Mesmo sistema operacional**  
  
## <a name="analysis-services-configuration---account-provisioning"></a>Configuração do Analysis Services - Provisionamento de conta
  Use esta página para definir o modo de servidor e para conceder permissões administrativas a usuários ou serviços que requerem acesso irrestrito ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A Instalação não adiciona automaticamente o Grupo local do Windows BUILTIN\Administradores à função de administrador de servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da instância que está sendo instalada. Para adicionar o grupo Administradores local à função de administrador do servidor, é necessário especificar explicitamente esse grupo.  
  
 Se você estiver instalando o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], conceda permissões administrativas aos administradores de farms do SharePoint ou aos administradores de serviços responsáveis por uma implantação do servidor [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um farm do [!INCLUDE[SPS2010](../../includes/sps2010-md.md)].  
  
### <a name="options"></a>Opções  
 **Modo de servidor** - o modo de servidor especifica o tipo de bancos de dados do Analysis Services que podem ser implantados no servidor. Os modos de servidor são determinados durante a Instalação e não podem ser modificados posteriormente. Cada modo é mutuamente exclusivo, o que significa que você precisará de duas instâncias do Analysis Services, cada uma configurada para um modo diferente, para oferecer suporte às soluções de modelo OLAP e de tabela.  
  
 **Especificar Administradores** – Você deve especificar, pelo menos, um administrador de servidor para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os usuários ou grupos que você especificar se tornarão membros da função de administrador de servidor da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que está sendo instalada. Eles devem ser contas de usuário de domínio do Windows no mesmo domínio que o computador no qual você está instalando o software.  
  
> [!NOTE]  
>  O UAC (Controle de Conta de Usuário) é um recurso de segurança do Windows que requer um administrador para aprovar especificamente aplicativos ou ações administrativas para que tenham permissão de execução. Como o UAC é ativado por padrão, será solicitado que você permita operações específicas que exijam privilégios elevados. É possível configurar o UAC para alterar o comportamento padrão ou personalizar o UAC para programas específicos. Para obter mais informações sobre o UAC e sua configuração, consulte o [Guia Passo a Passo do Controle de Conta de Usuário](http://go.microsoft.com/fwlink/?linkid=196350) e [User Account Control (Wikipedia)](http://go.microsoft.com/fwlink/?linkid=196351).  
  
### <a name="see-also"></a>Consulte também  
 [Configurar contas de serviço &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md) [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  

 ## <a name="analysis-services-configuration---data-directories"></a>Configuração do Analysis Services - diretórios de dados
  Os diretórios padrão na tabela a seguir podem ser configurados pelo usuário durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A permissão para acessar esses arquivos é concedida a administradores locais e a membros do grupo de segurança SQLServerMSASUser$\<instância> que é criado e provisionado durante a instalação.  
  
### <a name="uielement-list"></a>Lista de elementos de interface do usuário  
  
|Descrição|Diretório padrão|Recomendações|  
|-----------------|-----------------------|---------------------|  
|Diretório raiz de dados|C:\Arquivos de Programas\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Data\ |Assegure-se de que a pasta \Arquivos de programas\Microsoft SQL Server\ esteja protegida com permissões limitadas. O desempenho do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] depende, em muitas configurações, do desempenho do armazenamento no qual o diretório de dados está localizado. Coloque esse diretório no armazenamento de melhor desempenho conectado ao sistema. Para instalações de cluster de failover, verifique se os diretórios de dados estão colocados no disco compartilhado.|  
|Diretório do arquivo de log|C:\Arquivos de Programas\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Log\ |Este é o diretório de arquivos de log do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e inclui o log do FlightRecorder. Se você aumentar a duração do registrador de voo, atente para que o diretório de logs tenha espaço suficiente.|  
|Diretório temporário|C:\Arquivos de Programas\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Temp\ |Coloque o diretório Temp no subsistema de armazenamento de alto desempenho.|  
|Diretório de backup|C:\Arquivos de Programas\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Backup\ |Este é o diretório dos arquivos de backup padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Em instalações do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, também é o local em que os Serviços de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] armazenam em cache arquivos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].<br /><br /> Verifique se as permissões apropriadas estão definidas para impedir perda de dados e se o grupo de usuários do serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tem permissões suficientes para gravar no diretório de backup. O uso de uma unidade mapeada para diretórios de backup não tem suporte.|  
  
### <a name="notes"></a>Observações  
  
-   As instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que são implantadas em um farm do SharePoint armazenam arquivos de aplicativos, arquivos de dados e propriedades em bancos de dados de conteúdo e bancos de dados de aplicativo de serviços.  
  
-   Ao adicionar recursos a uma instalação existente, não é possível alterar o local de um recurso instalado anteriormente, nem especificar o local para o novo recurso.  

-   Talvez você precise configurar softwares de verificação, como aplicativos antivírus e antispyware, para excluir pastas e tipos de arquivos do SQL Server. Examine este artigo de suporte para obter mais informações: [Software antivírus em computadores que executam o SQL Server](https://support.microsoft.com/kb/309422).
  
-   Se você especificar diretórios de instalação diferentes do padrão, assegure que as pastas de instalação sejam exclusivas a esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os componentes [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também devem ser instalados em diretórios separados.  
  
-   Os arquivos de programas e os arquivos de dados não podem ser instalados nas seguintes situações:  
  
    -   Em uma unidade de disco removível  
  
    -   Em um sistema de arquivos que usa compactação  
  
    -   Em um diretório onde os arquivos do sistema estão localizados  
  
### <a name="see-also"></a>Consulte também  
 Para obter mais informações sobre nomenclatura de ID de instância, locais de arquivos e diretórios, consulte [Locais de arquivo para instâncias nomeadas e padrão do SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  
## <a name="database-engine-configuration---data-directories"></a>Configuração do Mecanismo de Banco de Dados – Diretórios de dados
  Use esta página para especificar o local de instalação para programas e arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]. Com base no tipo de instalação, o armazenamento com suporte pode incluir disco local, armazenamento compartilhado ou um servidor de arquivos SMB.  
  
 Para especificar um compartilhamento de arquivos SMB como um diretório, você deve digitar o caminho UNC com suporte manualmente. Não há suporte para a navegação até um compartilhamento de arquivos SMB. Este é um formato de caminho UNC de um compartilhamento de arquivos SMB com suporte: \\\NomeServidor\NomeCompartilhamento\\....  
  
### <a name="stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 A tabela a seguir lista os tipos de armazenamento com suporte e os diretórios padrão para uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que podem ser configurados pelo usuário durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="uielement-list"></a>Lista de elementos de interface do usuário  
  
|Descrição|Tipo de armazenamento com suporte|Diretório padrão|Recomendações|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Diretório raiz de dados|Disco local, servidor de arquivos SMB, armazenamento compartilhado* |C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A instalação configurará ACLs para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interromperá a herança como parte da configuração.|  
|Diretório do banco de dados de usuário|Disco local, servidor de arquivos SMB, armazenamento compartilhado*|C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data |As práticas recomendadas para diretórios de dados de usuário dependem dos requisitos de carga de trabalho e desempenho.|  
|Diretório de log do banco de dados de usuário|Disco local, servidor de arquivos SMB, armazenamento compartilhado*|C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|Verifique se o diretório de log tem espaço suficiente.|  
|Diretório de backup|Disco local, servidor de arquivos SMB, armazenamento compartilhado*|C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Backup|Defina as permissões adequadas para evitar perda de dados e verifique se a conta de usuário para o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem permissões suficientes para realizar gravações no diretório de backup. O uso de uma unidade mapeada para diretórios de backup não tem suporte.|  
  
 *Embora haja suporte para discos compartilhados, essa não é uma prática recomendada para uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 A tabela a seguir lista os tipos de armazenamento compatíveis e os diretórios padrão para uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que são configuráveis pelo usuário durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Descrição|Tipo de armazenamento com suporte|Diretório padrão|Recomendações|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Diretório raiz de dados|Armazenamento compartilhado, servidor de arquivos SMB|\<Unidade:>\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> Dica: se o disco compartilhado tiver sido selecionado na página **Seleção de Disco de Cluster** , o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster** .|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A instalação configurará ACLs para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interromperá a herança como parte da configuração.|  
|Diretório do banco de dados de usuário|Armazenamento compartilhado, servidor de arquivos SMB|\<Unidade:>Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> Dica: se o disco compartilhado tiver sido selecionado na página **Seleção de Disco de Cluster** , o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster** .|As práticas recomendadas para diretórios de dados de usuário dependem dos requisitos de carga de trabalho e desempenho.|  
|Diretório de log do banco de dados de usuário|Armazenamento compartilhado, servidor de arquivos SMB|\<Unidade:>\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> Dica: se o disco compartilhado tiver sido selecionado na página **Seleção de Disco de Cluster** , o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster** .|Verifique se o diretório de log tem espaço suficiente.|  
|Diretório de backup|Disco local, armazenamento compartilhado, servidor de arquivos SMB|\<Unidade:>\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Backup<br /><br /> Dica: se o disco compartilhado tiver sido selecionado na página **Seleção de Disco de Cluster** , o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster** .|Defina as permissões adequadas para evitar perda de dados e verifique se a conta de usuário do serviço do SQL Server tem permissões suficientes para gravar no diretório de backup. O uso de uma unidade mapeada para diretórios de backup não tem suporte.|  
  
### <a name="security-considerations"></a>Considerações sobre segurança  
 A instalação configurará ACLs para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interromperá a herança como parte da configuração.  
  
 As seguintes recomendações se aplicam ao servidor de arquivos SMB:  
  
-   A conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser uma conta de domínio se for usado um servidor de arquivos SMB.  
  
-   A conta usada para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter permissões NTFS FULL CONTROL na pasta de compartilhamento de arquivos SMB usada como o diretório de dados.  
  
-   A conta usada para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter privilégios SeSecurityPrivilege no servidor de arquivos SMB. Para conceder esse privilégio, use o console de Política de Segurança Local no servidor de arquivos para adicionar a conta de configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à política **Gerenciar o log de auditoria e segurança**. Essa configuração está disponível na seção **Atribuições de Direitos do Usuário** , em **Políticas Locais** , no console **Política de Segurança Local** .  
  
### <a name="notes"></a>Observações  
  
-   Ao adicionar recursos a uma instalação existente, você não pode alterar o local de um recurso instalado anteriormente, nem especificar o local para um novo recurso.  
  
-   Se você especificar diretórios de instalação diferentes do padrão, assegure que as pastas de instalação sejam exclusivas a esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os componentes [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também devem ser instalados em diretórios separados.  
  
-   Os arquivos de programas e os arquivos de dados não podem ser instalados nas seguintes situações:  
  
    -   Em uma unidade de disco removível  
  
    -   Em um sistema de arquivos que usa compactação  
  
    -   Em um diretório onde os arquivos do sistema estão localizados  
  
    -   Em uma unidade de rede mapeada em uma instância de cluster de failover  
  
### <a name="see-also"></a>Consulte também  
### <a name="analysis-services-configuration---data-directories"></a>Configuração do Analysis Services - diretórios de dados
  Os diretórios padrão na tabela a seguir podem ser configurados pelo usuário durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A permissão para acessar esses arquivos é concedida a administradores locais e a membros do grupo de segurança SQLServerMSASUser$\<instância> que é criado e provisionado durante a instalação.  
  
#### <a name="uielement-list"></a>Lista de elementos de interface do usuário  
  
|Descrição|Diretório padrão|Recomendações|  
|-----------------|-----------------------|---------------------|  
|Diretório raiz de dados |C:\Arquivos de Programas\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Data |Assegure-se de que a pasta \Arquivos de programas\Microsoft SQL Server\ esteja protegida com permissões limitadas. O desempenho do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] depende, em muitas configurações, do desempenho do armazenamento no qual o diretório de dados está localizado. Coloque esse diretório no armazenamento de melhor desempenho conectado ao sistema. Para instalações de cluster de failover, verifique se os diretórios de dados estão colocados no disco compartilhado.|  
|Diretório do arquivo de log|C:\Arquivos de Programas\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Log |Este é o diretório de arquivos de log do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e inclui o log do FlightRecorder. Se você aumentar a duração do registrador de voo, atente para que o diretório de logs tenha espaço suficiente.|  
|Diretório temporário|C:\Arquivos de Programas\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Temp |Coloque o diretório Temp no subsistema de armazenamento de alto desempenho.|  
|Diretório de backup|C:\Arquivos de Programas\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Backup |Este é o diretório dos arquivos de backup padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Em instalações do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, também é o local em que os Serviços de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] armazenam em cache arquivos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].<br /><br /> Verifique se as permissões apropriadas estão definidas para impedir perda de dados e se o grupo de usuários do serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tem permissões suficientes para gravar no diretório de backup. O uso de uma unidade mapeada para diretórios de backup não tem suporte.|  
  
#### <a name="notes"></a>Observações  
  
-   As instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que são implantadas em um farm do SharePoint armazenam arquivos de aplicativos, arquivos de dados e propriedades em bancos de dados de conteúdo e bancos de dados de aplicativo de serviços.  
  
-   Ao adicionar recursos a uma instalação existente, não é possível alterar o local de um recurso instalado anteriormente, nem especificar o local para o novo recurso.  

-   Talvez você precise configurar softwares de verificação, como aplicativos antivírus e antispyware, para excluir pastas e tipos de arquivos do SQL Server. Examine este artigo de suporte para obter mais informações: [Software antivírus em computadores que executam o SQL Server](https://support.microsoft.com/kb/309422).
  
-   Se você especificar diretórios de instalação diferentes do padrão, assegure que as pastas de instalação sejam exclusivas a esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os componentes [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também devem ser instalados em diretórios separados.  
  
-   Os arquivos de programas e os arquivos de dados não podem ser instalados nas seguintes situações:  
  
    -   Em uma unidade de disco removível  
  
    -   Em um sistema de arquivos que usa compactação  
  
    -   Em um diretório onde os arquivos do sistema estão localizados  
  
#### <a name="see-also"></a>Consulte também  
 Para obter mais informações sobre nomenclatura de ID de instância, locais de arquivos e diretórios, consulte [Locais de arquivo para instâncias nomeadas e padrão do SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  
    
 [Permissões de compartilhamento e de NTFS em um servidor de arquivos](http://go.microsoft.com/fwlink/?LinkID=206571) 

## <a name="database-engine-configuration---filestream"></a>Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos
  Use esta página para habilitar FILESTREAM para esta instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. O FILESTREAM integra o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] com um sistema de arquivos NTFS armazenando dados BLOB (objeto binário grande) **varbinary(max)** como arquivos no sistema de arquivos. [!INCLUDE[tsql](../../includes/tsql-md.md)] podem inserir, atualizar, consultar, pesquisar e fazer backup de dados FILESTREAM. As interfaces do sistema de arquivos do Win32 fornecem acesso de streaming aos dados.  
  
### <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Habilitar FILESTREAM para acesso Transact-SQL**  
 Selecione para habilitar FILESTREAM para acesso [!INCLUDE[tsql](../../includes/tsql-md.md)] . Este controle deve ser verificado antes que as demais opções de controle fiquem disponíveis.  
  
 **Habilitar FILESTREAM para acesso de fluxo de E/S de arquivo**  
 Selecione para habilitar o acesso de fluxo Win32 para FILESTREAM.  
  
 **Nome de compartilhamento do Windows**  
 Use este controle para digitar o nome do compartilhamento do Windows no qual os dados FILESTREAM serão armazenados.  
  
 **Permitir que clientes remotos tenham acesso de fluxo a dados FILESTREAM**  
 Selecione este controle para permitir que clientes remotos acessem dados FILESTREAM neste servidor.  
  
### <a name="see-also"></a>Consulte também  
 [Habilitar e configurar FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  

  
## <a name="database-engine-configuration---server-configuration"></a>Configuração do Mecanismo de Banco de Dados - Configuração do Servidor
  Use esta página para definir o modo de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e adicionar grupos ou usuários do Windows como administradores do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
### <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>Considerações sobre execução do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o grupo **BUILTIN\Administradores** era provisionado como um logon no [!INCLUDE[ssDE](../../includes/ssde-md.md)] e os membros do grupo local Administradores podiam fazer logon usando as credenciais de Administrador. O uso de permissões elevadas não é uma prática recomendada. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , o grupo **BUILTIN\Administradores** não é provisionado como logon. Por isso, você deve criar um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada usuário administrativo e adicionar esse logon à função de servidor fixa sysadmin durante a instalação de uma nova instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Você também deve fazer isso para as contas do Windows usadas para executar trabalhos de agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Eles incluem trabalhos do agente de replicação.  
  
### <a name="options"></a>Opções  
 **Modo de Segurança** – Selecione Autenticação do Windows ou Autenticação de Modo Misto para sua instalação.  
  
 **Provisionamento de Entidade do Windows** – Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o grupo local Windows Builtin\Administrator era colocado na função de servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin, concedendo efetivamente aos administradores do Windows o acesso à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o grupo Builtin\Administradores não é provisionado na função de servidor sysadmin. Em vez disso, você deve provisionar explicitamente administradores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para as novas instalações durante a Instalação.  
  
> [!IMPORTANT]  
>  Você deve provisionar explicitamente administradores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para as novas instalações durante a Instalação. A Instalação não permitirá que você continue até que conclua esta etapa.  
  
 **Especificar Administradores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** – É necessário especificar, pelo menos, uma entidade do Windows para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para adicionar a conta sob a qual a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada, clique no botão **Usuário Atual** . Para adicionar ou remover contas da lista de administradores do sistema, clique em **Adicionar** ou **Remover**e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Depois de concluir a edição da lista, clique em **OK**e verifique a lista de administradores na caixa de diálogo de configuração. Quando a lista estiver concluída, clique em **Avançar**.  
  
 Se você selecionar Autenticação de Modo Misto, deverá fornecer credenciais de logon para a conta interna AS (administrador do sistema) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Modo de autenticação do Windows**  
 Quando um usuário se conecta por uma conta de usuário do Windows, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valida o nome e a senha da conta usando o token da entidade do Windows no sistema operacional. Este é o modo de autenticação padrão e é muito mais seguro que o Modo Misto. A Autenticação do Windows usa o protocolo de segurança Kerberos, fornece imposição de política de senha e termos de validação de complexidade para senhas fortes, dá suporte ao bloqueio de contas e dá suporte à expiração de senhas.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Nunca defina uma senha de sa em branco ou fraca.  
  
 **Modo Misto (autenticação do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])**  
 Permite que os usuários se conectem usando Autenticação do Windows ou Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os usuários que se conectarem por uma conta de usuário do Windows podem usar conexões confiáveis que são validadas pelo Windows.  
  
 Se você deve escolher Autenticação de Modo Misto e tem um requisito para usar logons do SQL a fim de acomodar aplicativos herdados, deverá definir senhas fortes para todas as contas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  A autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é fornecida somente para fins de compatibilidade com versões anteriores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **Digite a senha**  
 Insira e confirme o logon de administrador de sistema (sa). As senhas são a primeira linha de defesa contra intrusos; portanto, a configuração de senhas fortes é essencial para a segurança do seu sistema. Nunca defina uma senha de sa em branco ou fraca.  
  
> [!NOTE]  
>  Senhas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem conter de 1 até 128 caracteres, incluindo qualquer combinação de letras, símbolos e números. Se você escolher a autenticação de Modo Misto, deverá inserir uma senha forte de sa antes de continuar na próxima página do Assistente de Instalação.  
  
 **Diretrizes de senha forte**  
 As senhas fortes não são prontamente adivinhadas por uma pessoa e não são facilmente violadas usando-se um programa de computador. As senhas fortes não podem usar condições ou termos proibidos, incluindo:  
  
-   Um espaço em branco ou condição NULL  
  
-   "Senha"  
  
-   "Admin"  
  
-   "Administrador"  
  
-   "sa"  
  
-   "sysadmin"  
  
 Uma senha forte não pode ter os termos a seguir associados ao computador de instalação:  
  
-   O nome do usuário atualmente conectado à máquina.  
  
-   O nome do computador.  
  
 Uma senha forte deve ter mais de 8 caracteres e satisfazer pelo menos três dos quatro critérios a seguir:  
  
-   Deve conter letras maiúsculas.  
  
-   Deve conter letras minúsculas.  
  
-   Deve conter números.  
  
-   Deve conter caracteres não alfanuméricos; por exemplo, #,% ou ^.  
  
 As senhas inseridas nessa página devem satisfazer os requisitos de política de senha forte. Se você tiver qualquer automação que use Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , assegure-se de que a senha satisfaça os requisitos de política de senha forte.  
  
### <a name="related-content"></a>Conteúdo relacionado  
 Para obter mais informações sobre como escolher a Autenticação do Windows vs. Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Escolher um modo de autenticação](../../relational-databases/security/choose-an-authentication-mode.md).  
  
 Para obter mais informações sobre como escolher uma conta para executar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], consulte [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).
  
## <a name="database-engine-configuration---tempdb"></a>Configuração do Mecanismo de Banco de Dados - TempDB
  Use esta página para especificar o local, tamanho, configurações de crescimento e número de arquivos dos dados de **tempdb** e do arquivo de log para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]. Com base no tipo de instalação, o armazenamento com suporte pode incluir disco local, armazenamento compartilhado ou um servidor de arquivos SMB.  
  
 Para especificar um compartilhamento de arquivos SMB como um diretório, você deve digitar o caminho UNC com suporte manualmente. Não há suporte para a navegação até um compartilhamento de arquivos SMB. Este é um formato de caminho UNC de um compartilhamento de arquivos SMB com suporte: \\\NomeServidor\NomeCompartilhamento\\....  
  
### <a name="data-and-log-directories-for--a-stand-alone-instance-of--includessnoversionincludesssnoversion-mdmd"></a>Diretórios de dados e de log para uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 A tabela a seguir lista os tipos de armazenamento com suporte e os diretórios padrão para instâncias autônomas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você pode definir durante a instalação.  
  
|Descrição|Tipo de armazenamento com suporte|Diretório padrão|Recomendações|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**Diretórios de dados**|Disco local, servidor de arquivos SMB, armazenamento compartilhado* |C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A instalação configurará ACLs para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interromperá a herança como parte da configuração.<br /><br /> As práticas recomendadas para diretórios **tempdb** dependem dos requisitos de carga de trabalho e desempenho. Especifique várias pastas/unidades para distribuir os arquivos de dados entre vários volumes.|  
|**Diretório de log**|Disco local, servidor de arquivos SMB, armazenamento compartilhado*|C:\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|Verifique se o diretório de log tem espaço suficiente.|  
  
 *Embora haja suporte para discos compartilhados, essa não é uma prática recomendada para uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="data-and-log-directories-for-a-failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Diretórios de dados e de log para uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 A tabela a seguir lista os tipos de armazenamento compatíveis e os diretórios padrão para uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que são configuráveis pelo usuário durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Descrição|Tipo de armazenamento com suporte|Diretório padrão|Recomendações|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Diretório de dados**tempdb** |Disco local, armazenamento compartilhado, servidor de arquivos SMB|\<Unidade:>\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\Data<br /><br /> Dica: se o disco compartilhado tiver sido selecionado na página **Seleção de Disco de Cluster** , o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster** .|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A instalação configurará ACLs para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interromperá a herança como parte da configuração.<br /><br /> Verifique se o diretório, ou diretórios, especificado (se vários arquivos forem especificados) é válido para todos os nós do cluster. Durante o failover, se os diretórios de **tempdb** não estiverem disponíveis no nó de destino de failover, o recurso do SQL Server não será exibido online.|  
|Diretório de logs de**tempdb** |Disco local, armazenamento compartilhado, servidor de arquivos SMB|\<Unidade:>\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> Dica: se o disco compartilhado tiver sido selecionado na página **Seleção de Disco de Cluster** , o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster** .|As práticas recomendadas para diretórios de dados de usuário dependem dos requisitos de carga de trabalho e desempenho.<br /><br /> Verifique se o diretório especificado é válido para todos os nós de cluster. Durante o failover, se os diretórios de **tempdb** não estiverem disponíveis no nó de destino de failover, o recurso do SQL Server não será exibido online.<br /><br /> Verifique se o diretório de log tem espaço suficiente.|  
  
### <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 Defina as configurações para **tempdb** de acordo com suas necessidades e carga de trabalho. As configurações a seguir se aplicam aos arquivos de dados **tempdb** :  
  
-   **Número de arquivos** é o número total de arquivos de dados para **tempdb**. O valor padrão é inferior a oito, ou o número de núcleos lógicos detectados pela instalação. Como regra geral, se o número de processadores lógicos for menor ou igual a oito, use o mesmo número de processadores lógicos para os arquivos de dados. Se o número de processadores lógicos for maior do que oito, use oito arquivos de dados e, se a contenção persistir, aumente o número de arquivos de dados em múltiplos de quatro (até atingir o número de processadores lógicos) até que a contenção seja reduzida a um nível aceitável, ou faça alterações no código/carga de trabalho. 
  
-   **Tamanho inicial (MB)** é o tamanho inicial em MB de cada arquivo de dados **tempdb** . O valor padrão é 8 MB (ou 4 MB para [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]). [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] apresenta um tamanho do arquivo inicial máximo de 262.144 MB (256 GB). [!INCLUDE[sssql15](../../includes/sssql15-md.md)] tinha um tamanho do arquivo inicial máximo de 1024 MB. Todos os arquivo de dados **tempdb** têm o mesmo tamanho inicial. Como o **tempdb** é recriado sempre que o SQL Server é iniciado ou passa por failover, você deve especificar um tamanho próximo ao tamanho exigido por sua carga de trabalho para uma operação normal. Para otimizar ainda mais a criação de **tempdb** durante o início, habilite a [Inicialização Instantânea de Arquivo do Banco de Dados](../../relational-databases/databases/database-instant-file-initialization.md).  
  
-   **Tamanho inicial total (MB)** é o tamanho cumulativo de todos os arquivos de dados **tempdb** .  
  
-   **Expansão automática (MB)** é a quantidade de espaço em megabytes que cada arquivo de dados **tempdb** aumentará automaticamente quando ficar sem espaço. No [!INCLUDE[sssql15](../../includes/sssql15-md.md)] e posterior, todos os arquivos de dados aumentarão ao mesmo tempo conforme a quantidade especificada nessa configuração.  
  
-   **Expansão automática total (MB)** é o tamanho cumulativo de cada evento de expansão automática.  
  
-   **Diretórios de dados** mostra todos os diretórios que contêm arquivos de dados **tempdb** . Quando há vários diretórios, os arquivos de dados são colocados em diretórios por meio de um rodízio. Por exemplo, se você criar três diretórios e especificar oito arquivos de dados, os números de arquivos de dados 1, 4 e 7 serão criados no diretório primeiro. Os arquivos de dados 2, 5 e 8 serão criados no segundo diretório. Os arquivos de dados 3 e 6 estarão no terceiro diretório.  
  
-   Para adicionar diretórios, clique em **Adicionar...**.  
  
-   Para remover um diretório, selecione o diretório e clique em **Remover**.  
  
 **Arquivo de logs TempDB** é o nome do arquivo de log. Ele é criado automaticamente. As configurações a seguir se aplicam apenas aos arquivos de dados **tempdb** :  
  
-   **Tamanho inicial (MB)** é o tamanho inicial do arquivo de log **tempdb** . O valor padrão é 8 MB (ou 4 MB para [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]). [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] apresenta um tamanho do arquivo inicial máximo de 262.144 MB (256 GB). [!INCLUDE[sssql15](../../includes/sssql15-md.md)] tinha um tamanho do arquivo inicial máximo de 1024 MB. Como o **tempdb** é recriado sempre que o SQL Server é iniciado ou passa por failover, você deve especificar um tamanho próximo ao tamanho exigido por sua carga de trabalho para uma operação normal. Para otimizar ainda mais a criação de **tempdb** durante o início, habilite a [Inicialização Instantânea de Arquivo do Banco de Dados](../../relational-databases/databases/database-instant-file-initialization.md).  
  
-   **Observação: Tempdb** usa o registro em log mínimo. O log do **tempdb** não pode passar por backup. Ele é recriado sempre que o SQL Server é iniciado ou quando uma instância de cluster passa por failover.  
  
-   **Expansão automática (MB)** é o incremento de expansão do log **tempdb** em megabytes.  O valor padrão de 64 MB cria o número ideal de arquivos de log virtuais durante a inicialização.  
  
-   **Observação: os arquivos de log Tempdb** não usam a inicialização instantânea de arquivo.  
  
-   **Diretório de log** é o diretório no qual os arquivos de log **tempdb** são criados. Há apenas um diretório de log **tempdb** .  
  
### <a name="security-considerations"></a>Considerações sobre segurança  
 A instalação configurará ACLs para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interromperá a herança como parte da configuração.  

 As seguintes recomendações se aplicam ao servidor de arquivos SMB:  
  
-   A conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser uma conta de domínio se for usado um servidor de arquivos SMB.  
  
-   A conta usada para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter permissões NTFS FULL CONTROL na pasta de compartilhamento de arquivos SMB usada como o diretório de dados.  
  
-   A conta usada para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter privilégios SeSecurityPrivilege no servidor de arquivos SMB. Para conceder esse privilégio, use o console de Política de Segurança Local no servidor de arquivos para adicionar a conta de configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à política **Gerenciar o log de auditoria e segurança**. Essa configuração está disponível na seção **Atribuições de Direitos do Usuário** , em **Políticas Locais** , no console **Política de Segurança Local** .  
  
### <a name="notes"></a>Observações  
  
-   Se você especificar diretórios de instalação diferentes do padrão, assegure que as pastas de instalação sejam exclusivas a esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os componentes [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também devem ser instalados em diretórios separados.  
  
### <a name="see-also"></a>Consulte também  
 [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Permissões de compartilhamento e de NTFS em um servidor de arquivos](http://go.microsoft.com/fwlink/?LinkID=206571)  

## <a name="database-engine-configuration---user-instance"></a>Configuração do Mecanismo de Banco de Dados - Instância de usuário
Use a página **Instância de Usuário** para gerar uma instância separada do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usuários sem permissões de administrador e adicione usuários à função de administrador.  
  
### <a name="option"></a>Opção  
 Habilitar instâncias de usuário  
 O padrão é habilitado. Para desabilitar a funcionalidade de habilitar instâncias de usuário, desmarque a caixa de seleção.  
  
 A instância do usuário, também conhecida como instância filha ou cliente, é uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerada pela instância pai (a instância primária executada como um serviço, como o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) em nome de um usuário. A instância de usuário é executada como um processo de usuário no contexto de segurança daquele usuário. A instância de usuário é isolada da instância pai e de qualquer outra instância de usuário que estiver em execução no computador. O recurso de instância de usuário também é chamado de "Executar como Usuário Normal (RANU, Run As Normal User)".  
  
> [!NOTE]  
>  Logons provisionados como membros da função de servidor fixa **sysadmin** durante a instalação são provisionados como administradores no banco de dados de modelo. Eles são membros da função de servidor fixa **sysadmin** na instância de usuário, a menos que sejam removidos  
  
 Adicionar usuário à função de Administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 O padrão é desabilitado. Para adicionar o usuário de instalação atual à função de Administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , marque a caixa de seleção.  
  
 Usuários do [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] que são membros de BUILTIN\Administrators não são adicionados automaticamente à função de servidor fixa sysadmin quando se conectam a [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Somente os usuários do [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] explicitamente adicionados a uma função de administrador de nível de servidor podem administrar o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Qualquer membro do grupo Built-In\Users pode se conectar à instância do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , mas terá permissões limitadas para executar tarefas do banco de dados. Por esse motivo, os usuários cujos privilégios do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] sejam herdados de BUILTIN\Administradores e Built-In\Users das versões anteriores do Windows devem receber explicitamente privilégios administrativos em instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] executadas no [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)].  
  
 Para fazer qualquer alteração nas funções de usuário após a conclusão deste programa de instalação, use a ferramenta SQLSAC.exe (Configuração da Área de Superfície) do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . Para atualizar a lista de usuários na função de Administrador de Sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , clique em **Adicionar Novo Administrador** .  
  
 Verifique se o campo **Usuário para provisionamento** lista o NomeDeDomínio\NomeDeUsuário do usuário cujas permissões devem ser atualizadas. Selecione a função que será atualizada na lista de instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no painel **Privilégios disponíveis** e clique na seta à direita. Para adicionar o usuário a todas as funções para todas as instâncias disponíveis das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e todas as funções disponíveis, clique duas vezes na seta à direita.  
  
 Para implementar as alterações quando suas seleções estiverem completas, [!INCLUDE[clickOK](../../includes/clickok-md.md)]. Para encerrar o uso da ferramenta sem fazer alterações, clique em **Cancelar**.  
  
  
