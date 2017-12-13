---
title: Configurar o Designer de Diagramas de Banco de Dados (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vdt.diagnostic.InstallSqlDiagramSupport
helpviewer_keywords:
- Database Diagram Designer
- database diagrams [SQL Server], Database Diagram Designer
- diagrams [SQL Server], Database Diagram Designer
ms.assetid: 927321ee-b459-4f5b-9719-4a7a95639143
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 227ab535221f24fb815e245dab9678fc9266a7b7
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="set-up-database-diagram-designer-visual-database-tools"></a>Configurar o Designer de Diagramas de Banco de Dados (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Para usar o Designer de Diagramas de Banco de Dados, ele precisa ser configurado primeiramente por um membro da função **db_owner** para controlar o acesso a diagramas.  
  
### <a name="to-set-up-database-diagramming"></a>Para configurar a diagramação de um banco de dados  
  
1.  Utilizando o Pesquisador de Objetos, expanda um nó do banco de dados.  
  
2.  Expanda o nó Diagrama de Banco de Dados na conexão do banco de dados.  
  
3.  Selecione **Sim** quando solicitado se desejar configurar a diagramação do banco de dados.  
  
    > [!NOTE]  
    > Isso criará a tabela de diagrama de banco de dados, os procedimentos armazenados do sistema e uma função do sistema no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
4.  O Visual Studio criará os seguintes objetos na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
    1.  Tabela sysdiagrams  
  
    2.  Procedimento armazenado sp_alterdiagram  
  
    3.  Procedimento armazenado sp_creatediagram  
  
    4.  Procedimento armazenado sp_dropdiagram  
  
    5.  Procedimento armazenado sp_renamediagram  
  
    6.  Função fn_diagramobjects  
  
    7.  Procedimento armazenado sp_helpdiagrams  
  
    8.  Procedimento armazenado sp_helpdiagramsdefinition  
  
    9. Procedimento armazenado sp_upgraddiagrams  
  
## <a name="see-also"></a>Consulte também  
[Compreender a propriedade do diagrama de banco de dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/understand-database-diagram-ownership-visual-database-tools.md)  
[Atualizar diagramas de banco de dados de edições anteriores &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
[ALTER AUTHORIZATION (Transact-SQL)](http://msdn.microsoft.com/en-us/8c805ae2-91ed-4133-96f6-9835c908f373)  
  
