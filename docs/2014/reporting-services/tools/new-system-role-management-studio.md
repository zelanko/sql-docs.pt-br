---
title: Nova Função de Sistema (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.newsystemrole.f1
ms.assetid: 7b4a0b98-975b-478a-8359-7db39ccbb347
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4d9227136ba3bd1526f8ec04476d6dc5d61ca41f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100177"
---
# <a name="new-system-role-management-studio"></a>Nova Função do Sistema (Management Studio)
  Use essa página para criar uma definição de função de nível de sistema. Uma definição de função de sistema especifica um conjunto de tarefas de nível de sistema que se aplica a um servidor de relatório como um todo.  
  
> [!NOTE]  
>  Definições de função só são usadas em um servidor de relatório que executa em modo nativo. Se o servidor de relatório for configurado para integração do SharePoint, essa página não estará disponível.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite o nome da definição da função. O nome de definição de função deve ser exclusivo no namespace do servidor de relatório. Um nome deve conter pelo menos um caractere alfanumérico. Também pode conter espaços e alguns símbolos. Não use os seguintes caracteres ao especificar um nome:  
  
 ; ? : \@ & = + , $ / * \< >  
  
 " /  
  
 **Descrição**  
 Fornece uma descrição que explica como usar a função e enumera a que a função dá suporte.  
  
 **Tarefa**  
 Selecione as tarefas de nível de sistema que podem ser executadas por essa função. Você não pode criar tarefas novas ou modificar as tarefas existentes compatíveis com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Você não pode escolher tarefas de nível de item para uma definição de função do sistema.  
  
 **Descrição da tarefa**  
 Exibe uma descrição de tarefa que enumera as operações ou permissões às quais a tarefa dá suporte.  
  
## <a name="see-also"></a>Consulte também  
 [Servidor de Relatório na ajuda F1 do Management Studio](report-server-in-management-studio-f1-help.md)   
 [Definições de função](../security/role-definitions.md)  
  
  
