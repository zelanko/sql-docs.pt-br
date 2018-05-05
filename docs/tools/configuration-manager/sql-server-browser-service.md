---
title: Serviço navegador do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.browseservers.local.f1
- sql13.swb.browseservers.network.f1
helpviewer_keywords:
- services [SQL Server], security
- SQL Browser service (See SQL Server Browser Service)
- Browser Service
- SQL Server Browser service
ms.assetid: 3cc00d3a-487c-4cd9-a155-655f02485fa0
caps.latest.revision: 61
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e60d4a23373ecd3ecb92540de4f8e6893482990a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-browser-service"></a>SQL Server Browser Service
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  O programa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser é executado como um serviço Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta as solicitações de entrada de recursos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fornece informações sobre as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas no computador. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Browser contribui para as seguintes ações:  
  
-   Navegando em uma lista de servidores disponíveis  
  
-   Conectando-se à instância de servidor correta  
  
-   Conectando-se aos pontos de extremidade da conexão de administrador dedicada (DAC)  
  
 Para cada instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e do [!INCLUDE[ssAS](../../includes/ssas-md.md)], o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (sqlbrowser) fornece o nome da instância e o número da versão. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Browser é instalado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Browser pode ser configurado durante a instalação ou por meio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Por padrão, o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado automaticamente:  
  
-   Quando uma instalação é atualizada.  
  
-   Quando um cluster é instalado.  
  
-   Quando uma instância nomeada do [!INCLUDE[ssDE](../../includes/ssde-md.md)] é instalada, inclusive todas as instâncias do SQL Server Express.  
  
-   Quando uma instância nomeada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]é instalada.  
  
## <a name="background"></a>Plano de fundo  
 Antes do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], somente uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderia ser instalada em um computador. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ouviu as solicitações de entrada na porta 1433, atribuídas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pela IANA (Internet Assigned Numbers Authority) oficial. Apenas uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar uma porta; por isso, quando o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] introduziu suporte para várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o protocolo SSRP ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol) foi desenvolvido para escutar na porta UDP 1434. Esse serviço de escuta respondia a solicitações de clientes com o nome das instâncias instaladas e as portas ou pipes nomeados utilizados pela instância. Para resolver as limitações de sistema do SSRP, o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduziu o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como um substituto para o SSRP.  
  
## <a name="how-sql-server-browser-works"></a>Como funciona o SQL Server Browser  
 Quando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for iniciada, se o protocolo TCP/IP estiver habilitado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], será atribuída uma porta TCP/IP ao servidor. Se o protocolo Pipes Nomeados estiver habilitado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escutará um determinado pipe nomeado. Essa porta, ou "pipe", será utilizado por aquela instância específica para trocar dados com os aplicativos clientes. Durante a instalação, a porta 1433 no TCP e o pipe `\sql\query` são atribuídos à instância padrão, mas esses podem ser alterados posteriormente pelo administrador de servidor usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Devido a apenas uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poder usar uma porta ou um pipe, diferentes números de porta e nomes de pipe são atribuídos a instâncias nomeadas, inclusive o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Por padrão, quando habilitado, ambas as instâncias nomeadas e o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] são configurados para usar portas dinâmicas, ou seja, será atribuída uma porta disponível quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for iniciado. Se você desejar, pode-se atribuir uma porta específica a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ao se conectar, os clientes podem determinar uma porta específica, mas se a porta for atribuída dinamicamente, o número da porta poderá ser alterado a qualquer momento em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for reinicializado. Portanto, o número correto da porta será desconhecido para o cliente.  
  
 Na inicialização, o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado e reivindica a porta UDP 1434. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Browser lê o Registro, identifica todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador e anota as portas e os pipes nomeados utilizados. Quando um servidor tiver dois ou mais cartões de rede, o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará para a primeira porta habilitada que encontrar do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Browser dá suporte ao IPv6 e IPv4.  
  
 Quando clientes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicitam recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a biblioteca de rede do cliente envia uma mensagem UDP para o servidor utilizando a porta 1434. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Browser responde com a porta TCP/IP ou o pipe nomeado da instância solicitada. Em seguida, a biblioteca de rede no aplicativo cliente completa a conexão, enviando uma solicitação ao servidor utilizando a porta ou o pipe nomeado da instância desejada.  
  
 Para obter informações sobre como iniciar e interromper o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="using-sql-server-browser"></a>Utilizando o SQL Server Browser  
 Se o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver sendo executado, você ainda poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , caso forneça o número correto da porta ou o pipe nomeado. Por exemplo, você poderá se conectar à instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o TCP/IP se ele estiver sendo executado na porta 1433.  
  
 Porém, se o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver sendo executado, as seguintes conexões não funcionarão:  
  
