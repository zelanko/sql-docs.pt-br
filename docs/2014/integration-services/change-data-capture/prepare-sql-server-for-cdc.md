---
title: Preparar o SQL Server para CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- prepSqlSrv
ms.assetid: 20b51dbf-a545-4234-87ae-4228268a0fb2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e52f15a66c858aa1a04826f69342ba6a9dcd687e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804838"
---
# <a name="prepare-sql-server-for-cdc"></a>Preparar SQL Server para CDC
  O serviço Oracle CDC exige que todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino contenham o banco de dados MSXDBCDC. Você cria este banco de dados usando a ação Preparar ação do SQL Server no Console de Configuração do Serviço CDC. Isto cria um script especial que é executado para criar as tabelas exigidas, os procedimentos armazenados e outros artefatos necessários para este banco de dados. Esta tarefa só é feita uma vez para cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 Para obter mais informações sobre o banco de dados MSXDBCDC, consulte O banco de dados MSXDBCDC.  
  
 No Console de Configuração do Serviço CDC, clique em **Preparar SQL Server**. Se esta opção não estiver disponível, verifique se a opção **Serviços Locais CDC** está marcada no painel esquerdo do console.  
  
## <a name="options"></a>Opções  
  
### <a name="server-name"></a>Nome do servidor  
 Digite o nome do servidor em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está localizado.  
  
### <a name="authentication"></a>Autenticação  
 Selecione uma destas opções:  
  
-   **Autenticação do Windows**  
  
-   **Autenticação do SQL Server**: Se você selecionar essa opção, você deve digitar o **nome de usuário** e **senha** para o usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] você está se conectando.  
  
 Para preparar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Oracle CDC, o logon deve ter permissão de gravação no banco de dados MSXDBCDC. Insira as credenciais para um logon que tem permissão de gravação no banco de dados MSXDBCDC, como um membro da função `sysasmin` .  
  
### <a name="options"></a>Opções  
 Clique na seta para exibir opções disponíveis a serem configuradas. Você pode escolher deixar estas opções com o valor padrão. As opções disponíveis são:  
  
-   **Tempo limite de Conexão**: Digite o tempo (em segundos) que o Serviço CDC para Oracle espera por uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de exceder o tempo limite. O valor padrão é **15**.  
  
-   **Tempo limite de execução**: Digite o tempo (em segundos) que o Serviço do Windows do Oracle CDC espera que um comando seja executado antes de exceder o tempo limite. O valor padrão é **30**.  
  
-   **Criptografar Conexão**: Selecione **criptografar Conexão** para a comunicação entre o serviço Oracle CDC e o destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância usando uma conexão criptografada.  
  
-   **Avançado**: Digite as propriedades de conexão adicionais, se necessário.  
  
### <a name="view-script"></a>Exibir script  
 Clique em **Exibir Script** para exibir uma versão somente leitura do script de instalação. Um administrador do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode copiar este script no Console de Gerenciamento do SQL Server para editá-lo, se for necessário. Para obter mais informações sobre o Script Preparar SQL Server, consulte [Script de visualização Preparar SQL Server para Oracle CDC](prepare-sql-server-for-oracle-cdc-view-script.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como trabalhar com os serviços CDC](work-with-cdc-services.md)   
 [Como Preparar o SQL Server para CDC](prepare-sql-server-for-cdc.md)  
  
  
