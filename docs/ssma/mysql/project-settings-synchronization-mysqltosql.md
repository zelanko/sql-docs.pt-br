---
title: Configurações do projeto (sincronização) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c4437f76a926e84ffe3592042f9d29b50f3eabf9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67908847"
---
# <a name="project-settings-synchronization-mysqltosql"></a>Configurações do projeto (sincronização) (MySQLToSQL)
As **configurações do projeto** de sincronização permitem configurar como os objetos de banco de dados MySQL são sincronizados com SQL Server objetos de banco de dados.  
  
As ações padrão especificam as configurações padrão para atualizar objetos do banco de dados MySQL e para sincronizar objetos com o banco de dados do SQL Server. Para obter mais informações, consulte [Atualizar do banco de dados &#40;MySQLToSQL&#41;](../../ssma/mysql/refresh-from-database-mysqltosql.md)  
  
Você pode acessar duas páginas de sincronização diferentes que contêm as mesmas configurações:  
  
-   Para especificar as configurações para todos os projetos do SSMA futuros, no menu **ferramentas** , clique em **configurações do defaultproject**e clique em **sincronização** na parte inferior do painel esquerdo.  
  
-   Para especificar as configurações do projeto atual, no menu **ferramentas** , clique em **configurações do projeto**e, em seguida, clique em **sincronização** na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
  
##### <a name="misc"></a>Diversos  
  
##### <a name="attempts"></a>Falhas  
Fornece as informações sobre o número de passagens que os objetos levam para carregar em SQL Server. Carregar objetos em SQL Server normalmente é executado em várias passagens. Os objetos que não carregam na primeira passagem, como chaves estrangeiras, podem ser carregados com êxito na próxima passagem.  
  
Por padrão, o valor é 2.  
  
## <a name="synchronization-for-mysql"></a>Sincronização para MySQL  
  
##### <a name="action-on-local-and-remote-object-change"></a>Ação em alteração de objeto local e remoto  
Especifica a configuração padrão na caixa de diálogo de sincronização quando a definição de objeto é alterada no SSMA e no servidor de banco de dados.  
  
-   Se você selecionar atualizar do banco de dados, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar ignorar, o SSMA não executará nenhuma ação de atualização.  
  
##### <a name="action-on-local-object-change"></a>Ação na alteração do objeto local  
Especifica a configuração padrão na caixa de diálogo de sincronização quando o objeto é alterado no SSMA.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
##### <a name="action-on-remote-object-change"></a>Ação na alteração do objeto remoto  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os objetos são alterados no servidor de banco de dados.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Ação quando os metadados do objeto local estão ausentes  
Especifica a configuração padrão na caixa de diálogo sincronização quando os metadados locais estão ausentes.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização  
  
## <a name="synchronization-for-sql-server"></a>Sincronização para SQL Server  
  
##### <a name="action-on-local-and-remote-object-change"></a>Ação em alteração de objeto local e remoto  
Especifica a configuração padrão na caixa de diálogo de sincronização quando a definição de objeto é alterada no SSMA e no servidor de banco de dados.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, o SSMA atualizará objetos no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
##### <a name="action-on-local-object-change"></a>Ação na alteração do objeto local  
Especifica a configuração padrão na caixa de diálogo de sincronização quando o objeto é alterado no SSMA.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, o SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
##### <a name="action-on-remote-object-change"></a>Ação na alteração do objeto remoto  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os objetos são alterados no servidor de banco de dados.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, o SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>Ação quando os metadados do objeto local estão ausentes  
Especifica a configuração padrão na caixa de diálogo de sincronização quando os metadados locais estão ausentes.  
  
-   Se você selecionar **Atualizar do banco de dados**, o SSMA selecionará a opção Atualizar do banco de dados quando a condição for atendida.  
  
-   Se você selecionar **gravar no banco de dados**, o SSMA excluirá o objeto do banco de dados quando a condição for atendida.  
  
-   Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.  
  
