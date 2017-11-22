---
title: Projeto Settings(Synchronization) (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e223fb7d-05ec-4fa5-8973-d845c33a23dd
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 81a3c4860c3916753435e2b5c608628650bae255
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="project-settingssynchronization-oracletosql"></a>Projeto Settings(Synchronization) (OracleToSQL)
A página de sincronização do **configurações de projeto** caixa de diálogo contém configurações que personalizam o SSMA carrega e atualizações de banco de dados objetos, como tabelas e procedimentos armazenados, em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
As opções de ações padrão especificam as configurações padrão para atualizar objetos do banco de dados Oracle e para sincronizar objetos do banco de dados do SQL Server. Para obter mais informações, consulte [de atualização do banco de dados - Oracle](../../ssma/oracle/refresh-from-database-oracletosql.md).  
  
Você pode acessar duas páginas diferentes de sincronização que contêm as mesmas configurações:  
  
-   Para especificar configurações para todos os projetos futuros do SSMA, no **ferramentas** menu, clique em **configurações de projeto padrão**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
-   Para especificar as configurações para o projeto atual, no **ferramentas** menu, clique em **configurações de projeto**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
## <a name="miscellaneous-options"></a>Opções diversas  
**Tentativas**  
Especifica o número de tentativas SSMA deve fazer ao carregar objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Objetos que não são carregados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] na tentativa atual será tentada novamente até que o SSMA atinge o número máximo de tentativas no processo de sincronização atual. Conjunto de valor padrão é **2**  
  
## <a name="synchronization-for-oracle-options"></a>Sincronização para opções de Oracle  
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
  
