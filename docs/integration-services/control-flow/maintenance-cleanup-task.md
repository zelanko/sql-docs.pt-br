---
title: Tarefa Limpeza de Manutenção | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.maintenancecleanuptask.f1
helpviewer_keywords:
- deleting files
- removing files
- Maintenance Cleanup task
ms.assetid: 73ad3cd6-9a6d-44cf-905f-c56aa658bf42
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 333ccd783a1ef55a3c2ddc79936011330cf79b9d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294110"
---
# <a name="maintenance-cleanup-task"></a>Tarefa Limpeza de Manutenção

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A tarefa de Limpeza de Manutenção remove arquivos relacionados a planos de manutenção, inclusive arquivos de backup de banco de dados e relatórios criados por planos de manutenção. Para obter mais informações, consulte [Planos de manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md) e [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 Usando a tarefa de Limpeza de Manutenção, um pacote pode remover os arquivos de backup ou relatórios de plano de manutenção do servidor especificado. A tarefa de Limpeza de Manutenção inclui uma opção para remover um arquivo específico ou remover um grupo de arquivos em uma pasta. Opcionalmente, você pode especificar a extensão dos arquivos a serem excluídos.  
  
 Quando você configura a tarefa de Limpeza de Manutenção para remover arquivos de backup, a extensão de nome de arquivo padrão é BAK. Para arquivos de relatório, a extensão de nome de arquivo padrão é TXT. Você pode atualizar as extensões para serem adequadas a suas necessidades; a única limitação é que as extensões devem ter menos de 256 caracteres.  
  
 Geralmente, você quer remover arquivos antigos que não são mais necessários e a tarefa de Limpeza de Manutenção pode ser configurada para excluir arquivos que alcançaram uma determinada idade. Por exemplo, a tarefa pode ser configurada para excluir arquivos que têm mais de quatro semanas. Você pode especificar a idade dos arquivos a excluir usando dias, semanas, meses ou anos. Se você não especificar a idade mínima de arquivos para excluir, todos os arquivos do tipo especificado serão excluídos.  
  
 Em contraste com versões anteriores da tarefa de Limpeza de Manutenção, a versão da tarefa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não exclui automaticamente arquivos nos subdiretórios do diretório especificado. Essa restrição reduz a área da superfície de qualquer ataque que poderia explorar a funcionalidade da tarefa de Limpeza de Manutenção para excluir arquivos maliciosamente. Para excluir as subpastas do primeiro nível, você deve optar explicitamente por fazer isso com a marcação da opção **Incluir subpastas de primeiro nível** na caixa de diálogo **Tarefa Limpeza de Manutenção** .  
  
## <a name="configuration-of-the-maintenance-cleanup-task"></a>Configuração da tarefa Limpeza de Manutenção  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Tarefa Limpeza de manutenção &#40;Plano de manutenção&#41;](../../relational-databases/maintenance-plans/maintenance-cleanup-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter detalhes sobre como definir essas propriedades no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Definir as propriedades de uma tarefa ou de um contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b).  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  
