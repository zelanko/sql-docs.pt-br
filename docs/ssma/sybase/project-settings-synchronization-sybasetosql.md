---
title: Configurações do projeto (sincronização) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2cd6bc01-b8e5-4312-83a4-eac66dc1d460
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 663a4b1e49d1f81ce040254a2c8f39a1a1f84b38
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028678"
---
# <a name="project-settings-synchronization-sybasetosql"></a>Configurações do projeto (sincronização) (SybaseToSQL)
A página sincronização da caixa de diálogo **configurações do projeto** contém configurações que personalizam como o SSMA carrega objetos de banco de dados, como tabelas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e procedimentos armazenados, em ou SQL Azure.  
  
Você pode acessar duas páginas de sincronização diferentes que contêm as mesmas configurações:  
  
-   Se você quiser especificar configurações para todos os projetos do SSMA futuros, no menu **ferramentas** , selecione **configurações de projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações devem ser exibidas ou alteradas no menu suspenso **versão de destino de migração** e, em seguida, selecione **sincronização** na parte inferior do painel esquerdo.  
  
-   Para especificar as configurações do projeto atual, no menu **ferramentas** , selecione **configurações do projeto**e, em seguida, selecione **sincronização** na parte inferior do painel esquerdo.  
  
## <a name="options"></a>Opções  
**Falhas**  
Especifica o número de tentativas que o SSMA deve fazer quando carrega objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no. Os objetos que não forem carregados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no na tentativa atual serão tentados novamente até que o SSMA atinja o número máximo de tentativas no processo de sincronização atual.  
  
## <a name="synchronization-for-sql-server"></a>Sincronização para SQL Server  
**Atualizar objeto local em alteração de objeto local e remoto**  
Especifica se o SSMA deve substituir os metadados do objeto local por metadados de objeto remoto se os objetos locais e remotos forem alterados.  
Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
Se você selecionar **gravar no banco de dados**, o SSMA atualizará objetos no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.   
A opção padrão definida é **gravar no banco de dados.**  
  
**Atualizar objeto local na alteração do objeto local**  
Especifica se o SSMA deve substituir os metadados do objeto local por metadados do objeto remoto se o objeto remoto for alterado.  
Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
Se você selecionar **gravar no banco de dados**, o SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.   
A opção padrão definida é **gravar no banco de dados**.  
  
**Atualizar objeto local na alteração do objeto remoto**  
Especifica se o SSMA deve substituir os metadados do objeto local por metadados do objeto remoto se o objeto remoto for alterado.  
Se você selecionar **Atualizar do banco de dados**, o SSMA carregará as definições de banco de dados nos metadados quando a condição for atendida.  
Se você selecionar **gravar no banco de dados**, o SSMA atualizará o objeto no banco de dados de acordo com o conteúdo de metadados do SSMA quando a condição for atendida.  
Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.   
O conjunto de opções padrão é **Atualizar do banco de dados**.  
  
**Atualizar quando os metadados do objeto local estiverem ausentes**  
Especifica se o SSMA deve criar metadados locais se um objeto existir no banco de dados de destino, mas não localmente.  
Se você selecionar **Atualizar do banco de dados**, o SSMA selecionará a opção Atualizar do banco de dados quando a condição for atendida.  
Se você selecionar **gravar no banco de dados**, o SSMA excluirá o objeto do banco de dados quando a condição for atendida.  
Se você selecionar **ignorar**, o SSMA não executará nenhuma ação de atualização.   
O conjunto de opções padrão é **Atualizar do banco de dados**.  
  
