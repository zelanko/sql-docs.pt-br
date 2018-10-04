---
title: Especifique um servidor de destino&#39;s local (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], location
ms.assetid: 511ff311-21f5-4f2f-839f-b4deee26ec98
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5ffae4f02e598157215e1062863ffce05794983f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135362"
---
# <a name="specify-a-target-server39s-location-sql-server-management-studio"></a>Especificar o local de um servidor de destino (SQL Server Management Studio)
  Este tópico descreve como especificar o local de um servidor de destino em uma configuração de administração multisservidor no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para especificar o local de um servidor de destino usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Executar essa ação edita o registro. A edição manual do registro não é recomendada, pois alterações incorretas ou não apropriadas podem causar sérios problemas de configuração para o sistema. Portanto, apenas usuários experientes deveriam usar o programa Editor do Registro para editar o registro. Para obter mais informações, consulte a documentação do Microsoft Windows.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-specify-a-target-servers-location"></a>Para especificar o local de um servidor de destino  
  
1.  No **Pesquisador de Objetos,** clique no sinal de adição para expandir o servidor mestre no qual você deseja especificar o local de um servidor de destino.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e selecione **Gerenciar Servidores de Destino**.  
  
3.  Clique com o botão direito do mouse em um servidor de destino e selecione **Propriedades**.  
  
4.  Na caixa **Local** , insira um local para o servidor e clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-specify-a-target-servers-location"></a>Para especificar o local de um servidor de destino  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE msdb ;  
    GO  
    -- enlists the current server into the AdventureWorks1 master server.   
    -- The location for the current server is Building 21, Room 309, Rack 5  
    EXEC dbo.sp_msx_enlist N'AdventureWorks2012',   
        N'Building 21, Room 309, Rack 5' ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_msx_enlist &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql).  
  
  
