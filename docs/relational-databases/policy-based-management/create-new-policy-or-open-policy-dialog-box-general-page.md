---
description: Caixas de diálogo Criar Nova Política ou Abrir política, Página geral
title: Caixa de diálogo 'Criar Política' ou 'Abrir Política', Página Geral
descripton: Describes the 'General Page' of the 'Create New Policy' and 'Open Policy' dialog boxes for Policy-Based Management in SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.policy.f1
- sql13.swb.dmf.policy.filter.f1
- sql13.swb.dmf.newgroup.f1
ms.assetid: c00bebd0-d04b-4c64-840e-8b7a2c603436
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 88741c77d43e3f68303c6624ba32e1d58a2d8392
ms.sourcegitcommit: 827ad02375793090fa8fee63cc372d130f11393f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89480272"
---
# <a name="create-new-policy-or-open-policy-dialog-box-general-page"></a>Caixas de diálogo Criar Nova Política ou Abrir política, Página geral
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use esta caixa de diálogo para criar uma nova política ou modificar uma política existente do Gerenciamento Baseado em Políticas. Use as áreas **Em relação aos destinos** e **Restrição de servidor** como um filtro para limitar as políticas a um subconjunto de todos os destinos possíveis. Com relação às condições a serem usadas como filtros de destino, elas devem ser definidas em uma faceta física e não devem conter funções e nem operador LIKE. Quando o sistema computar o objeto definido para uma política, por padrão os objetos do sistema serão excluídos.  Por exemplo, se o conjunto de objetos da política referenciar todas as tabelas, a política não se aplicará a tabelas do sistema. Se os usuários desejarem avaliar uma política em relação a objetos do sistema, eles poderão explicitamente adicionar objetos do sistema ao conjunto de objetos. Entretanto, embora todas as políticas tenham suporte para o modo de avaliação **verificação de agenda** , por questões de desempenho, nem todas as políticas com conjuntos de objetos arbitrários têm suporte para o modo de avaliação **verificação de alterações** . Para obter mais informações, consulte [https://docs.microsoft.com/archive/blogs/sqlpbm/policy-evaluation-modes](https://docs.microsoft.com/archive/blogs/sqlpbm/policy-evaluation-modes)  
  
## <a name="options"></a>Opções  
 **Nome**  
 No caso de uma nova política, digite o nome da nova política. No caso de uma política existente, o nome será exibido.  
  
 **Enabled**  
 Selecione a caixa de seleção **Habilitado** para habilitar a política. Desmarque a caixa de seleção **Habilitado** para desabilitar a política. A caixa **Habilitado** se aplica à automação da política. Ela cria ou remove o sistema de automação da política. A automação usa os seguintes mecanismos:  
  
 **Ao alterar: impedir**  
 Um gatilho de banco de dados garante conformidade.  
  
 **Ao alterar: log apenas**  
 Um evento dos serviços de notificação verifica a conformidade.  
  
 **Ao agendar**  
 Um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é criado para verificar a conformidade em uma agenda.  
  
 Políticas executadas usando o modo de avaliação **Sob Demanda** não usam esta caixa de seleção.  
  
 **Verificar condição**  
 Selecione a condição de Gerenciamento Baseado em Política que esta política usa. Todas as condições no servidor para a faceta de Gerenciamento Baseado em Política associada são listadas. Clique em **Nova condição** para criar uma condição nova. Clique no botão de reticências (**…**) para modificar a condição.  
  
 **Em relação aos destinos**  
 Selecione os tipos de destinos que estão disponíveis para essa faceta para completar uma expressão de filtro.  
  
 **Modo de avaliação**  
 Selecione o modo de avaliação para a política. Algumas políticas podem ser marcadas, mas não impostas. Os modos de avaliação são os seguintes:  
  
 **Sob Demanda**  
 A política só será executada quando você executá-la na caixa de diálogo **Avaliar** .  
  
 **Ao agendar**  
 Avalia periodicamente a política, registra uma entrada de log para políticas sem-conformidade e cria um relatório. Habilita a caixa **Agenda** .  
  
 **Ao alterar: log apenas**  
 Quando se tenta fazer alterações, esta opção não evita alterações sem-conformidade, mas registra violações de política.  
  
 **Ao alterar: impedir**  
 Quando se tenta fazer alterações, esta opção evita alterações que possam violar a política.  
  
 **Agenda**  
 Esta opção aparece quando o modo de avaliação **Ao agendar** é selecionado. Digite o nome da agenda, clique em **Escolher** para selecionar uma agenda de uma lista ou clique em **Novo** para criar uma nova agenda. Para habilitar a área da agenda, **Na agenda** deve ser selecionado.  
  
 **Restrição de servidor**  
 Selecione os tipos de servidores que são apropriados para esta política. As opções são **Nenhum** ou selecione uma condição que filtra os possíveis servidores.  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
