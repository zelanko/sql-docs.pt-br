---
title: Nova Função de Usuário (Management Studio) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.suite: pro-bi
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.newrole.f1
ms.assetid: 9f76a235-0b58-479c-8e5b-50588091b71c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 12e664ce6040f623754d2662859d23293d747864
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43278437"
---
# <a name="new-user-role-management-studio"></a>Nova função do usuário (Management Studio)
  Use essa página para criar uma definição de função de nível de item. Uma definição de função de nível é uma coleção nomeada de tarefas que enumera as tarefas que um usuário pode executar em relação a pastas, relatórios, modelos, recursos e fontes de dados compartilhadas. Um exemplo de uma definição de função de nível de item é uma função de navegador predefinida que identifica os tipos de ações que um usuário final de relatório pode necessitar para navegar pelas pastas e exibir relatórios.  
  
 As definições de função devem ser em baixo número. A maioria das organizações só requer algumas definições de função. Porém, se as definições de função predefinidas forem insuficientes, você poderá variá-las ou criar novas definições.  
  
> [!NOTE]  
>  Definições de função só são usadas em um servidor de relatório que executa em modo nativo. Se o servidor de relatório for configurado para integração do SharePoint, essa página não estará disponível.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite o nome da definição da função. O nome de definição de função deve ser exclusivo no namespace do servidor de relatório. Um nome deve conter pelo menos um caractere alfanumérico. Também pode conter espaços e alguns símbolos. Não use os seguintes caracteres ao especificar um nome:  
  
 ; ? : \@ & = + , $ / * < >  
  
 " /  
  
 **Descrição**  
 Digite uma descrição que explica como usar a função e enumera ao que ela oferece suporte.  
  
 **Tarefa**  
 Selecione as tarefas que podem ser executadas por essa função. Você não pode criar tarefas novas ou modificar as tarefas existentes compatíveis com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Somente tarefas do nível de item podem ser usadas em uma definição de função de nível de item.  
  
 **Descrição da tarefa**  
 Exibe uma descrição de tarefa que enumera as operações ou permissões às quais a tarefa dá suporte.  
  
## <a name="see-also"></a>Consulte Também  
 [Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Definições de função](../../reporting-services/security/role-definitions.md)  
  
  