-   Qualquer componente que tente conectar-se a uma instância nomeada sem especificar completamente todos os parâmetros (como a porta do TCP/IP ou o pipe nomeado).  
  
-   Qualquer componente que gere ou passe informações de servidor\instância que possa ser utilizada posteriormente por outros componentes para se reconectar.  
  
-   Conectando-se a uma instância nomeada sem fornecer o número da porta ou pipe.  
  
-   Uma DAC para uma instância nomeada ou para uma instância padrão se não utilizar a porta 1433 do TCP/IP.  
  
-   O serviço redirecionador do OLAP (Online Analytical Processing).  
  
-   Enumerar servidores no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no Enterprise Manager ou no Query Analyzer.  
  
 Se você estiver usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um cenário cliente-servidor (por exemplo, quando seu aplicativo estiver acessando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por uma rede), caso você pare ou desabilite o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você deverá atribuir um número de porta específico a cada instância e gravar seu código de aplicativo cliente para sempre usar aquele número de porta. Esta abordagem tem os seguintes problemas:  
  
-   Você deve atualizar e manter o código de aplicativo cliente para assegurar que ele se conectará à porta correta.  
  
-   A porta que você escolhe para cada instância pode ser utilizada por outro serviço ou aplicativo no servidor, tornando a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indisponível.  
  
## <a name="clustering"></a>Clustering  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Browser não é um recurso clusterizado e não dá suporte ao failover de um nó de cluster para outro. Portanto, no caso de um cluster, o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser instalado e ativado para cada nó do cluster. Em clusters, o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta em IP_ANY.  
  
> [!NOTE]  
>  Quando escutar em IP_ANY e habilitar a escuta em IPs específicos, o usuário deverá configurar a mesma porta do TCP em cada IP, pois o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna ao primeiro par de IP/porta que ele encontrar.  
  
## <a name="installing-uninstalling-and-running-from-the-command-line"></a>Instalando, desinstalando e executando a partir da linha de comandos  
 Por padrão, o programa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser é instalado em C:\Arquivos de Programas (x86)\Microsoft SQL Server\90\Shared\sqlbrowser.exe.  
  
 O serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será desinstalado quando a última instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for removida.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Browser pode ser iniciado no prompt de comando para a solução de problemas por meio da opção **-c** :  
  
```  
<drive>\<path>\sqlbrowser.exe -c  
```  
  
## <a name="security"></a>Segurança  
  
### <a name="account-privileges"></a>Privilégios da conta  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Browser escuta em uma porta UDP e aceita as solicitações não autenticadas usando o protocolo SSRP ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Browser deve ser executado no contexto de segurança de um usuário com privilégios baixos para minimizar exposição a um ataque mal-intencionado. A conta de logon pode ser alterada com o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os direitos mínimos do usuário para o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são os seguintes:  
  
-   Negar acesso a este computador pela rede  
  
-   Negar logon localmente  
  
-   Negar logon como um trabalho em lotes  
  
-   Negar Logon pelos Serviços de Terminal  
  
-   Fazer logon como um serviço  
  
-   Ler e gravar as chaves do Registro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relacionadas à comunicação de rede (portas e pipes)  
  
### <a name="default-account"></a>Conta padrão  
 O programa de instalação configura o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usar durante a instalação, a conta selecionada para serviços. Outras contas possíveis incluem:  
  
-   Qualquer conta **domínio\localização**  
  
-   A conta de **serviço local**  
  
-   A conta **sistema local** (não recomendada por ter privilégios desnecessários)  
  
### <a name="hiding-sql-server"></a>Ocultando o SQL Server  
 As instâncias ocultas são instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que dão suporte apenas a conexões de memória compartilhada. Para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], defina o sinalizador de `HideInstance` para indicar que o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não deve responder com informações sobre essa instância de servidor.  
  
### <a name="using-a-firewall"></a>Usando um firewall  
 Para comunicar-se com o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um servidor por trás de um firewall, abra a porta UDP 1434, além da porta TCP usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por exemplo, 1433). Para obter informações sobre como trabalhar com um firewall, consulte "Como configurar um firewall para acessar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] " nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Protocolos de rede e bibliotecas de rede](../../sql-server/install/network-protocols-and-network-libraries.md)  
  
  
