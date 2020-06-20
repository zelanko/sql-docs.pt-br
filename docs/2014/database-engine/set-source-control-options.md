---
title: Definir opções de controle do código-fonte | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Source_Control.Visual_SourceSafe
- VS.ToolsOptionsPages.Source_Control.General
- VS.ToolsOptionsPages.Source_Control.Environment
helpviewer_keywords:
- source controls [SQL Server Management Studio], options
ms.assetid: b2c6ca00-46f0-4f86-b067-07bae779c147
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5ab6d134177c7861c3a8f92cf767c71c0b56e233
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929097"
---
# <a name="set-source-control-options"></a>Definir opções de controle do código-fonte
  Antes de poder se beneficiar dos recursos internos de controle do código-fonte do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], é necessário configurar as opções de controle do código-fonte dos vários ambientes em que você trabalha.  
  
 Configure as opções de controle do código-fonte usando a caixa de diálogo **Opções** para configurar uma ou mais funções de controle do código-fonte. Uma função consiste em uma descrição geral da configuração em que você usa o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]e as opções de controle do código-fonte associadas com aquela configuração.  
  
 Por exemplo, se você for um desenvolvedor de banco de dados independente, em geral não criará conflitos com outros usuários, mantendo arquivos que passaram pelo check-out após seu check-in Por conseguinte, o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] define uma função de desenvolvedor independente. Para essa função, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] seleciona automaticamente a opção **manter itens com check-out ao fazer check-in** .  
  
 Como é possível definir e personalizar funções, você pode trabalhar em várias configurações de desenvolvimento sem ter que reconfigurar totalmente o controle do código-fonte sempre que alternar de uma configuração para outra.  
  
### <a name="to-set-source-control-options"></a>Para definir opções de controle do código-fonte  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , expanda **controle do código-fonte**e clique na página **seleção de plug-in** .  
  
     **Plug-in atual de controle de código-fonte**  
     Selecione nesta lista o controle do código-fonte que você deseja usar. O cliente de produto de controle do código-fonte deve ser instalado neste computador para que apareça na lista. Se nenhum cliente de controle do código-fonte for instalado no computador, a única seleção disponível será Nenhum. Se você instalou Microsoft Source Safe, então os seguinte plug ins são exibidos:  
  
    -   Microsoft Visual SourceSafe  
  
    -   Microsoft Visual SourceSafe (Internet)  
  
3.  Defina credenciais de logon para cada função de controle do código-fonte que você quiser usar. Esta página só estará disponível se um plug-in de controle do código-fonte estiver instalado.  
  
     **Descrição da função**  
     Selecionar uma dessas funções faz com que as opções de controle do código-fonte apropriadas sejam automaticamente selecionadas.  
  
    |Função|Descrição|  
    |----------|-----------------|  
    |**Visual SourceSafe**|Especifica que você deseja usar as configurações usadas com mais frequência pelos [!INCLUDE[msCoName](../includes/msconame-md.md)] usuários do Visual SourceSafe.|  
    |**Desenvolvedor Independente**|Especifica que você está trabalhando independentemente.|  
    |**Personalizado**|Especifica que você modificou as configurações para uma função.|  
  
     **Executar atualizações de status em plano de fundo**  
     Atualiza automaticamente os ícones de sinalização do controle do código fonte no Gerenciador de Soluções conforme o status de um item é alterado. Se você constatar atrasos ao executar operações que exijam muito do servidor, especialmente ao abrir uma solução ou projeto do controle do código fonte, tente desmarcar essa caixa de seleção, pois isso pode melhorar o desempenho.  
  
     **ID de Logon**  
     Especifica o nome de usuário a usar para fazer o logon no provedor de controle do código-fonte. Se houver suporte do seu provedor de controle do código-fonte, esse nome será preenchido automaticamente na caixa de diálogo de **logon** para acessar o servidor de controle do código-fonte. Para tornar ativa essa opção, desabilite os logons de usuário automáticos usando o programa de administrador do provedor do controle do código fonte e, depois, reinicie o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
     **Avançado**  
     Exibe opções adicionais para adicionar itens ao controle do código fonte. Essas opções variam, dependendo de seu provedor de controle do código fonte. A ajuda para essas opções é fornecida pelo programa de controle do código fonte.  
  
