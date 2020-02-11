---
title: Configurações do projeto (sincronização) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e223fb7d-05ec-4fa5-8973-d845c33a23dd
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 743ed010107c9557c84b1683f7a81b369ca7cf3c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266594"
---
# <a name="project-settingssynchronization-oracletosql"></a>Configurações do projeto (sincronização) (OracleToSQL)
A página sincronização da caixa de diálogo **configurações do projeto** contém configurações que personalizam como o SSMA carrega e atualiza objetos de banco de dados, como tabelas e procedimentos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]armazenados, em.  
  
As opções de ações padrão especificam as configurações padrão para atualizar objetos do banco de dados Oracle e para sincronizar objetos com o banco de dados do SQL Server. Para obter mais informações, consulte [Atualizar do banco de dados – Oracle](../../ssma/oracle/refresh-from-database-oracletosql.md).  
  
Você pode acessar duas páginas de sincronização diferentes que contêm as mesmas configurações:  
  
-   Para especificar as configurações para todos os projetos do SSMA futuros, no menu **ferramentas** , clique em **configurações do projeto padrão**e clique em **sincronização** na parte inferior do painel esquerdo.  
  
-   Para especificar as configurações do projeto atual, no menu **ferramentas** , clique em **configurações do projeto**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
## <a name="miscellaneous-options"></a>Opções diversas  
**Falhas**  
Especifica o número de tentativas que o SSMA deve fazer quando carrega objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no. Os objetos que não forem carregados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no na tentativa atual serão tentados novamente até que o SSMA atinja o número máximo de tentativas no processo de sincronização atual. O valor padrão definido é **2**  
  
## <a name="synchronization-for-oracle-options"></a>Sincronização para opções Oracle  
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
  
