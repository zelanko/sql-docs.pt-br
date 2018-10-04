---
title: Use o Supervisor de atualização para preparar para atualizações | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server]
- upgrading SQL Server, Upgrade Advisor
- upgrading SQL Server, preparing to upgrade
- SQL Server Upgrade Advisor
- analyzing installations for upgrading [SQL Server]
ms.assetid: d85b0833-ddeb-42e3-9397-97ea60d521b7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c8ade9c0d0d877ca1c12c1361e0e0ba45c2e7ecb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209286"
---
# <a name="use-upgrade-advisor-to-prepare-for-upgrades"></a>Usar o Supervisor de Atualização para preparar para atualizações
  O Supervisor de Atualização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajuda você a se preparar para atualizações do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. O Supervisor de Atualização analisa os componentes instalados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gera um relatório que identifica os problemas a serem corrigidos antes ou depois da atualização.  
  
## <a name="how-upgrade-advisor-works"></a>Como o Supervisor de Atualização funciona  
 Quando você executar o Supervisor de atualização, a página inicial do Supervisor de atualização é exibida. Na página inicial, você pode executar as seguintes ferramentas:  
  
-   Assistente para Análise do Supervisor de Atualização  
  
-   Visualizador de Relatórios do Supervisor de Atualização  
  
-   Tópicos da Ajuda do Supervisor de Atualização  
  
 Ao usar o Supervisor de Atualização pela primeira vez, execute o Assistente para Análise do Supervisor de Atualização a fim de analisar os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando o assistente concluir a análise, exiba os relatórios resultantes no Visualizador de Relatórios do Supervisor de Atualização. Cada relatório fornece links para informações na Ajuda do Supervisor de Atualização que ajudarão a corrigir ou reduzir o efeito dos problemas conhecidos.  
  
## <a name="upgrade-advisor-analysis"></a>Análise do Supervisor de Atualização  
 O Supervisor de Atualização analisa os seguintes componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
 A análise examina os objetos que podem ser acessados, como scripts, procedimentos armazenados, gatilhos e arquivos de rastreamento. O Supervisor de Atualização não pode analisar aplicativos da área de trabalho ou procedimentos armazenados criptografados.  
  
 A saída é feita no formato de um relatório XML. Exiba o relatório XML usando o Visualizador de Relatórios do Supervisor de Atualização.  
  
> [!NOTE]  
>  Os relatórios podem conter um item "outros problemas de atualização". Esse item é vinculado a uma lista de problemas que não são detectados pelo Supervisor de Atualização, mas que podem existir em seu servidor ou em seus aplicativos. Você deve revisar a lista de problemas não detectáveis e determinar se deve alterar seu servidor ou seus aplicativos devido aos problemas não detectáveis.  
  
## <a name="how-to-install-and-run-upgrade-advisor"></a>Como instalar e executar o Supervisor de Atualização  
 O local onde você instala o Aconselhador de Atualização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] depende do que você irá analisar. O Supervisor de Atualização dá suporte à análise remota de todos os componentes com suporte, exceto o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se não estiver examinando instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você poderá instalar o Supervisor de Atualização em qualquer computador que possa se conectar à sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e que atenda aos pré-requisitos do Supervisor de Atualização. Para obter mais informações, consulte [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md). Se você estiver verificando instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], será necessário instalar o Supervisor de Atualização no servidor de relatório.  
  
 O Supervisor de Atualização está disponível em um pacote de recursos.  
  
 Pré-requisitos para instalar e executar o Supervisor de atualização são da seguinte maneira:  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2, Windows 7 SP1 e [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1.  
  
-   Windows Installer desde a versão 4.5. Você pode instalar o Windows Installer a partir de [site da Web do Windows Installer](http://go.microsoft.com/fwlink/?LinkId=49112).  
  
-   Microsoft .NET Framework 4. .NET framework 4 está disponível na [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mídia do produto e para o [página de download do .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=209895).  
  
    -   Para instalar o .NET Framework 4 a partir da mídia do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], localize a raiz da unidade de disco. Clique duas vezes nas pastas \redist e DotNetFrameworks; execute o dotNetFx40_Full_x86_x64.exe (para sistemas operacionais de 32 ou 64 bits).  
  
 Para instalar o Supervisor de Atualização a partir da Web, clique no botão de download na página de download. Você poderá executar a instalação imediatamente ou salvar o arquivo SQLUA.msi para execução posterior. Se você estiver instalando de disco do produto, execute sqlua. msi diretamente no disco do produto.  
  
 Depois de instalar o Supervisor de atualização, você poderá abri-lo partir o **iniciar** menu:  
  
-   Clique em **inicie**, aponte para **todos os programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]e, em seguida, clique em  **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Supervisor de atualização**.  
  
 Para obter mais informações, consulte a documentação do Supervisor de Atualização incluída no download do Supervisor de Atualização e nas Notas de Versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com várias versões e instâncias do SQL Server](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)   
 [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Compatibilidade com versões anteriores](../../../2014/getting-started/backward-compatibility.md)  
  
  
