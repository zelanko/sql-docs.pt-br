---
title: Página de segurança (Gerenciador de relatórios) do Item de modelo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.modelitemsecurity.f1
ms.assetid: 8c5b29ae-1f17-41f2-ab59-97899b8fb4fc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f45169a2fdc8fdc4d56cb27a8bf6348a3c3c1a29
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108226"
---
# <a name="model-item-security-page-report-manager"></a>Página segurança de item de modelo (Gerenciador de Relatórios)
  Use essa página para proteger partes de um modelo concedendo ou revogando permissões somente leitura em itens específicos. A segurança de item de modelo afeta a exploração de dados ad hoc em tempo de execução e a capacidade de usar partes de um modelo publicado ao criar relatórios no Construtor de Relatórios. Para usar esse recurso, você deve ter permissões de Gerenciador de Conteúdo.  
  
 Ela é aplicada a um modelo processado no servidor de relatório e não afeta arquivos .smdl que você edita no Designer de Modelo ou usa no Designer de Relatórios. Além disso, ela não afeta os usuários que têm permissão para modificar uma definição de modelo. Qualquer usuário com permissões do Gerenciador de Conteúdo ou do Publicador em um modelo pode ver partes dele, independentemente de você aplicar a segurança de item de modelo.  
  
> [!NOTE]  
>  Os itens de modelo podem ter uma proteção ainda maior se você usar filtros de segurança.  
  
 Você pode definir a segurança de item de modelo em entidades, pastas e campos individuais de um modelo. Como um modelo apresenta uma grande superfície de itens de segurança, herança de permissão é criada no modelo para que um grande número de itens possa ser protegido em um número de atribuições de função relativamente pequeno. Herança de permissão é baseada no seguinte:  
  
-   Modelo  
  
-   Nó raiz  
  
-   Pastas ou entidades  
  
-   Campos  
  
 Inicialmente, permissão para acessar itens de modelo é herdada por tarefas de função definidas no próprio modelo. Um usuário com permissão para exibir um modelo em uma pasta no Gerenciador de Relatórios pode exibir todos os itens no modelo.  
  
 Se você aplicar segurança de item modelo, deve criar pelo menos uma atribuição de função no nó raiz. Essa atribuição de função inicial no nó raiz se torna a nova fonte de permissões herdadas. A atribuição de função no nó raiz é automaticamente herdada por todos os itens na hierarquia do modelo.  
  
 Para personalizar mais permissões na exploração de dados, você pode variar as permissões nas pastas e entidades. Finalmente, você pode definir permissões em campos individuais.  
  
 Para facilitar a manutenção das atribuições de função, só defina permissões em pastas ou entidades em vez de em campos individuais. Você não pode procurar tarefas de função que você cria. Se você definir segurança em campos específicos e quiser posteriormente atualizar as definições de segurança, terá de clicar pelo namespace do modelo para encontrar os campos protegidos.  
  
 Para iniciar, crie uma atribuição de função no nó raiz e crie atribuições de função adicionais nas entidades e pastas. Para desmarcar segurança do item modelo, desmarque a caixa de seleção **Proteja os itens de modelo individuais independentemente para este modelo**. Ao desmarcar a caixa de seleção, as permissões iniciais herdadas do modelo serão revertidas.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-general-properties-page-for-a-report"></a>Para abrir a página Propriedades gerais de um relatório  
  
1.  Abra o Gerenciador de Relatórios e localize o modelo para o qual você deseja configurar a segurança de itens de modelo.  
  
2.  Focalize o modelo e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. Esse procedimento abre a página de propriedades Geral do modelo.  
  
4.  Selecione a guia **Segurança do Item de Modelo** .  
  
## <a name="options"></a>Opções  
 **Proteger itens de modelo individuais independentemente para este modelo**  
 Clique nesta caixa de seleção para habilitar a segurança de item de modelo.  
  
 **Especifique a segurança para itens de modelo individuais no modo**  
 Mostra todos os itens em um modelo. Você pode navegar no namespace do modelo para selecionar o item você quer proteger. Você só pode selecionar um item de cada vez. Crie a primeira atribuição de função no nó raiz antes de prosseguir com outras entidades e pastas.  
  
 **Herdar permissões do item pai**  
 Clique nessa opção para herdar as configurações de segurança do item pai.  
  
 **Atribuir permissão de leitura aos seguintes usuários e grupos (separados por ponto-e-vírgula)**  
 Clique nessa opção para especificar o usuário ou a conta de grupo para os quais você está definindo acesso. Se você estiver usando segurança padrão, as contas de usuário e grupo serão contas do domínio Windows. Especifique as contas neste formato:  *\<domínio >\\< conta\>*.  
  
## <a name="see-also"></a>Consulte também  
 [Servidor de Relatório na ajuda F1 do Management Studio](tools/report-server-in-management-studio-f1-help.md)  
  
  
