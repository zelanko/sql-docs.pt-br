---
title: Relatórios de Clickthrough de página (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.drilthroughreports.f1
ms.assetid: e96cdeba-452b-45a8-9bcf-b75d76261e31
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7f76a4c0d2e9cc3bd2d5591a704491a4bed0ebfb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63266136"
---
# <a name="clickthrough-reports-page-report-manager"></a>Página Relatórios de Clickthrough (Gerenciador de Relatórios)
  Um relatório de clickthrough é aquele que exibe dados relacionados quando você clica nos dados interativos contidos no relatório. Esses relatórios são gerados pelo servidor de relatórios com base nas informações contidas no modelo usado para criar o relatório. Se você não quiser usar os relatórios de clickthrough gerados pelo servidor de relatórios, você pode criar relatórios personalizados publicados em um servidor de relatórios e mapear até pontos de dados interativos definidos no modelo. Os relatórios personalizados devem ser criados no Construtor de Relatórios do mesmo modelo e depois publicados no servidor de relatórios. Para mapear relatórios personalizados para itens no modelo, use a página Relatórios de Clickthrough no Gerenciador de Relatórios.  
  
 A página Relatórios de Clickthrough fornece um modo de mapear relatórios predefinidos, publicados do Construtor de Relatórios para entidades, pastas e itens específicos dentro de um modelo. Quando você mapeia um relatório para um item dentro de um modelo, os usuários que navegam até aquele item obtêm o relatório personalizado em vez de um relatório temporário gerado pelo servidor de relatórios.  
  
 Se você estiver fornecendo relatórios personalizados, deve incluir uma versão de única instância e uma versão de várias instâncias do relatório. O caminho de dados pelo qual um usuário navega para uma entidade específica determina se um relatório de única instância ou de várias instâncias será apresentado ao usuário em tempo de execução. Você não pode saber sempre com antecedência se uma determinada versão do relatório não é necessária.  
  
 Relatórios personalizados que você mapeia para entidades são protegidos pela hierarquia de pastas do servidor de relatórios. Se você mapear um item de modelo para um relatório e o relatório não estiver disponível para um usuário que navegou até ele, o usuário obterá um relatório temporário gerado pelo servidor de relatórios em vez do relatório personalizado pretendido.  
  
 Embora você possa selecionar qualquer relatório ao qual tenha acesso, selecione somente relatórios criados especificamente para o modelo que está sendo configurado.  
  
> [!NOTE]  
>  Os relatórios de clickthrough não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Caso você não tenha certeza sobre qual edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sua organização está usando, contate o administrador do banco de dados.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-clickthrough-reports-page"></a>Para abrir a página Relatórios de Clickthrough  
  
1.  Abra o Gerenciador de Relatórios e localize o modelo para o qual você deseja mapear relatórios de clickthrough para entidades no modelo.  
  
2.  Focalize o modelo e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. Esse procedimento abre a página de propriedades **Geral** do modelo.  
  
4.  Selecione a guia **Clickthrough** .  
  
## <a name="options"></a>Opções  
 **Hierarquia de modelo de item**  
 Mostra as entidades, pastas e itens no namespace de modelo para o qual você pode fornecer um relatório personalizado.  
  
 **Relatório de instância única**  
 Especifica o relatório personalizado a ser usado quando a navegação de usuário exigir uma exibição de dados de única instância. Clique no botão de procura para selecionar o relatório que deseja usar.  
  
 **Relatório de várias instâncias**  
 Especifica o relatório personalizado a ser usado quando a navegação de usuário exigir uma exibição de dados de várias instâncias. Clique no botão de procura para selecionar o relatório que deseja usar.  
  
## <a name="see-also"></a>Consulte também  
 [Publicar Relatórios](../../2014/reporting-services/publish-reports.md)  
  
  
