---
title: Configurar o Designer de Diagramas de Banco de Dados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.InstallSqlDiagramSupport
helpviewer_keywords:
- Database Diagram Designer
- database diagrams [SQL Server], Database Diagram Designer
- diagrams [SQL Server], Database Diagram Designer
ms.assetid: 927321ee-b459-4f5b-9719-4a7a95639143
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e8236a18c715451ecb32c5fdcb890d5bf00901c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65099895"
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
[ALTER AUTHORIZATION (Transact-SQL)](https://msdn.microsoft.com/8c805ae2-91ed-4133-96f6-9835c908f373)  
  
