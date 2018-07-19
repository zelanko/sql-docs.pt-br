---
title: Como instalar e gerenciar extensões de recurso | Microsoft Docs
ms.custom:
- SSDT
ms.date: 04/26/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9cdc8cd5-c36f-4bee-a191-87ed457803e7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b3d6d4c85a287dc000d761df1eafeb49e4261336
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093608"
---
# <a name="how-to-install-and-manage-feature-extensions"></a>Como instalar e gerenciar extensões de recurso
Você pode adicionar regras para a análise de código do banco de dados, condições para testes de unidade de banco de dados e colaboradores de criação/implantação para aumentar a funcionalidade que as edições do Visual Studio, que incluem o SQL Server Data Tools, oferecem. No entanto, você deve primeiro instalar uma extensão de recurso antes de poder usá-la, se criou a extensão ou instalou uma que outra pessoa criou.  
  
O local onde sua extensão será instalada depende do tipo de extensão e de onde você pretende usá-la. Nas últimas edições do Visual Studio, o local de instalação de alguns componentes foi movido do diretório de instalação do SQL Server para dentro do diretório do Visual Studio. Essa configuração facilita ter diferentes versões do software em execução lado a lado, mas significa que você talvez precise instalar sua extensão em vários locais, se desejar usá-la em outra versão do SQL Server Data Tools e na linha de comando.  
  
### <a name="installing-extensions-for-use-inside-visual-studio"></a>Instalar extensões para uso dentro do Visual Studio  
  
|Tipo de extensão|Local de instalação|  
|------------------|--------------------|  
|Condição de teste personalizado para testes de unidade do SQL Server|<Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\TestConditions|  
|Colaboradores de compilação<br /><br />Colaboradores de implantação<br /><br />Regras de análise de código estático|<Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120\Extensions|  
  
O <Visual Studio Install Dir> varia dependendo da versão do Visual Studio que você está usando e de onde você escolheu instalá-lo. Para o Visual Studio 2012, geralmente será C:\Arquivos de Programas (x86)\\MicrosoftVisual Studio 11.0. Para o Visual Studio 2013, geralmente será C:\Arquivos de Programas (x86)\\MicrosoftVisual Studio 12.0.  
  
As extensões podem ser executadas como parte dos nossos serviços de linha de comando:  
  
|Tipo de extensão|Serviço da linha de comando|Pasta de instalação|  
|------------------|------------------------|------------------|  
|Condição de teste personalizado para testes de unidade do SQL Server|MSBuild / MSTest pode ser usado para executar testes de unidade no Prompt de Comando do Desenvolvedor para o Visual Studio 2013 e Ferramentas de linha de comando semelhantes.|A mesma de quando estiver sendo executado dentro do Visual Studio.|  
|Colaboradores de compilação<br /><br />Colaboradores de implantação|[SqlPackage.exe](../tools/sqlpackage.md), ou usando os destinos Implantar ou Publicar do MSBuild ao criar um projeto de banco de dados.|MSBuild: a mesma de quando estiver sendo executado dentro do Visual Studio.<br /><br />[SqlPackage.exe](../tools/sqlpackage.md): se localizado dentro do diretório do Visual Studio, a mesma que antes.<br /><br />Se o SqlPackage.exe e outras DLLs DacFx estiverem localizados fora desse diretório, as extensões devem ser incluídas no mesmo diretório ou em C:\Arquivos de Programas (x86)\\MicrosoftSQL Server\120\DAC\bin\Extensions.|  
|Regras de análise de código estático|O MSBuild pode ser usado para criar o projeto e executar análise de código estático.<br /><br />Além disso, você pode executar a análise de código usando uma API CodeAnalysisService de seus próprios aplicativos. Nesse caso, as regras de pesquisa de extensão funcionam da mesma forma como quando SqlPackage.exe é usado.|O mesmo ocorre para os Colaboradores de Compilação e Implantação|  
  
> [!NOTE]  
> Você deve ter permissões de administrador no seu computador para acessar qualquer um dos diretórios de instalação na pasta Arquivos de Programas. Se você não tiver as permissões apropriadas, contate o administrador de rede.  
  
**Considerações sobre segurança**  
  
Antes de instalar uma extensão que não criou, você deverá entender os seguintes riscos:  
  
-   O programa de instalação para a extensão pode ser malicioso e obter acesso a recursos protegidos baseado nas suas permissões de instalação.  
  
-   A própria extensão pode ser maliciosa e obter controle de recursos protegidos se quem usar a extensão tiver permissões suficientes.  
  
Para minimizar o risco, você deverá instalar uma extensão somente se for de uma origem conhecida. Se você obtiver uma extensão de uma origem não confiável, deverá inspecionar o código-fonte para essa extensão e seu programa de instalação (se houver) antes de instalá-la e usá-la.  
  
## <a name="to-install-a-custom-feature-extension"></a>Para instalar uma extensão de recurso personalizada  
Copie o assembly assinado (.dll) para a pasta de instalação correta. Feche e reabra o Visual Studio. Agora, a extensão deve estar disponível.  
  
## <a name="see-also"></a>Consulte Também  
[Estender os recursos de banco de dados](../ssdt/extending-the-database-features.md)  
  
