---
title: Projeto Settings(Synchronization) (DB2ToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: a5629a72-8c17-46a4-bb4d-19d51a0b98a2
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: da4be629e37646b10011c76f5a78a2cde246865e
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="project-settingssynchronization-db2tosql"></a>Projeto Settings(Synchronization) (DB2ToSQL)
A página de sincronização do **configurações de projeto** caixa de diálogo contém configurações que personalizam o SSMA carrega e atualizações de banco de dados objetos, como tabelas e procedimentos armazenados, em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
As opções de ações padrão especificam as configurações padrão para atualizar objetos do banco de dados DB2 e para sincronizar objetos do banco de dados do SQL Server. Para obter mais informações, consulte [de atualização do banco de dados &#40;DB2ToSQL&#41;](../../ssma/db2/refresh-from-database-db2tosql.md).  
  
Você pode acessar duas páginas diferentes de sincronização que contêm as mesmas configurações:  
  
-   Para especificar configurações para todos os projetos futuros do SSMA, no **ferramentas** menu, clique em **configurações de projeto padrão**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
-   Para especificar as configurações para o projeto atual, no **ferramentas** menu, clique em **configurações de projeto**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
## <a name="miscellaneous-options"></a>Opções diversas  
**Tentativas**  
Especifica o número de tentativas SSMA deve fazer ao carregar objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Objetos que não são carregados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] na tentativa atual será tentada novamente até que o SSMA atinge o número máximo de tentativas no processo de sincronização atual. Conjunto de valor padrão é **2**  
  
## <a name="synchronization-for-db2-options"></a>Sincronização de opções do DB2  
**Ação de alteração de objeto local e remoto**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando a definição do objeto alterado no SSMA e no servidor de banco de dados. Conjunto de valor padrão é **de atualização do banco de dados**.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA carregar definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
**Ação de alteração de objeto local**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando o objeto for alterado no SSMA. Conjunto de valor padrão é **ignorar**.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA carregar definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
**Ação de alteração de objeto remoto**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os objetos alterados no servidor de banco de dados. Conjunto de valor padrão é **de atualização do banco de dados**.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA carregar definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
**Ação quando os metadados de objeto local estão ausente**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando metadados local estão ausente. Conjunto de valor padrão é **de atualização do banco de dados**.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA SSMA carregar definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
## <a name="synchronization-for-sql-server-options"></a>Sincronização de opções do SQL Server  
**Ação de alteração de objeto local e remoto**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando a definição do objeto alterado no SSMA e no servidor de banco de dados. Conjunto de valor padrão é **gravação ao banco de dados**.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA carregar definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA atualizará os objetos no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
**Ação de alteração de objeto local**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando o objeto for alterado no SSMA. Conjunto de valor padrão é **gravação ao banco de dados**.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA carregar definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
**Ação de alteração de objeto remoto**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os objetos alterados no servidor de banco de dados.  Conjunto de valor padrão é **de atualização do banco de dados**.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA carregar definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
**Ação quando os metadados de objeto local estão ausente**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando metadados local estão ausente. Conjunto de valor padrão é **de atualização do banco de dados**.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA seleciona o **de atualização do banco de dados** opção quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA excluirá o objeto do banco de dados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
