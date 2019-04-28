---
title: Project Settings (Synchronization) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0a221d5c24606707ba9876e0980e6c28d2dacc67
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62667967"
---
# <a name="project-settings-synchronization-sybasetosql"></a>Configurações do projeto (sincronização) (SybaseToSQL)
A página de sincronização do **configurações do projeto** caixa de diálogo contém configurações que personalizam como SSMA carrega os objetos de banco de dados, como tabelas e procedimentos armazenados, em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
Você pode acessar duas páginas diferentes de sincronização que contêm as mesmas configurações:  
  
-   Se você deseja especificar configurações para todos os projetos futuros do SSMA, na **ferramentas** menu, selecione **configurações do projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibida ou alterada partir **versão de destino de migração** lista suspensa e, em seguida, selecione **sincronização** na parte inferior do painel esquerdo.  
  
-   Para especificar configurações para o projeto atual, nos **ferramentas** menu, selecione **configurações do projeto**e, em seguida, selecione **sincronização** na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
**Tentativas**  
Especifica o número de tentativas SSMA deve fazer quando ele carregar objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Objetos que não são carregados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na tentativa atual será tentada novamente até que o SSMA atinja o número máximo de tentativas no processo de sincronização atual.  
  
## <a name="synchronization-for-sql-server"></a>Sincronização para o SQL Server  
**Atualizar o objeto local na alteração de objeto local e remota**  
Especifica se o SSMA deve substituir os metadados de objeto local com os metadados do objeto remoto se alterar os objetos locais e remotos.  
Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
Se você selecionar **gravar no banco de dados**, SSMA atualizará os objetos no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.   
Conjunto de opção padrão é **gravar no banco de dados.**  
  
**Atualizar o objeto local na alteração de objeto local**  
Especifica se o SSMA deve substituir os metadados de objeto local com os metadados do objeto remoto se o objeto remoto for alterado.  
Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
Se você selecionar **gravar no banco de dados**, SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.   
É o conjunto de opções padrão **gravar no banco de dados**.  
  
**Atualizar o objeto local na alteração do objeto remoto**  
Especifica se o SSMA deve substituir os metadados de objeto local com os metadados do objeto remoto se o objeto remoto for alterado.  
Se você selecionar **Refresh do banco de dados**, SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
Se você selecionar **gravar no banco de dados**, SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.   
É o conjunto de opções padrão **Refresh do banco de dados**.  
  
**Atualizar quando os metadados de objeto local estão ausente**  
Especifica se o SSMA deve criar metadados locais se existe um objeto no banco de dados de destino, mas não localmente.  
Se você selecionar **Refresh do banco de dados**, SSMA seleciona a atualização da opção de banco de dados quando a condição for atendida.  
Se você selecionar **gravar no banco de dados**, SSMA excluirá o objeto do banco de dados quando a condição for atendida.  
Se você selecionar **Skip**, SSMA não executará nenhuma ação de atualização.   
É o conjunto de opções padrão **Refresh do banco de dados**.  
  