4.  Selecione a página **ambiente** .  
  
5.  Na caixa **configurações de ambiente de controle do código-fonte** , selecione a função na qual você deseja definir as opções de controle do código-fonte.  
  
     O [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] seleciona automaticamente as opções padrão de controle do código-fonte da função selecionada. Se você desmarcar qualquer uma das opções padrão, a caixa **configurações do ambiente de controle do código-fonte** exibirá a opção **personalizado** para indicar que você personalizou a função originalmente selecionada.  
  
     **Configurações de Ambiente de Controle do Código Fonte**  
     Especifica a função que você deseja usar. O [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] define as seguintes funções.  
  
    |Função|Descrição|  
    |----------|-----------------|  
    |**Visual SourceSafe**|Especifica que você deseja usar as configurações usadas com mais frequência pelos [!INCLUDE[msCoName](../includes/msconame-md.md)] usuários do Visual SourceSafe.|  
    |**Desenvolvedor Independente**|Especifica que você está trabalhando independentemente.|  
    |**Personalizado**|Especifica que você modificou as configurações para uma função.|  
  
     Selecionar uma dessas funções faz com que as opções de controle do código-fonte apropriadas sejam automaticamente selecionadas.  
  
     **Manter itens que passaram pelo check out ao fazer o check-in**  
     Especifica que ao fazer o check-in de itens para atualizar o armazenamento de controle do código fonte, os itens devem permanecer com o check-out aplicado para você. Se você quiser alterar essa opção para um check-in específico, clique na seta **Opções** na caixa de diálogo **check-in** e desmarque a caixa de seleção **manter check-out** .  
  
     **Itens verificados**  
     Exibe uma lista de opções que especificam como o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] deve se comportar quando você tenta editar um item cujo check-out não foi feito. As tabelas a seguir descrevem as opções disponíveis.  
  
     **Tentando**  
  
    |Ação|Descrição|  
    |------------|-----------------|  
    |**Prompt para check out**|Exibe a caixa de diálogo **check-out** .|  
    |**Executar check out automaticamente**|Faz o check-out do item sem exibir a caixa de diálogo **check-out** . Essa é a opção padrão.|  
    |**Salvar como**|Salva como um arquivo novo.|  
  
     **Edição**  
  
    |Ação|Descrição|  
    |------------|-----------------|  
    |**Prompt para check out**|Exibe a caixa de diálogo **check-out** .|  
    |**Prompt para check outs exclusivos**|Exibe a caixa de diálogo **check-out** .|  
    |**Executar check out automaticamente**|Faz o check-out do item sem exibir a caixa de diálogo **check-out** . Essa é a opção padrão.|  
    |**Não fazer nada**|Não verifica o arquivo.|  
  
     **Permita a edição de itens verificados**  
     Especifica que itens cujo check-in é executado podem ser editados na memória. Se você marcar essa caixa de seleção, um botão **Editar** será exibido na caixa de diálogo **check-out** quando você tentar editar um item com check-in. Depois de clicar nesse botão, é possível editar o item. Se tentar salvar o item, você deve fazer o check out ou salvá-lo em um local diferente.  
  
     **Redefinir**  
     Reajusta caixas de diálogo de confirmação de controle do código-fonte para suas configurações padrão. Por exemplo, se você tiver selecionado a caixa de seleção **não mostrar esta dialogo novamente** em uma caixa de diálogo controle do código-fonte, a seleção da opção **Redefinir** inverterá essa ação.  
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas do controle do código-fonte](../../2014/database-engine/source-control-basics.md)   
 [Alterar conexões de controle do código-fonte](../../2014/database-engine/change-source-control-connections.md)   
 [Excluir arquivos do controle do código-fonte](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
