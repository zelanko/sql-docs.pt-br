---
title: Como preparar o SQL Server para CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a327fa18-58f4-4e69-bb87-44faf47e20ef
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 38e13d715eaeee5e9ec5dc53c2297b0bbb697260
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85435713"
---
# <a name="how-to-prepare-sql-server-for-cdc"></a>Como Preparar o SQL Server para CDC
  O serviço Oracle CDC exige que todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino contenham o banco de dados MSXDBCDC. Você cria este banco de dados usando a ação Preparar SQL Server no Console de Configuração do Serviço CDC. Esta tarefa é feita uma vez somente para cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 Veja a seguir uma descrição sobre como preparar um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Change Data Capture da Oracle usando o Console de Configuração do Serviço CDC. Este processo cria o banco de dados MSXDBCDC e define as tabelas necessárias, os procedimentos armazenados e outros artefatos necessários.  
  
 A preparação do SQL Server para Oracle CDC é feito pelo Administrador de Serviço Oracle CDC. Para obter mais informações sobre a função de administrador de serviço CDC, consulte [funções de usuário para o serviço de captura de dados de alterações para Oracle por Attunity](user-roles.md).  
  
### <a name="to-enable-sql-server-for-cdc"></a>Para habilitar o SQL Server para CDC  
  
1.  No menu **Iniciar** , selecione **Configuração do Serviço CDC para Oracle**.  
  
2.  No painel esquerdo, selecione **Serviços Locais CDC** no painel **Ações** e clique em **Preparar SQL Server**.  
  
     Você também pode clicar com o botão direito do mouse em **Local CDC Services (Serviços Locais de CDC)** e selecionar **Prepare SQL Server (Preparar SQL Server)** .  
  
3.  Insira as informações necessárias na caixa de diálogo Preparando a Instância SQL Server para Oracle CDC. Para obter informações sobre como inserir as informações necessárias nessa caixa de diálogo, consulte [Prepare SQL Server for CDC](prepare-sql-server-for-cdc.md).  
  
     Para Preparar a instância do SQL Server para Oracle CDC, o logon deve ter permissão de gravação no banco de dados MSXDBCDC. Insira as credenciais para um logon que tem permissão de gravação no banco de dados MSXDBCDC, como um membro da função `sysasmin` .  
  
 **Observação**: clique em **Exibir Script** para exibir uma versão somente leitura do script de instalação. Um administrador do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode copiar este script no Console de Gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para editá-lo e executá-lo, se for necessário.  
  
## <a name="see-also"></a>Consulte Também  
 [Preparar o SQL Server para CDC](prepare-sql-server-for-cdc.md)  
  
  
