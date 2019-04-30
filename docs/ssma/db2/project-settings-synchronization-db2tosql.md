---
title: Project Settings(Synchronization) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a5629a72-8c17-46a4-bb4d-19d51a0b98a2
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 5dce11338b2d67412df1259e48d50c0734778d0d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270079"
---
# <a name="project-settingssynchronization-db2tosql"></a>Project Settings(Synchronization) (DB2ToSQL)
A página de sincronização do **configurações do projeto** caixa de diálogo contém configurações que personalizam o SSMA carrega e as atualizações de banco de dados objetos como tabelas e procedimentos armazenados, em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
As opções de ações padrão especificam as configurações padrão para atualizar objetos do banco de dados DB2 e para sincronização de objetos com o banco de dados do SQL Server. Para obter mais informações, consulte [Refresh do banco de dados &#40;DB2ToSQL&#41;](../../ssma/db2/refresh-from-database-db2tosql.md).  
  
Você pode acessar duas páginas diferentes de sincronização que contêm as mesmas configurações:  
  
-   Para especificar configurações para todos os projetos futuros do SSMA, na **ferramentas** menu, clique em **configurações do projeto padrão**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
-   Para especificar configurações para o projeto atual, nos **ferramentas** menu, clique em **configurações do projeto**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
## <a name="miscellaneous-options"></a>Opções diversas  
**Tentativas**  
Especifica o número de tentativas SSMA deve fazer quando ele carregar objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Objetos que não são carregados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na tentativa atual será tentada novamente até que o SSMA atinja o número máximo de tentativas no processo de sincronização atual. Valor padrão definido é **2**  
  
## <a name="synchronization-for-db2-options"></a>Sincronização para opções de DB2  
**Ação de alteração de objeto local e remota**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando a definição do objeto é alterado no SSMA e no servidor de banco de dados. Conjunto de valor padrão é **Refresh do banco de dados**.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
**Ação de alteração de objeto local**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando o objeto é alterado no SSMA. Conjunto de valor padrão é **Skip**.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
**Ação de alteração do objeto remoto**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os objetos alterados no servidor de banco de dados. Conjunto de valor padrão é **Refresh do banco de dados**.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
**Ação quando os metadados de objeto local estão ausente**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando metadados local estão ausente. Conjunto de valor padrão é **Refresh do banco de dados**.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
## <a name="synchronization-for-sql-server-options"></a>Sincronização de opções do SQL Server  
**Ação de alteração de objeto local e remota**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando a definição do objeto é alterado no SSMA e no servidor de banco de dados. Conjunto de valor padrão é **gravação ao banco de dados**.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA atualizará os objetos no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
**Ação de alteração de objeto local**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando o objeto é alterado no SSMA. Conjunto de valor padrão é **gravação ao banco de dados**.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
**Ação de alteração do objeto remoto**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os objetos alterados no servidor de banco de dados.  Conjunto de valor padrão é **Refresh do banco de dados**.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
**Ação quando os metadados de objeto local estão ausente**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando metadados local estão ausente. Conjunto de valor padrão é **Refresh do banco de dados**.  
  
-   Se você selecionar **atualização do banco de dados**, SSMA seleciona o **atualização do banco de dados** quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA excluirá o objeto do banco de dados quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
