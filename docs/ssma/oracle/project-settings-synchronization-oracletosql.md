---
title: Projeto (sincronização) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e223fb7d-05ec-4fa5-8973-d845c33a23dd
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: f1dde13356f684d7fa6d7273156485bd6b5d07fd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47780724"
---
# <a name="project-settingssynchronization-oracletosql"></a>Configurações do projeto (sincronização) (OracleToSQL)
A página de sincronização do **configurações do projeto** caixa de diálogo contém configurações que personalizam o SSMA carrega e as atualizações de banco de dados objetos como tabelas e procedimentos armazenados, em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
As opções de ações padrão especificam as configurações padrão para atualizar objetos do banco de dados Oracle e para a sincronização de objetos com o banco de dados do SQL Server. Para obter mais informações, consulte [Refresh do banco de dados – Oracle](../../ssma/oracle/refresh-from-database-oracletosql.md).  
  
Você pode acessar duas páginas diferentes de sincronização que contêm as mesmas configurações:  
  
-   Para especificar configurações para todos os projetos futuros do SSMA, na **ferramentas** menu, clique em **configurações do projeto padrão**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
-   Para especificar configurações para o projeto atual, nos **ferramentas** menu, clique em **configurações do projeto**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
## <a name="miscellaneous-options"></a>Opções diversas  
**Tentativas**  
Especifica o número de tentativas SSMA deve fazer quando ele carregar objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Objetos que não são carregados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na tentativa atual será tentada novamente até que o SSMA atinja o número máximo de tentativas no processo de sincronização atual. Valor padrão definido é **2**  
  
## <a name="synchronization-for-oracle-options"></a>Sincronização para opções de Oracle  
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
  
-   Se você selecionar **Refresh do banco de dados**, SSMA SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
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
  
