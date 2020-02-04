---
title: Habilitar e desabilitar Meus Relatórios | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- deactivated My Reports folder
- folders [Reporting Services], My Reports
- activated My Reports folder
- My Reports folder [Reporting Services]
- disabling My Reports folder
ms.assetid: 16c76e82-9fd4-417c-9ed3-a7d5bcd1dba2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6670d1da918ac1bdc6cb1947b265f9d543259814
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65577774"
---
# <a name="enable-and-disable-my-reports"></a>Habilitar e desabilitar Meus Relatórios
  O recurso Meus Relatórios aloca armazenamento pessoal no banco de dados do servidor de relatório, para que os usuários possam salvar seus relatórios em uma pasta particular. Como um administrador do servidor de relatório, você pode habilitar ou desabilitar esse recurso ou alterar a maneira como ele funciona, por meio das configurações de segurança que controlam o que os usuários podem fazer com esse workspace.  
  
 Por padrão, o recurso Meus Relatórios está desabilitado. Você pode habilitar ou desabitar o recurso para todos os usuários, mas não pode habilitá-lo para um subconjunto de usuários. A maioria dos usuários e organizações considera o recurso valioso; avalie as vantagens e desvantagens apresentadas mais adiante neste tópico para determinar se ele é adequado para sua organização.  
  
## <a name="how-to-enable-and-disable-my-reports"></a>Como habilitar e desabilitar Meus Relatórios  
 Para habilitar Meus Relatórios usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do servidor de relatório e abra a página **Propriedades de Servidor** . Em seguida, na guia **Geral** , selecione a opção **Habilitar uma pasta Meus Relatórios para cada usuário** .  
  
 A definição de função usada para Meus Relatórios determina para quais ações há suporte no workspace Meus Relatórios. Por exemplo, se a função Meus Relatórios excluir "Criar relatórios vinculados", os usuários não poderão criar relatórios vinculados nas pastas Meus Relatórios. Para obter mais informações, consulte [Proteger Meus Relatórios](../../reporting-services/security/secure-my-reports.md).  
  
 Para desativar Meus Relatórios, desmarque a opção **Habilitar uma pasta Meus Relatórios para cada usuário**. A desativação de Meus Relatórios remove todas as indicações visíveis para os usuários da pasta Meus Relatórios. As pastas que fornecem armazenamento real (ou seja, as subpastas em Pastas dos Usuários) devem ser excluídas manualmente assim que o recurso for desabilitado.  
  
### <a name="when-my-reports-is-activated"></a>Quando Meus Relatórios está ativado  
 Quando o recurso está ativado, os usuários veem uma pasta Meus Relatórios localizada na pasta raiz, Base. Além de uma pasta Meus Relatórios, os administradores do servidor de relatório também veem uma pasta Pastas dos Usuários que contém a subpasta de cada usuário.  
  
 Enquanto o recurso está ativado, Pastas dos Usuários e suas subpastas não podem ser excluídas. Além disso, o nome "Meus Relatórios" se torna um nome reservado para pastas criadas sob o nó raiz (Base).  
  
 Se você ativar Meus Relatórios depois de sua desativação, o servidor de relatório criará uma nova pasta Pastas dos Usuários caso ainda não exista uma. Se Pastas dos Usuários já existir, o servidor de relatório adicionará novas subpastas à medida que os usuários fizerem logon em suas pastas Meus Relatórios.  
  
### <a name="when-my-reports-is-deactivated"></a>Quando Meus Relatórios está desativado  
 Assim que o recurso for desativado, o nome "Meus Relatórios" não será mais reservado. Os usuários podem criar uma pasta pessoal chamada Meus Relatórios na pasta Base. Além disso, o redirecionamento de Meus Relatórios para subpastas Meus Relatórios específicas do usuário não ocorre mais. Finalmente, qualquer link de relatório que inclua uma pasta Meus Relatórios específica do usuário no endereço URL não funcionará mais.  
  
## <a name="choosing-to-use-my-reports"></a>Optando por usar Meus Relatórios  
 A decisão sobre se a opção Meus Relatórios deve ser usada ou não depende de se você deseja dedicar recursos do servidor para oferecer suporte a um workspace do usuário. Meus Relatórios é um recurso poderoso que permite que os usuários tenham controle sobre os recursos de informações que os ajudam a realizar seus trabalhos. Também fornece uma maneira para que os usuários trabalhem com aqueles relatórios não destinados a uso geral. Um dos principais motivos para usar o recurso Meus Relatórios é que ele oferece suporte seguro e gerenciável para o segmento de usuários que precisa criar e revisar relatórios. Sem esse recurso, você pode se pegar criando pastas e políticas de segurança para vários usuários em uma base ad hoc. À medida que os usuários e as suas necessidades mudam, essa abordagem resulta em um número cada vez maior de pastas e políticas difíceis de serem mantidas com o tempo.  
  
 Observe que se você ativar a opção Meus Relatórios, o servidor de relatório criará uma pasta Meus Relatórios para cada usuário com uma conta de domínio que clica no link Meus Relatórios, mesmo que o usuário não queria nem precise de uma pasta Meus Relatórios. Não há uma maneira sistemática de determinar quais pastas estão sendo usadas. Você deve revisar as pastas manualmente para ver se elas contêm alguma coisa.  
  
## <a name="see-also"></a>Consulte Também  
 [Proteger Meus Relatórios](../../reporting-services/security/secure-my-reports.md)   
 [Gerenciamento de conteúdo do Servidor de Relatório &#40;Modo Nativo do SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
