---
description: Configurações do projeto (sincronização) (DB2ToSQL)
title: Configurações do projeto (sincronização) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a5629a72-8c17-46a4-bb4d-19d51a0b98a2
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: d6b4aef228ca1631bb550437ff0f66ff20555cb0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88321062"
---
# <a name="project-settingssynchronization-db2tosql"></a>Configurações do projeto (sincronização) (DB2ToSQL)
A página sincronização da caixa de diálogo **configurações do projeto** contém configurações que personalizam como o SSMA carrega e atualiza objetos de banco de dados, como tabelas e procedimentos armazenados, em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
As opções de ações padrão especificam as configurações padrão para atualizar objetos do banco de dados DB2 e para sincronizar objetos com o banco de dados do SQL Server. Para obter mais informações, consulte [Atualizar do banco de dados &#40;DB2ToSQL&#41;](../../ssma/db2/refresh-from-database-db2tosql.md).  
  
Você pode acessar duas páginas de sincronização diferentes que contêm as mesmas configurações:  
  
-   Para especificar as configurações para todos os projetos do SSMA futuros, no menu **ferramentas** , clique em **configurações do projeto padrão**e clique em **sincronização** na parte inferior do painel esquerdo.  
  
-   Para especificar as configurações do projeto atual, no menu **ferramentas** , clique em **configurações do projeto**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
## <a name="miscellaneous-options"></a>Opções diversas  
**Falhas**  
Especifica o número de tentativas que o SSMA deve fazer quando carrega objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os objetos que não forem carregados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no na tentativa atual serão tentados novamente até que o SSMA atinja o número máximo de tentativas no processo de sincronização atual. O valor padrão definido é **2**  
  
## <a name="synchronization-for-db2-options"></a>Sincronização para opções do DB2  
**Ação em alteração de objeto local e remoto**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando a definição de objeto é alterada no SSMA e no servidor de banco de dados. O valor padrão definido é **Atualizar do banco de dados**.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
**Ação na alteração do objeto local**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando o objeto é alterado no SSMA. O valor padrão definido é **Skip**.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
**Ação na alteração do objeto remoto**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os objetos são alterados no servidor de banco de dados. O valor padrão definido é **Atualizar do banco de dados**.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
**Ação quando os metadados do objeto local estão ausentes**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os metadados locais estão ausentes. O valor padrão definido é **Atualizar do banco de dados**.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
## <a name="synchronization-for-sql-server-options"></a>Sincronização para opções de SQL Server  
**Ação em alteração de objeto local e remoto**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando a definição de objeto é alterada no SSMA e no servidor de banco de dados. O valor padrão definido é **gravar no banco de dados**.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, o SSMA atualizará objetos no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
**Ação na alteração do objeto local**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando o objeto é alterado no SSMA. O valor padrão definido é **gravar no banco de dados**.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, o SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
**Ação na alteração do objeto remoto**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os objetos são alterados no servidor de banco de dados.  O valor padrão definido é **Atualizar do banco de dados**.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, o SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
**Ação quando os metadados do objeto local estão ausentes**  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os metadados locais estão ausentes. O valor padrão definido é **Atualizar do banco de dados**.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA selecionará a opção **Atualizar do banco de dados** quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, o SSMA excluirá o objeto do banco de dados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
