---
title: Instalar, desinstalar e oferecer suporte ao construtor de relatórios | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- administering Report Builder
ms.assetid: 2c9a5814-17bf-4947-8fb3-6269e7caa416
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 939a60c8c23ee59e77f6a2f3c3a2b71a98a426bf
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241714"
---
# <a name="install-uninstall-and-report-builder-support"></a>Instalar, desinstalar e oferecer suporte ao Construtor de Relatórios
  O Construtor de Relatórios é uma ferramenta de criação de relatórios usada para criar, atualizar e compartilhar relatórios, partes de relatório e conjuntos de dados compartilhados. O Construtor de Relatórios está disponível em duas versões: autônoma e [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]. A versão autônoma é instalada no computador por você ou por um administrador. A versão [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] é instalada automaticamente com o [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] e baixada no computador a partir do Gerenciador de Relatórios ou de um site do SharePoint integrado ao [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 A versão autônoma do Construtor de Relatórios não é instalada com o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Baixe e instale-o separadamente do [Construtor de Relatórios do Microsoft® SQL Server® 2012](https://go.microsoft.com/fwlink/?LinkId=401502).  
  
> [!NOTE]  
>  O Construtor de Relatórios não pode ser instalado em computadores baseados no Itanium. Isso se aplica ao [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] e às versões autônomas do Construtor de Relatórios.  
  
 Um administrador normalmente instala e configura o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], concede permissão para usar a versão [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] do Construtor de Relatórios e gerencia pastas e permissões para relatórios, partes de relatório e conjuntos de dados compartilhados salvos no servidor de relatório. Para obter mais informações sobre [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] administração, consulte [servidor de relatório do Reporting Services &#40;nativo&#41; ](report-server/reporting-services-report-server-native-mode.md) na [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [Manuais Online do](https://go.microsoft.com/fwlink/?LinkId=154888) em msdn.microsoft.com.  
  
##  <a name="Installing"></a> Instalando o construtor de relatórios  
 O Construtor de Relatórios está disponível em versões autônoma e [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] . Você ou o administrador baixa e instala a versão autônoma no computador, e a versão [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] é instalada com o [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Você pode baixar o Construtor de Relatórios do [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/?LinkID=186083).  
  
> [!NOTE]  
>  Não é possível instalar o Construtor de Relatórios em computadores baseados no Itanium 64. Isso se aplica ao [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] e às versões autônomas do Construtor de Relatórios.  
  
 Antes de instalar uma versão do Construtor de Relatórios, verifique os requisitos do sistema e instale todos.  
  
### <a name="system-requirements"></a>Requisitos do sistema  
 O Construtor de Relatórios requer que o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] versão 3.5 esteja instalado no computador local. Se o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] não estiver instalado no computador local quando você instalar o Construtor de Relatórios, você será solicitado a instalá-lo para continuar e concluir a instalação:  
  
 O Microsoft .NET Framework 3.5 é gratuito. É possível baixar o .NET Framework 3.5 no [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/?LinkID=110520).  
  
 É possível instalar o Construtor de Relatórios em qualquer sistema operacional [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows com suporte para o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 3.5. Por exemplo, é possível instalar o Construtor de Relatórios no Windows Vista ou no Windows 7.  
  
 É recomendável que os computadores que executarão o Construtor de Relatórios tenham 512 MB de RAM. No entanto, dependendo da complexidade dos relatórios executados, talvez você queira menos ou mais RAM.  
  
### <a name="installing-the-stand-alone-version-of-report-builder-directly-on-your-computer"></a>Instalando a versão autônoma do Construtor de Relatórios diretamente no computador  
 Você instala o Construtor de Relatórios no site de download, [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/?LinkID=186083), ou um administrador cria o arquivo ReportBuilder3.msi, o pacote do Windows Installer do Construtor de Relatórios, disponível em um compartilhamento do qual é possível instalá-lo.  
  
 Também é possível executar uma instalação de linha de comando e incluir opções, como tornar a instalação silenciosa e gravar arquivos de log para a instalação. A documentação do Windows Installer, que executa arquivos .msi, fornece informações sobre as opções disponíveis.  
  
 Para obter mais informações, consulte [instalar a versão de autônoma do construtor de relatórios &#40;construtor de relatórios&#41;](install-windows/install-report-builder.md).  
  
 Um administrador também pode usar software como o SMS (Microsoft Systems Manager Server) para instalar o programa no computador. Para saber como usar software específico para instalar o Construtor de Relatórios, consulte a documentação do software.   
  
### <a name="installing-the-clickonce-version-of-report-builder-on-your-computer"></a>Instalando a versão ClickOnce do Construtor de Relatórios no seu computador  
 A versão [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] do Construtor de Relatórios é instalada com o [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Ela é instalada pelas instalações nativa e integrada do SharePoint do [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)].  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] é uma tecnologia da Microsoft para implantar aplicativos do Windows. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] permite que os usuários instalem e executem um aplicativo Windows, como o Construtor de Relatórios, clicando em um link de uma página da Web. Para obter mais informações sobre como implantar [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos, aplicando [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] segurança do aplicativo, ou execução [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativos na zona da Internet, consulte a "implantação de ClickOnce para Windows Forms aplicativos", "segurança no Visão geral dos Windows Forms"ou"Trusted Application Deployment Overview"artigos sobre o [!INCLUDE[msCoName](../includes/msconame-md.md)] site da Developer Network em [ https://developer.microsoft.com/ ](https://developer.microsoft.com/).  
  
 A versão [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] do Construtor de Relatórios está localizada no servidor de relatório e é instalada no computador quando você clica no botão **Construtor de Relatórios** no Gerenciador de Relatórios ou clica na opção **Relatório do Construtor de Relatórios** no menu **Novo Documento** em uma biblioteca do SharePoint.  
  
> [!NOTE]  
>  Se o menu **Novo Documento** não listar as opções **Relatório do Construtor de Relatórios**, **Modelo do Construtor de Relatórios**e **Fonte de Dados de Relatório** , seus tipos de conteúdo precisarão ser adicionados à biblioteca do SharePoint.   
  
 É possível abrir o Construtor de Relatórios a partir do Gerenciador de Relatórios ou de uma biblioteca do SharePoint. Para obter mais informações sobre como abrir o construtor de relatórios, consulte [iniciar o construtor de relatórios &#40;construtor de relatórios&#41;](report-builder/start-report-builder.md).  
  
### <a name="report-builder-languages"></a>Idiomas do Construtor de Relatórios  
 O Construtor de Relatórios está disponível em 21 idiomas além do inglês. Quando você baixa a versão autônoma do Construtor de Relatórios, escolhe a versão de idioma que deseja instalar. Você deve repetir o download para cada versão de idioma que deseja usar.  
  
 Para a versão [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] , todas as versões de idioma são instaladas no servidor de relatório quando você instala o [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. A cultura do computador do usuário determina a versão instalada. Se a cultura não corresponder a um idioma do Construtor de Relatórios, será instalada a versão em inglês.  
  
 A tabela a seguir contém informações sobre as versões de idioma disponíveis.  
  
|LCID|Idioma|Cultura|  
|----------|--------------|-------------|  
|1028|Chinês (tradicional)|zh-TW|  
|1029|Czech|cs-CZ|  
|1030|Danish|da-DK|  
|1031|German|de-DE|  
|1032|Greek|el-GR|  
|1046|Inglês|pt-BR|  
|1035|Finlandês|fi-FI|  
|1036|Francês|fr-FR|  
|1038|Húngaro|hu-HU|  
|1040|Italiano|it-IT|  
|1041|Japonês|ja-JP|  
|1042|Coreano|ko-KR|  
|1043|Holandês|nl-NL|  
|1044|Norueguês (Bokmal)|nb-NO|  
|1045|Polonês|pl-PLl|  
|1046|Português (Brasil)|pt-BR|  
|1049|Russo|ru-RU|  
|1053|Sueco|sv-SE|  
|1055|Turco|tr-TR|  
|2052|Chinês (simplificado)|zh-CN|  
|2070|Português (Portugal)|pt-PT|  
|3082|Espanhol (Espanha)|es-ES|  
  
  
##  <a name="Uninstalling"></a> Desinstalando o construtor de relatórios  
 É possível desinstalar a versão autônoma do Construtor de Relatórios no painel de controle ou na linha de comando. Isso se aplica apenas à versão autônoma do Construtor de Relatórios. O [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] do Construtor de Relatórios não pode ser desinstalado separadamente. Ele sempre é instalado e desinstalado com o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 Para obter mais informações, consulte [desinstalar a versão de autônoma do construtor de relatórios &#40;construtor de relatórios&#41;](install-windows/uninstall-report-builder.md).  
  
  
##  <a name="Supporting"></a> Dando suporte ao construtor de relatórios  
 Para dar suporte a autores de relatório, um administrador é responsável por gerenciar pastas, relatórios e itens relacionados ao relatório no servidor de relatório, conceder permissão a recursos no servidor de relatório e configurar o servidor de relatório para acesso.  
  
### <a name="folders-reports-and-report-related-items"></a>Pastas, relatórios e itens relacionados ao relatório  
 As pastas, os relatórios e os itens relacionados ao relatório a seguir são gerenciados no servidor de relatório:  
  
-   Pastas nas quais você armazena relatórios, fontes de dados compartilhadas, modelos etc.  
  
-   Meus Relatórios, a pasta particular na qual você armazena os relatórios e itens relacionados ao relatório.  
  
-   Fontes de dados compartilhadas que permitem aos autores de relatórios usar fontes de dados armazenadas externamente a relatórios.  
  
-   Conjuntos de dados compartilhados que podem fornecer dados consultados prontos para uso a vários relatórios para vários usuários.  
  
-   Partes de relatório, como tabelas e gráficos, que permitem aos usuários aprimorar e reutilizar partes de relatório, criados por outras pessoas, em um ambiente de colaboração.  
  
-   Modelos de relatório que podem simplificar e facilitar a obtenção de dados para relatórios de fontes de dados complexas.  
  
-   Imagens como imagens de plano de fundo e logotipos que podem ser usadas em vários relatórios e armazenadas externamente de relatórios tendo em vista uma manutenção mais fácil.  
  
 Para obter mais informações, consulte [gerenciamento de conteúdo de servidor de relatório &#40;modo nativo do SSRS&#41; ](report-server/report-server-content-management-ssrs-native-mode.md) na [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [Manuais Online](https://go.microsoft.com/fwlink/?LinkId=154888) em msdn.microsoft.com.  
  
### <a name="permissions"></a>Permissões  
 O administrador concede permissão para o servidor de relatório. Como usuário do Construtor de Relatórios, você precisa de permissões para o servidor de relatório para poder acessar o conteúdo e a funcionalidade do servidor de relatório. Por exemplo, você talvez queira usar partes de relatório armazenadas no servidor de relatório, atualizar relatórios e salvá-los novamente no servidor de relatório e executar relatórios no Gerenciador de Relatórios. Dependendo das necessidades e das tarefas executadas, permissões mais baixas ou mais altas podem ser concedidas. Por exemplo, permissões com privilégios menores são concedidas a usuários que só precisam abrir relatórios compartilhados, em comparação com usuários que precisam modificar um relatório compartilhado.  
  
 Quando o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] é instalado no modo nativo, um administrador pode:  
  
-   Habilite o recurso Meus Relatórios para criar uma pasta particular e criar e salvar seus próprios relatórios.  
  
-   Use a função Construtor de Relatórios em pastas públicas para poder abrir uma cópia de um relatório compartilhado e salvar uma versão modificada em uma pasta particular.  
  
-   Use a função Publicador para permitir gerenciar relatórios e fontes de dados compartilhadas em pastas públicas. Essa função é concedida a usuários mais experientes.  
  
 Quando o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] é instalado no modo integrado do SharePoint, um administrador pode:  
  
-   Usar o nível de permissão de leitura, concedido por padrão ao grupo Visitantes, para permitir a abertura de uma cópia de um relatório em uma pasta pública e salvar a versão modificada do relatório em uma pasta particular ou no computador.  
  
-   Usar o nível de permissão de contribuição, concedido por padrão aos grupos Membros, para permitir o gerenciamento de relatórios e fontes de dados compartilhadas em pastas públicas. Esse nível de permissão é concedido a usuários mais experientes.  
  
 Para obter informações gerais sobre permissões e criação e uso de funções, consulte a documentação do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] nos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [do](https://go.microsoft.com/fwlink/?LinkId=154888) em msdn.microsoft.com.  
  
### <a name="configuration-of-report-server"></a>Configuração do servidor de relatório  
 Ao criar relatórios no Construtor de Relatórios e se conectar a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instalada no Windows Vista, no Windows Server 2008 ou no Windows 7, você talvez encontre um erro de acesso negado ao tentar acessar o servidor de relatório para abrir ou salvar um relatório. Isso ocorre porque o recurso de segurança, UAC (Controle de Conta de Usuário), no Windows Vista, no Windows Server 2008 e no Windows 7, limita o uso excessivo de permissões elevadas, removendo as permissões de administrador no acesso a aplicativos.  
  
 No entanto, com uma configuração adicional, o servidor de relatório é disponibilizado para usuários do Construtor de Relatórios. É possível adicionar URLs do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] a sites confiáveis. Por padrão, o Internet Explorer 7.0 ou posterior é executado no Modo Protegido no Windows Vista, no Windows Server 2008 e no Windows 7. O Modo Protegido é um recurso que impede que solicitações do navegador alcancem processos de nível superior executados no mesmo computador. Você pode desabilitar o modo protegido para os aplicativos do servidor de relatório adicionando-os como Sites Confiáveis. Você deve ter permissão de administrador para fazer essa alteração.  
  
 Para obter mais informações sobre como configurar [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], consulte [Reporting Services Configuration Manager &#40;/DEL&#41; ](/sql/2014/sql-server/install/reporting-services-configuration-manager-native-mode) no [documentação do Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) em msdn.microsoft.com.  
  
  
##  <a name="SampleDatabases"></a> Bancos de dados de exemplo do SQL Server  
 A família Adventure Works de bancos de dados de exemplo oferece dados que você pode usar para aprender a criar relatórios e a escrever relatórios de exemplo.  
  
 Os bancos de dados estão disponíveis nas seguintes versões:  
  
-   O banco de dados Adventure Works OLTP dá suporte a cenários de processamento de transações online padrão de um fabricante de bicicletas fictício (Adventure Works Cycles). Os cenários incluem Produção, Vendas, Compras, Gerenciamento de Produtos, Gerenciamento de Contatos e Recursos Humanos.  
  
-   O banco de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] demonstra como criar um data warehouse.  
  
-   O projeto [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] pode ser usado para criar um banco de dados AS para cenários de business intelligence.  
  
 Os bancos de dados de exemplo não são incluídos no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e não são instalados quando você instala o [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] ou a versão autônoma do Construtor de Relatórios. Você baixa bancos de dados de exemplo do [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843). Todas as versões dos bancos de dados de exemplo são baixadas juntas. Também é possível baixar versões anteriores do banco de dados que foram lançadas com o [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], o [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]e o [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)].  
  
 Para obter os pré-requisitos e as instruções sobre como baixar e instalar os bancos de dados de exemplo do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] , consulte os [pré-requisitos de instalação dos bancos de dados de exemplo do SQL Server 2008](https://go.microsoft.com/fwlink/?LinkId=166648) e a [instalação de bancos de dados de exemplos](https://go.microsoft.com/fwlink/?LinkId=166649) no CodePlex.  
  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 Esta seção lista procedimentos que mostram como instalar e desinstalar o Construtor de Relatórios.  
  
 [Instalar a versão autônoma do construtor de relatórios &#40;construtor de relatórios&#41;](install-windows/install-report-builder.md)  
  
 [Desinstalar a versão autônoma do construtor de relatórios &#40;construtor de relatórios&#41;](install-windows/uninstall-report-builder.md)  
  
 [Iniciar o construtor de relatórios &#40;construtor de relatórios&#41;](report-builder/start-report-builder.md)  
  
  
## <a name="see-also"></a>Consulte também  
 [Construtor de Relatórios no SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
