---
title: Configurar o Designer de Diagramas de Banco de Dados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.InstallSqlDiagramSupport
helpviewer_keywords:
- Database Diagram Designer
- database diagrams [SQL Server], Database Diagram Designer
- diagrams [SQL Server], Database Diagram Designer
ms.assetid: 927321ee-b459-4f5b-9719-4a7a95639143
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dfa43eb6ced096a5ae4facd215cf06a87a97976f
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42774139"
---
# <a name="set-up-database-diagram-designer-visual-database-tools"></a>Configurar o Designer de Diagramas de Banco de Dados (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Para usar o Designer de Diagramas de Banco de Dados, ele precisa ser configurado primeiramente por um membro da função **db_owner** para controlar o acesso a diagramas.  
  
### <a name="to-set-up-database-diagramming"></a>Para configurar a diagramação de um banco de dados  
  
1.  Utilizando o Pesquisador de Objetos, expanda um nó do banco de dados.  
  
2.  Expanda o nó Diagrama de Banco de Dados na conexão do banco de dados.  
  
3.  Selecione **Sim** quando solicitado se desejar configurar a diagramação do banco de dados.  
  
    > [!NOTE]  
    > Isso criará a tabela de diagrama de banco de dados, os procedimentos armazenados do sistema e uma função do sistema no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
4.  O Visual Studio criará os seguintes objetos na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    1.  Tabela sysdiagrams  
  
    2.  Procedimento armazenado sp_alterdiagram  
  
    3.  Procedimento armazenado sp_creatediagram  
  
    4.  Procedimento armazenado sp_dropdiagram  
  
    5.  Procedimento armazenado sp_renamediagram  
  
    6.  Função fn_diagramobjects  
  
    7.  Procedimento armazenado sp_helpdiagrams  
  
    8.  Procedimento armazenado sp_helpdiagramsdefinition  
  
    9. Procedimento armazenado sp_upgraddiagrams  
  
## <a name="see-also"></a>Consulte Também  
[Compreender a propriedade do diagrama de banco de dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/understand-database-diagram-ownership-visual-database-tools.md)  
[Atualizar diagramas de banco de dados de edições anteriores &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
[ALTER AUTHORIZATION (Transact-SQL)](http://msdn.microsoft.com/en-us/8c805ae2-91ed-4133-96f6-9835c908f373)  
  
