---
title: Grupo de carga de trabalho do Resource Governor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group
- workload groups [SQL Server]
- workload groups [SQL Server], overview
ms.assetid: a84c3c3f-55b6-4a30-9c42-13f082d9281e
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 4f15d4e443f0ffd6df700bff67ed6ba7514e0c90
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68126877"
---
# <a name="resource-governor-workload-group"></a>Grupos de carga de trabalho do Administrador de Recursos
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  No Administrador de Recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o grupo de carga de trabalho funciona como um contêiner para as solicitações de sessão que têm critérios de classificação similares. Uma carga de trabalho permite o monitoramento de agregação de sessões e define políticas para as sessões. Cada grupo de carga de trabalho está em um pool de recursos, que representa um subconjunto dos recursos físicos de uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Quando uma sessão é iniciada, o classificador do Administrador de Recursos atribui a sessão a um grupo de carga de trabalho específico e a sessão deve ser executada, usando as políticas atribuídas ao grupo de carga de trabalho e os recursos definidos para o pool de recursos.  
  
## <a name="workload-group-concepts"></a>Conceitos do grupo de cargas de trabalho  
 O grupo de cargas de trabalho funciona como um contêiner para as solicitações de sessão similares, de acordo com os critérios de classificação aplicados a cada solicitação. O grupo de carga de trabalho permite o monitoramento agregado do consumo de recursos e a aplicação de uma política uniforme para todas as solicitações no grupo. Um grupo define as políticas para seus membros.  
  
> [!NOTE]  
>  Os grupos de carga de trabalho definidos pelo usuário podem ser movidos de um pool de recursos para outro.  
  
 O Administrador de Recursos predefine dois grupos de carga de trabalho: o grupo interno e o padrão. Um usuário não pode alterar nada que esteja classificado como grupo interno, mas pode fazer o monitoramento. As solicitações são classificadas no grupo padrão quando existem as seguintes condições:  
  
-   Não há nenhum critério para classificar uma solicitação.  
  
-   Há uma tentativa de classificar a solicitação em um grupo inexistente.  
  
-   Há uma falha de classificação geral.  
  
 O Administrador de Recursos também fornece instruções DDL para criar, alterar e descartar grupos de carga de trabalho.  
  
## <a name="workload-group-tasks"></a>Tarefas do grupo de carga de trabalho  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como criar um grupo de cargas de trabalho.|[Criar um grupo de carga de trabalho](../../relational-databases/resource-governor/create-a-workload-group.md)|  
|Descreve como alterar as configurações de um grupo de cargas de trabalho.|[Alterar as configurações do grupo de carga de trabalho](../../relational-databases/resource-governor/change-workload-group-settings.md)|  
|Descreve como excluir um grupo de cargas de trabalho.|[Excluir um grupo de carga de trabalho](../../relational-databases/resource-governor/delete-a-workload-group.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar Administrador de Recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Função de classificação do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [Configurar o administrador de recursos usando um modelo](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [Exibir Propriedades do Administrador de Recursos](../../relational-databases/resource-governor/view-resource-governor-properties.md)  
  
  
