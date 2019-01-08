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
manager: craigg
ms.openlocfilehash: 0a654932689785d96aaff049551faf19494c311a
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53589890"
---
# <a name="set-source-control-options"></a>Definir opções de controle do código-fonte
  Antes de poder se beneficiar dos recursos internos de controle do código-fonte do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], é necessário configurar as opções de controle do código-fonte dos vários ambientes em que você trabalha.  
  
 Configurar opções de controle do código-fonte usando o **opções** caixa de diálogo para configurar um ou mais funções de controle do código-fonte. Uma função consiste em uma descrição geral da configuração em que você usa o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]e as opções de controle do código-fonte associadas com aquela configuração.  
  
 Por exemplo, se você for um desenvolvedor de banco de dados independente, em geral não criará conflitos com outros usuários, mantendo arquivos que passaram pelo check-out após seu check-in Por conseguinte, o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] define uma função de desenvolvedor independente. Para esta função, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] seleciona automaticamente o **manter itens com check-ao fazer check-in** opção.  
  
 Como é possível definir e personalizar funções, você pode trabalhar em várias configurações de desenvolvimento sem ter que reconfigurar totalmente o controle do código-fonte sempre que alternar de uma configuração para outra.  
  
### <a name="to-set-source-control-options"></a>Para definir opções de controle do código-fonte  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  No **opções** diálogo caixa, expanda **controle do código-fonte**e, em seguida, clique no **seleção de plug-in** página.  
  
     **Controle de origem atual plug-in**  
     Selecione nesta lista o controle do código-fonte que você deseja usar. O cliente de produto de controle do código-fonte deve ser instalado neste computador para que apareça na lista. Se nenhum cliente de controle do código-fonte for instalado no computador, a única seleção disponível será Nenhum. Se você instalou Microsoft Source Safe, então os seguinte plug ins são exibidos:  
  
    -   Microsoft Visual SourceSafe  
  
    -   Microsoft Visual SourceSafe (Internet)  
  
3.  Defina credenciais de logon para cada função de controle do código-fonte que você quiser usar. Esta página só estará disponível se um plug-in de controle do código-fonte estiver instalado.  
  
     **Descrição da função**  
     Selecionar uma dessas funções faz com que as opções de controle do código-fonte apropriadas sejam automaticamente selecionadas.  
  
    |Role|Descrição|  
    |----------|-----------------|  
    |**Visual SourceSafe**|Especifica que você deseja usar as configurações mais comumente usadas pelo [!INCLUDE[msCoName](../includes/msconame-md.md)] usuários do Visual SourceSafe.|  
    |**Desenvolvedor independente**|Especifica que você está trabalhando independentemente.|  
    |**Custom**|Especifica que você modificou as configurações para uma função.|  
  
     **Executar atualizações de status do plano de fundo**  
     Atualiza automaticamente os ícones de sinalização do controle do código fonte no Gerenciador de Soluções conforme o status de um item é alterado. Se você constatar atrasos ao executar operações que exijam muito do servidor, especialmente ao abrir uma solução ou projeto do controle do código fonte, tente desmarcar essa caixa de seleção, pois isso pode melhorar o desempenho.  
  
     **ID de Logon**  
     Especifica o nome de usuário a usar para fazer o logon no provedor de controle do código-fonte. Se seu provedor de controle de origem tiver suporte, esse nome será preenchido automaticamente na **Login** caixa de diálogo para alcançar o servidor de controle de origem. Para tornar ativa essa opção, desabilite os logons de usuário automáticos usando o programa de administrador do provedor do controle do código fonte e, depois, reinicie o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
     **Avançado**  
     Exibe opções adicionais para adicionar itens ao controle do código fonte. Essas opções variam, dependendo de seu provedor de controle do código fonte. A ajuda para essas opções é fornecida pelo programa de controle do código fonte.  
  
4.  Selecione o **ambiente** página.  
  
5.  No **as configurações de ambiente de controle do código-fonte** , selecione a função na qual você deseja definir as opções de controle de origem.  
  
     O [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] seleciona automaticamente as opções padrão de controle do código-fonte da função selecionada. Se você desmarcar qualquer uma das opções padrão, o **as configurações de ambiente de controle do código-fonte** caixa exibe a **personalizado** opção para indicar que você personalizou a função selecionada originalmente.  
  
     **Configurações de ambiente de controle do código-fonte**  
     Especifica a função que você deseja usar. O [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] define as seguintes funções.  
  
    |Role|Descrição|  
    |----------|-----------------|  
    |**Visual SourceSafe**|Especifica que você deseja usar as configurações mais comumente usadas pelo [!INCLUDE[msCoName](../includes/msconame-md.md)] usuários do Visual SourceSafe.|  
    |**Desenvolvedor independente**|Especifica que você está trabalhando independentemente.|  
    |**Custom**|Especifica que você modificou as configurações para uma função.|  
  
     Selecionar uma dessas funções faz com que as opções de controle do código-fonte apropriadas sejam automaticamente selecionadas.  
  
     **Manter itens com check-ao fazer check-in**  
     Especifica que ao fazer o check-in de itens para atualizar o armazenamento de controle do código fonte, os itens devem permanecer com o check-out aplicado para você. Se você deseja alterar esta opção para um check-in específico, clique no **opções** seta na **Check-in** caixa de diálogo e desmarque o **mantenha check-out** caixa de seleção.  
  
     **Itens com check-in**  
     Exibe uma lista de opções que especificam como o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] deve se comportar quando se tentar editar um item cujo check out não tenha sido feito.  As tabelas a seguir descrevem as opções disponíveis.  
  
     **Salvando**  
  
    |Ação|Descrição|  
    |------------|-----------------|  
    |**Prompt para check-out**|Exibe a **Check-Out** caixa de diálogo.|  
    |**Fazer check-out automaticamente**|Verifica o item sem exibir o **Check-Out** caixa de diálogo. Essa é a opção padrão.|  
    |**Salvar como**|Salva como um arquivo novo.|  
  
     **Edição**  
  
    |Ação|Descrição|  
    |------------|-----------------|  
    |**Prompt para check-out**|Exibe a **Check-Out** caixa de diálogo.|  
    |**Prompt para check outs exclusivos**|Exibe a **Check-Out** caixa de diálogo.|  
    |**Fazer check-out automaticamente**|Verifica o item sem exibir o **Check-Out** caixa de diálogo. Essa é a opção padrão.|  
    |**Não fazer nada**|Não verifica o arquivo.|  
  
     **Permitir que os itens de check-in a ser editado**  
     Especifica que itens cujo check-in é executado podem ser editados na memória. Se você selecionar essa caixa de seleção, um **edite** botão aparece no **Check-Out** caixa de diálogo quando você tentar editar um item de check-in. Depois de clicar nesse botão, é possível editar o item. Se tentar salvar o item, você deve fazer o check out ou salvá-lo em um local diferente.  
  
     **Redefinir**  
     Reajusta caixas de diálogo de confirmação de controle do código-fonte para suas configurações padrão. Por exemplo, se você tiver selecionado a **não mostrar esta caixa de diálogo novamente** caixa de seleção em uma caixa de diálogo de controle do código-fonte, selecionando a **redefinir** opção inverte a ação.  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas de controle do código-fonte](../../2014/database-engine/source-control-basics.md)   
 [Conexões de controle de fonte de alteração](../../2014/database-engine/change-source-control-connections.md)   
 [Excluir arquivos do controle do código-fonte](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
