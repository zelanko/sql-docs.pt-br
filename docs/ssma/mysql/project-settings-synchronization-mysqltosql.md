---
title: Configurações (sincronização) (MySQLToSQL) do projeto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 630700b4541bf804ca9dd5b1b6c6ca705412643c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792554"
---
# <a name="project-settings-synchronization-mysqltosql"></a>Configurações do projeto (sincronização) (MySQLToSQL)
A sincronização **configurações do projeto** permitem que você configure como os objetos de banco de dados MySQL são sincronizados com os objetos de banco de dados do SQL Server.  
  
As ações padrão especificam as configurações padrão para atualizar objetos do banco de dados MySQL e para a sincronização de objetos com o banco de dados do SQL Server. Para obter mais informações, consulte [Refresh do banco de dados &#40;MySQLToSQL&#41;](../../ssma/mysql/refresh-from-database-mysqltosql.md)  
  
Você pode acessar duas páginas diferentes de sincronização que contêm as mesmas configurações:  
  
-   Para especificar configurações para todos os projetos futuros do SSMA, na **ferramentas** menu, clique em **DefaultProject configurações**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
-   Para especificar configurações para o projeto atual, nos **ferramentas** menu, clique em **configurações do projeto**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
  
##### <a name="misc"></a>Diversos  
  
##### <a name="attempts"></a>Tentativas  
Fornece as informações sobre o número de etapas necessárias para carregar no SQL Server. Carregando objetos no SQL Server é geralmente executado em várias passagens. Objetos que não carregarão na primeira passagem, tais como chaves estrangeiras, podem carregar com êxito na próxima fase.  
  
Por padrão, o valor é 2.  
  
## <a name="synchronization-for-mysql"></a>Sincronização para MySQL  
  
##### <a name="action-on-local-and-remote-object-change"></a>Ação de alteração de objeto local e remota  
Especifica a configuração padrão na caixa de diálogo de sincronização quando a definição do objeto é alterado no SSMA e no servidor de banco de dados.  
  
-   Se você selecionar a atualização do banco de dados, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar Ignorar, SSMA não executará nenhuma ação de atualização.  
  
##### <a name="action-on-local-object-change"></a>Ação de alteração de objeto local  
Especifica a configuração padrão na caixa de diálogo de sincronização quando o objeto é alterado no SSMA.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
##### <a name="action-on-remote-object-change"></a>Ação de alteração do objeto remoto  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os objetos alterados no servidor de banco de dados.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Ação quando os metadados de objeto local estão ausente  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os metadados de local estão ausente.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização  
  
## <a name="synchronization-for-sql-server"></a>Sincronização para o SQL Server  
  
##### <a name="action-on-local-and-remote-object-change"></a>Ação de alteração de objeto Local e remoto  
Especifica a configuração padrão na caixa de diálogo de sincronização quando a definição do objeto é alterado no SSMA e no servidor de banco de dados.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA atualizará os objetos no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
##### <a name="action-on-local-object-change"></a>Ação de alteração de objeto local  
Especifica a configuração padrão na caixa de diálogo de sincronização quando o objeto é alterado no SSMA.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
##### <a name="action-on-remote-object-change"></a>Ação de alteração do objeto remoto  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os objetos alterados no servidor de banco de dados.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Ação quando os metadados de objeto local estão ausente  
Especifica a configuração padrão na caixa de diálogo de sincronização quando metadados local estão ausente.  
  
-   Se você selecionar **Refresh do banco de dados**, SSMA seleciona a atualização da opção de banco de dados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, SSMA excluirá o objeto do banco de dados quando a condição for atendida.  
  
-   Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.  
  
