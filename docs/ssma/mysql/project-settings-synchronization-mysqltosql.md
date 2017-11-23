---
title: "Configurações (sincronização) (MySQLToSQL) do projeto | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
caps.latest.revision: "3"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 27a5deab2aec74b58e2d23f3812246a15659ff20
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="project-settings-synchronization-mysqltosql"></a>Configurações de projeto (sincronização) (MySQLToSQL)
A sincronização **configurações do projeto** permitem que você configure como os objetos de banco de dados MySQL são sincronizados com os objetos de banco de dados do SQL Server.  
  
As ações padrão especifica as configurações padrão para atualizar objetos do banco de dados MySQL e para sincronizar objetos do banco de dados do SQL Server. Para obter mais informações, consulte [de atualização de banco de dados &#40; MySQLToSQL &#41;](../../ssma/mysql/refresh-from-database-mysqltosql.md)  
  
Você pode acessar duas páginas diferentes de sincronização que contêm as mesmas configurações:  
  
-   Para especificar configurações para todos os projetos futuros do SSMA, no **ferramentas** menu, clique em **DefaultProject configurações**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
-   Para especificar as configurações para o projeto atual, no **ferramentas** menu, clique em **configurações de projeto**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
  
##### <a name="misc"></a>Diversos  
  
##### <a name="attempts"></a>Tentativas  
Fornece as informações sobre o número de etapas necessárias de objetos para carregar no SQL Server. Carregando objetos no SQL Server normalmente é executada em várias etapas. Objetos que não carregarão na primeira passagem, tais como chaves estrangeiras, poderão carregar com êxito no próximo passo.  
  
Por padrão, o valor é 2.  
  
## <a name="synchronization-for-mysql"></a>Sincronização para MySQL  
  
##### <a name="action-on-local-and-remote-object-change"></a>Ação de alteração de objeto local e remoto  
Especifica a configuração padrão na caixa de diálogo de sincronização quando a definição do objeto alterado no SSMA e no servidor de banco de dados.  
  
-   Se você selecionar a atualização do banco de dados, o SSMA carregará definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar Ignorar, SSMA não executará qualquer ação de atualização.  
  
##### <a name="action-on-local-object-change"></a>Ação de alteração de objeto local  
Especifica a configuração padrão na caixa de diálogo de sincronização quando o objeto for alterado no SSMA.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA carregar definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
##### <a name="action-on-remote-object-change"></a>Ação de alteração de objeto remoto  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os objetos alterados no servidor de banco de dados.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA carregar definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Ação quando os metadados de objeto local estão ausente  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os metadados locais estão ausente.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA SSMA carregar definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização  
  
## <a name="synchronization-for-sql-server"></a>Sincronização para o SQL Server  
  
##### <a name="action-on-local-and-remote-object-change"></a>Ação de alteração de objeto Local e remoto  
Especifica a configuração padrão na caixa de diálogo de sincronização quando a definição do objeto alterado no SSMA e no servidor de banco de dados.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA carregar definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA atualizará os objetos no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
##### <a name="action-on-local-object-change"></a>Ação de alteração de objeto local  
Especifica a configuração padrão na caixa de diálogo de sincronização quando o objeto for alterado no SSMA.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA carregar definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
##### <a name="action-on-remote-object-change"></a>Ação de alteração de objeto remoto  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os objetos alterados no servidor de banco de dados.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA carregar definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Ação quando os metadados de objeto local estão ausente  
Especifica a configuração padrão na caixa de diálogo de sincronização quando metadados local estão ausente.  
  
-   Se você selecionar **de atualização do banco de dados**, SSMA seleciona a atualização da opção de banco de dados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA excluirá o objeto do banco de dados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, SSMA não executará qualquer ação de atualização.  
  
