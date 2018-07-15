---
title: Renomear uma instância do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- instances of Analysis Services, renaming
- renaming instances of Analysis Services
- names [Analysis Services], renaming instances
- names [Analysis Services]
ms.assetid: 87494741-4a2e-4fed-8061-418fd1e111c3
caps.latest.revision: 49
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0dfa3a42caf787fad5e8eb64e5bdbab38997640b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37326806"
---
# <a name="rename-an-analysis-services-instance"></a>Renomear uma instância do Analysis Services
  Você pode renomear uma instância existente do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando o **renomear instância** caixa de diálogo.  
  
> [!IMPORTANT]  
>  Na renomeação da instância, a ferramenta Renomeação de Instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é executada com privilégios elevados, atualizando o nome do serviço Windows, contas de segurança e entradas do Registro associados com essa instância. Para garantir a execução dessas ações, execute essa ferramenta como um administrador do sistema local.  
  
 A ferramenta Renomeação de Instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não modifica a pasta de programa que foi criada para a instância original. Não modifique o nome da pasta de programa para coincidir com a instância que você está renomeando. A alteração de um nome de pasta de programa pode impedir o reparo da instalação ou sua desinstalação.  
  
> [!NOTE]  
>  A Ferramenta que renomeia a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não tem suporte para uso em um ambiente de cluster.  
  
### <a name="to-rename-an-instance-of-analysis-services"></a>Para renomear uma instância do Analysis Services  
  
1.  Inicie o **renomeação de instância** ferramenta **asinstancerename.exe**, de C:\Program Files\Microsoft SQL Server\110\Tools\Binn\ManagementStudio.  
  
2.  Na caixa de diálogo **Renomear Instância** , na lista **Instância a ser renomeada** , selecione a instância que você deseja renomear.  
  
3.  Na caixa **Novo nome da instância** , digite o novo nome da instância.  
  
4.  Verifique se o nome de usuário e senha estão corretos e, então, clique em **Renomear**.  
  
     A instância do Analysis Services será interrompida e reiniciará como parte da alteração de nome.  
  
### <a name="post-rename-checklist"></a>Lista de verificação pós-renomeação  
  
1.  Para retomar o acesso a bancos de dados em execução na instância renomeada, atualize as conexões de dados manualmente no Excel ou em outros aplicativos cliente. Também verifique qualquer conexão predefinida, como fontes de dados compartilhadas do Reporting Services, arquivos ODC do Excel ou arquivos de conexão de Modelo Semântico BI que possam referenciar a instância recém-renomeada. Para obter mais informações, consulte [Conectar ao Analysis Services](connect-to-analysis-services.md).  
  
2.  Atualize scripts do PowerShell ou scripts AMO que você costuma usar para fazer backup, sincronizar ou processar bancos de dados.  
  
3.  Atualize propriedades de projeto para projetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] com os quais você trabalha no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Para instâncias de servidor de modo de tabela, atualize a propriedade de Servidor de Espaço de trabalho no arquivo model.bim, assim como a propriedade Servidor no projeto.  
  
4.  Dependendo de como você especificou a conta de serviço, poderá precisar atualizar logons de banco de dados ou permissões de arquivo que concedam ao serviço direitos de acesso a dados (por exemplo, se você usar a conta de serviço para processar dados ou acessar objetos vinculados em outro servidor).  
  
     A atualização de um logon de banco de dados ou de permissões de arquivo será necessária se você tiver usado uma conta virtual para provisionar o serviço. Contas virtuais se baseiam no nome de instância; portanto, se você renomear a instância, a conta virtual também será atualizada ao mesmo tempo. Isso significa que qualquer logon anterior ou permissões criadas para a instância anterior não serão mais válidas.  
  
     O exemplo a seguir ilustra esse cenário. Digamos que você instalou um servidor de modo de tabela como uma instância denominada "Tabelar" usando a conta virtual padrão, resultando na seguinte configuração:  
  
    1.  Nome da instância = \<server > \TABULAR  
  
    2.  Nome de serviço = MSOLAP$TABULAR  
  
    3.  Conta virtual = NT Service\ MSOLAP$TABULAR  
  
     Digamos que você renomeie a instância como "TAB2". Como resultado da alteração de nome, sua configuração teria a seguinte aparência agora:  
  
    1.  Nome da instância = \<server > \TAB2  
  
    2.  Nome de serviço = MSOLAP$TAB2  
  
    3.  Conta virtual = NT Service\ MSOLAP$TAB2  
  
     Como você pode observar, as permissões de banco de dados e de arquivo antes concedidas ao “NT Service\ MSOLAP$TABULAR” não são mais válidas. Para garantir que tarefas e operações realizadas pelo serviço sejam executadas antes, você precisaria conceder novas permissões de banco de dados e de arquivo ao “NT Service\ MSOLAP$TAB2”.  
  
  
